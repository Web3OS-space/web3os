# Building a web3os.space application

This guide shows how to write, test and publish an application. Every list of calls, scopes and refusal codes is in the
generated [SDK reference](reference.md); this guide links to it and never repeats it. The six reference applications in
`Apps/` (index: `Apps/README.md`) are the examples; every example below names its file.

## What an application is

An application is a front end, a folder of static files, plus a manifest. Both are published to the network, and a
registered name points at the manifest. The user's own node, the daemon, resolves the name, checks the user's grant and
serves the front end into a sandboxed frame of the web3os.space app. The frame talks to nothing but the host: each SDK
call goes to the host, which passes it to the daemon, and the daemon decides.

Sandbox rules (every response of the front-end route carries them):

- CSP `default-src 'self'; connect-src 'none'; sandbox allow-scripts`. The frame loads only its own files and opens no
  connection: no `fetch`, XHR or WebSocket, no data or blob media, no inline script or style.
- The frame has an opaque origin, so it has no cookies and no storage shared with other origins. Keep state in the
  user's stream (see [Content and streams](#content-and-streams)).
- The only way out is `postMessage` to the host, and the SDK does that for you.

The SDK is one ES module with no dependencies and no build step: `Apps/sdk/web3os-sdk.js`. Copy it into the root of
your front-end folder and import it:

```js
import { call } from './web3os-sdk.js';
const { address } = await call('identity.address', {});
```

`call(name, args)` resolves with the call's result, or rejects with `Error(code)`, where the code is one of the
[refusals](reference.md#refusals). `Apps/board/fe/board.js` (`run`) shows the usual wrapper.

## The manifest and scopes

The manifest names the application and lists what it may ask for:

```json
{"name":"board","services":[],"scopes":["content.read","identity","pay","streams.read","streams.write"],"authorShareBps":0}
```

(`Apps/board/manifest.json`; every reference application has one.)

- `name`: the registered name the manifest is published under. The daemon refuses a manifest whose name is not the
  name it resolves from (`ERR_APP_MANIFEST_NAME_MISMATCH`).
- `scopes`: the [scopes](reference.md#scopes) the application asks for. The user grants a subset. A call whose scope
  was not granted answers `ERR_APP_SCOPE_NOT_GRANTED`, and a call the SDK v1 does not serve answers
  `ERR_APP_SCOPE_UNSUPPORTED`.
- `services`: the job, goods and call services the application uses, by service id. `Apps/jobs/fe/jobs-config.js` and
  `Apps/shop/fe/shop-config.js` keep the ids the front end uses. They stay empty until a real service exists, and the
  front end says so instead of calling.
- `authorShareBps`: the author's share, in basis points, of every payment made through the application (`pay`,
  subscriptions). It is paid to the author's account and taken out of the merchant's amount.

The front end itself is not in the JSON: publishing builds the manifest from these fields plus the published front-end
folder (see [Publishing and updating](#publishing-and-updating)). A rebuilt manifest is a new version with a new
`appId`, and every grant is pinned to one `appId`.

## Sign-in

Each application gets its own key for each user. `identity.address` returns the user's address for this application,
and `identity.signIn` signs an EIP-4361 message once the user confirms it in the host's own sheet. The message's domain
must be the application name and its address the application address (`ERR_APP_SIGNIN_DOMAIN`,
`ERR_APP_SIGNIN_MESSAGE`). `Apps/board/fe/board-model.js` (`signInMessage`) builds a fixed message that carries no
clock, and `Apps/board/fe/board.js` (`start`) signs it. The calls and their rules are under
[`identity`](reference.md#scopes).

## Content and streams

- Streams: `streams.append` adds one entry, at most 1024 bytes of payload, to the user's own stream of this application.
  `streams.get` returns the verified entries of an owner's stream above a sequence number. The entries come as hex
  canonical bytes; decode them with `decodeAppEntry` from the SDK. Every user writes only their own stream, and a feed
  is the fold of the streams it reads. Examples: `Apps/board/fe/board-model.js` (posts and follows, `encodePost`),
  `Apps/events/fe/events-model.js` (events and replies), `Apps/polls/fe/polls-model.js` (votes).
- Content: `content.pick` lets the user choose an item of their Public library, and `content.get` reads a byte range of
  a root the application may read (`Apps/board/fe/board.js`, attachments).

The calls are under [`streams.read`, `streams.write` and `content.read`](reference.md#scopes).

## Waits, subjects and the delivery lines

A read can wait for news. `streams.get` and `messages.read` take an optional `waitSeconds` (0 to 20) and wait until a row
exists that the read would return, or until the time is up. A read that returns every stored row (no `afterSeq` on
`streams.get`, no `since` on `messages.read`) therefore answers at once whenever anything is stored, so give a wait the
cursor of the newest row you hold: `afterSeq` for a stream, and for messages `since`, which is the `last` of the previous
answer (the entry id of the newest row the daemon stores for the application, empty when none, then send no `since`).
A read with `since` answers only the rows after it.
`messages.read` also takes `replyTo` (the entry id
of a request) and then answers only the reply to that request. Both reads answer `delivery` (`live`, `polling` or
`unreachable`) and `outcome` (the worst result among the writers read: `ok`, `unreachable`, `invalid` or `forked`), so a
writer that could not be read never looks like an empty conversation. The application shows these words as the daemon gave
them and decides nothing from them. `Apps/chat/fe/chat-model.js` (`deliveryLines`) shows the two lines "Checking every 15
seconds" (`polling`) and "Cannot reach this conversation" (`unreachable`) and one sentence per outcome.

The three subject calls are shorthand for the typed calls, one subject router onto them (the subject table is ADR-240
(11)); each needs the scope of the typed call it maps to, and the SDK shim exports them as `publish`, `subscribe` and `request` and posts the wire
names `subjects.publish`, `subjects.subscribe` and `subjects.request` (the bare name `subscribe` is the payment call):

| Subject call | Typed equivalent |
| --- | --- |
| `publish {subject, data}` | `streams.append` for a stream subject, `messages.send` for a message subject |
| `subscribe {subject, afterSeq, waitSeconds}` | `streams.get` or `messages.read`, with `waitSeconds` |
| `request {subject, data, waitSeconds}` | `messages.send`, then `messages.read {replyTo}` for the first answer |

`data` is base64. The host forwards `waitSeconds` and every field of the call as given and the answer comes back unchanged. A stream entry is readable by every
public node as it is published, so never put anything in a stream that must stay private. A request to a group is answered
by some other current member, not by a fixed one: the application compares `from` to tell who answered.

The SDK shim has one helper for waiting: `wait(kind, name, args, again)` with kind `messages` or `stream`. It keeps at most
one open wait per kind, so an application has at most two open waits. It calls `name` with `args`, and while
`again(answer)` says the answer brought nothing it issues the same call once more; it has no timer, no cursor and no other
retry, and it returns an `unreachable` answer as it is. The call you pass must carry the cursor (see above): a wait
without one is answered at once and `wait` would issue it again without pause.

## Payments, subscriptions, jobs, metered calls and goods

Money never moves without the user: every paying call opens the host's own confirmation sheet. The calls marked
"Confirmed by the user" in the [call table](reference.md#calls) work this way, and the application only gets the
answer.

- `pay`: one payment to a merchant from the application's sub-escrow (`Apps/board/fe/board.js`, tips).
  `subscribe` and `subscription.voucher` cover recurring payments.
- Jobs: `jobs.offers`, `jobs.order`, `jobs.status` and `jobs.result` (`Apps/jobs/fe/jobs.js`).
- Metered calls: `calls.invoke` sends one request to a call service of the manifest, paid per answered call. Its grant
  carries the waiver text versions the host shows.
- Goods: `goods.offers`, `goods.order` and `goods.status` (`Apps/shop/fe/shop.js`).

The host-only calls (`goods.placed`, `jobs.placed`) belong to the host. An application never calls them; see the
"Host only" column of the [call table](reference.md#calls).

## Messaging

The `messages` scope gives the application a mailbox of its own for each user: `messages.me` (the mailbox id and
contact code), `messages.send`, `messages.read`, `messages.seen`, `messages.allow` and `messages.block`, groups, and
attachments shared as Private links. `Apps/chat/fe/chat.js` uses all of them; the list is under
[`messages`](reference.md#scopes).

## Handling refusals

Every refused call rejects with one code from the [refusal table](reference.md#refusals). The table gives each code's
origin (the daemon, or the host without reaching the daemon) and its action:

- `retry`: the same call may succeed later.
- `ask-user`: the user has to act first, for example grant a scope, confirm a sheet or, after an update, grant the new
  manifest (`ERR_APP_GRANT_STALE`: a grant stays pinned to the manifest it was given for).
- `fix-app`: the application or its manifest has to change.

Map each code to one plain sentence for the user and never show the raw code alone. `Apps/shop/fe/shop-model.js`
(`REFUSALS`, `refusalSentence`) and `Apps/chat/fe/chat-model.js` do this.

## Publishing and updating

You publish from the web3os.space app's publish screen, in the order below. Start the app against your node A: set
`Web3OS_GATEWAY_ADDR=127.0.0.1:<port>` when you start it, where `<port>` is node A's gateway port (`devnode.sh status`
prints `node A gateway http://127.0.0.1:<port>`; the base port is 27000 unless you set `DEVNODE_BASE_PORT`, and node A is
base + 50). The screens the steps name, as the app labels them:

- Upload: the Discover tab's Upload button, then "Batch upload" with the folder's path typed into the path box; a folder
  goes up with everything under it.
- Publish an application: the Apps tab (shown when your node reports the apps feature), then "Publish an application". The
  form has Application name, Front-end folder (your uploaded folders), Services (one per line), Scopes (one per line),
  Author share (basis points) and "Build application".

The walkthrough script
`Scripts/testnet/devwalk.sh` runs the same steps against a local developer node (`Scripts/testnet/devnode.sh up`) with
`Apps/board`. Each step names the step id the script uses, and `Scripts/testnet/devwalk_test.sh` checks that the guide
and the script list the same ids in the same order.

`devnode.sh up` takes seven to ten minutes on one host (389 s and 559 s were measured). It brings up three validators, a faucet and six storage nodes,
A to F, on loopback. Node A is the author's node. B to F hold your published files: each object of `Apps/board/fe` is one
segment of five columns on five distinct nodes, and the uploader holds none of them. `up` signs a seed account in on each
holder, funds it from the faucet, binds the node's peer key to it and bonds its storage stake. It ends with:

```
devnode: ok: holders B C D E F bound and staked (seed accounts 10 .. 14)
devnode: up in <seconds> s; state /tmp/web3os-devnode-<user>/devnode.env
devnode: holders count for column placement from epoch 1 (chain time P >= 604800 s); GET /node/checks placement on B to F
```

A peer binding counts from the epoch after the one it was made in. The developer node's chain starts at epoch 0, and an
epoch is one week of chain time, which is never shortened. So for the first week, `devwalk.sh publish` stops before step 1
with exit 3 and names each holder's wait:

```
devwalk: WAIT step fe-upload: holders not yet eligible for column placement: B: binding counts from epoch 1 (starts 2026-11-24T12:48:35Z); C: ...; run the phase again then
```

The first run after `up` can answer `B: not read yet` for every holder: asking is what queues the node's read of its
placement check. Run the phase again a moment later and the answer carries the time above. Leave the node running
(`devnode.sh status`) and run the phase again after that time. A holder check that answers anything other than `ok` or
`wait` fails the step, because `up` bound and staked every holder. Only `placement` gates the walk: `GET /node/checks` also
lists `host`, which fails `ERR_ALLOT_ABOVE_FREE` on a host whose free disk is smaller than the 1 TiB each holder declares,
and `audit`, which waits; neither stops it.

As the author, on your node (`devwalk.sh publish`):

1. Upload the front-end folder to your Vault. <!-- step: fe-upload -->
   `Apps/board/fe` is not the folder to upload as it is: it holds the model tests and no SDK, so the page's
   `import './web3os-sdk.js'` would find nothing. Stage a copy: `index.html`, `board.js`, `board-model.js`, `board.css`
   and `Apps/sdk/web3os-sdk.js` at the copy's root (`devwalk.sh` does this in `fe_copy`), and upload that folder.
2. Publish the folder: the Publish sheet commits it, the matchers clear it, then you sign the reveal and it is public. <!-- step: fe-publish -->
   In the app, open "Publish an application": the folder's row has a Publish button that opens the sheet (the Upload
   screen's own Publish switch commits each file of the folder, not the folder, and "Build application" then answers
   "That folder is not a published folder yet."). Publish, who is selling, and the confirmation take it to stage `commit`, and
   the sheet then shows Sign: your account signs the commit (a confirmation, then the six-digit code of your authenticator
   app). Signing needs your account's device key, so use an account you created or restored in the app; with a node that was
   signed in by seed only, the sheet answers with a link to "Account & keys" and `devwalk.sh` signs with the seed instead.
   Public publishing needs the network's matchers. On a network that seats none (the public testnet until the licensed
   hash lists exist), the row has no Publish button and the commit is refused before any signature or fee with 503
   `ERR_NOT_AVAILABLE` `publish-public`; the script prints a `GATED-A4` line from that refusal. Where matchers are seated
   but cannot clear yet, the publication stays at stage `clearance` and the script prints the same line. Either way step
   3 answers 409 `ERR_APP_FRONTEND_UNPUBLISHED`, which ends the phase. `DEVWALK_STRICT=1` makes that a failure.
3. Build the manifest from its fields and the published folder (`POST /apps/manifest`); it lands as a Private file in your Vault. <!-- step: manifest-build -->
   In the app, fill the form (scopes one per line: `content.read`, `identity`, `pay`, `streams.read`, `streams.write`) and
   press "Build application"; it answers "That folder is not a published folder yet." until the folder's publication is public.
4. Publish the manifest file the same way as the folder. <!-- step: manifest-publish -->
5. Register the name: commit it, then register it pointing at the manifest file in a later block. <!-- step: name-register -->

A name resolves only from the sealed root of its publication's epoch. The wait is the same rule on the testnet and on
mainnet, not a limit of the developer node: test the model first (the model tests run without a network), publish once,
and use the application after the seal. The epoch is one week of chain time, so the next steps run once that epoch has
sealed.

As a user, on a second node with a second account (`devwalk.sh use`):

6. Open the name: the node resolves it to the manifest's `appId` and its scopes. <!-- step: user-resolve -->
7. Grant the application its scopes; the grant is pinned to that `appId`. <!-- step: user-grant -->
8. The front end loads (`fe/index.html` of the granted root). <!-- step: user-frontend -->
9. Sign in (`identity.address`, then `identity.signIn`). <!-- step: user-signin -->
10. Post (`streams.append`). <!-- step: user-append -->
11. Read it back (`streams.get`). <!-- step: user-read -->
12. A call outside the granted scopes is refused (`messages.me` answers `ERR_APP_SCOPE_NOT_GRANTED`). <!-- step: user-scope-refusal -->

To update, as the author:

13. Publish the changed front-end folder. <!-- step: update-fe-publish -->
    To publish a changed front end, upload the folder again; that makes a new folder record, and the earlier version stays a
    loose row in `GET /vault` until it is deleted by its cid.
14. Build its manifest: a new `appId`. <!-- step: update-manifest-build -->
15. Publish the new manifest file. <!-- step: update-manifest-publish -->
16. Re-point the name at the new manifest file. <!-- step: update-repoint -->

Once the new manifest's epoch has sealed (`devwalk.sh stale`):

17. The user's existing grant stays pinned to the manifest it was given for. A grant of the old `appId` after the re-point is refused (`ERR_APP_GRANT_STALE`), and the user grants the new manifest to move on. <!-- step: user-stale -->

## The model-test loop

Keep everything that is not DOM or SDK in a pure model module, with no clock and no randomness, so the same input
always gives the same output, and test it with Node's built-in runner. Every reference application does this
(`Apps/board/fe/board-model.js` and `Apps/board/fe/board-model.test.mjs`, likewise for the others; the SDK has
`Apps/sdk/web3os-sdk.test.mjs`). Run all of them with:

```sh
node --test "Apps/**/*.test.mjs"
```

To test the calls an application makes without a browser, pass a fake window as the last argument of `call` (and of
`publish`, `subscribe`, `request` and `wait`). The SDK posts each call to `win.parent` and listens on `win` for the answer
`{id, result}` or `{id, error}`, so a fake host is a few lines:

```js
const w = { l: null, addEventListener: (t, f) => { w.l = f; },
  parent: { postMessage: (m) => queueMicrotask(() => w.l({ data: { id: m.id, result: { address: '0x…' } } })) } };
const { address } = await call('identity.address', {}, w);
```

`Apps/board/fe/board-host.test.mjs` runs the sign-in and the post-and-read-back this way, and a thrown code in the fake host
arrives as `Error(code)`, the way a refusal does.

Then run the walkthrough against a local node: `Scripts/testnet/devnode.sh up`, `Scripts/testnet/devwalk.sh publish`,
and after the epoch seals `devwalk.sh use` and `devwalk.sh stale`. `devnode.sh down` stops the node. Each phase prints one
line per step. A failure (exit 1) names the step id and the daemon's answer. A `GATED` line (exit 0) names a state the
local network cannot pass yet, and a `PENDING` line (exit 0) a step this release cannot run yet. A `WAIT` line (exit 3) names the chain time the phase waits for: the holders' bindings
before `publish`, and the epoch seal before `use` and `stale`.
