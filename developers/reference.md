# Application SDK reference

Generated from Extensible_Upgradable/ClientGateway/AppCallRegistry.go; do not edit. The argument and result schemas of every call are in Extensible_Upgradable/ClientGateway/app_sdk_calls.json.

An application declares its scopes in its manifest and the user grants them; a call whose scope the user did not grant is refused with ERR_APP_SCOPE_NOT_GRANTED.

## Scopes

| Scope | Calls |
| --- | --- |
| `calls` | `calls.invoke` |
| `content.read` | `content.get`, `content.pick` |
| `goods` | `goods.list`, `goods.offers`, `goods.order`, `goods.status` |
| `identity` | `identity.address`, `identity.signIn` |
| `jobs` | `jobs.list`, `jobs.offers`, `jobs.order`, `jobs.result`, `jobs.status` |
| `messages` | `groups.create`, `groups.setMembers`, `messages.allow`, `messages.attach`, `messages.block`, `messages.me`, `messages.read`, `messages.seen`, `messages.send` |
| `pay` | `pay`, `subscribe`, `subscription.voucher` |
| `streams.read` | `streams.get` |
| `streams.write` | `streams.append` |

## Calls

Confirmed by the user: the host shows its own sheet and answers the call once the user confirms. Host only: an application's call is refused; only the host calls it. Metered: every answered call is paid from the application's allowance.

| Call | Scope | What it does | Confirmed by the user | Host only | Metered |
| --- | --- | --- | --- | --- | --- |
| `calls.invoke` | `calls` | Sends one request to a call service of the manifest and returns its answer, paid from the sub-escrow. | no | no | yes |
| `content.get` | `content.read` | Reads a byte range of a root the application may read. | no | no | no |
| `content.pick` | `content.read` | Lets the user pick one item of their Public library and returns its root. | yes | no | no |
| `goods.list` | `goods` | Lists the goods orders this application opened, newest first, at most 50 ids. | no | no | no |
| `goods.offers` | `goods` | Lists the offers of a goods service of the manifest, with each seller's card. | no | no | no |
| `goods.order` | `goods` | Opens the host's order sheet for a goods offer; the user confirms, types the address and signs. | yes | no | no |
| `goods.placed` | `goods` | Links a confirmed goods order to the application; the host calls it, never the application. | no | yes | no |
| `goods.status` | `goods` | Returns the status of a goods order this application opened. | no | no | no |
| `groups.create` | `messages` | Creates a message group of the given members. | no | no | no |
| `groups.setMembers` | `messages` | Replaces the members of a group the user owns. | no | no | no |
| `identity.address` | `identity` | Returns the user's address for this application. | no | no | no |
| `identity.signIn` | `identity` | Signs an EIP-4361 sign-in message with the application address once the user confirms it. | yes | no | no |
| `jobs.list` | `jobs` | Lists the job orders this application placed, newest first, at most 50 ids. | no | no | no |
| `jobs.offers` | `jobs` | Lists the offers of a job service of the manifest for a number of units. | no | no | no |
| `jobs.order` | `jobs` | Opens the host's job order sheet; the user picks an offer, confirms and signs. | yes | no | no |
| `jobs.placed` | `jobs` | Links a confirmed job order to the application and sends its input; the host calls it, never the application. | no | yes | no |
| `jobs.result` | `jobs` | Returns the result root of a delivered job order this application placed. | no | no | no |
| `jobs.status` | `jobs` | Returns the status of a job order this application placed. | no | no | no |
| `messages.allow` | `messages` | Lets a peer write to the user's application mailbox. | no | no | no |
| `messages.attach` | `messages` | Uploads a file as a Private share and returns the link to attach to a message. | no | no | no |
| `messages.block` | `messages` | Drops a peer's future messages. | no | no | no |
| `messages.me` | `messages` | Returns the user's mailbox id and contact code for this application. | no | no | no |
| `messages.read` | `messages` | Returns the verified, opened messages of every conversation. | no | no | no |
| `messages.seen` | `messages` | Tells the sender that the user has seen a message. | no | no | no |
| `messages.send` | `messages` | Sends a message to a peer or a group. | no | no | no |
| `pay` | `pay` | Pays a merchant from the sub-escrow once the user confirms the host's payment sheet. | yes | no | no |
| `streams.append` | `streams.write` | Appends one entry to the user's stream of this application. | no | no | no |
| `streams.get` | `streams.read` | Returns the verified entries of an owner stream above a sequence number. | no | no | no |
| `subjects.publish` | the subject's call | Publishes data on a networked subject through the typed call the subject maps to. | no | no | no |
| `subjects.request` | the subject's call | Sends a request to a peer or a group and waits for the first answer. | no | no | no |
| `subjects.subscribe` | the subject's call | Returns the messages of a networked subject above a stream sequence, waiting for one. | no | no | no |
| `subscribe` | `pay` | Opens a subscription to a merchant's offer once the user confirms the host's subscription sheet. | yes | no | no |
| `subscription.voucher` | `pay` | Signs the vouchers of the current period of a subscription. | no | no | no |

## Refusals

A refused call answers an error code. Origin daemon: the daemon answers it; origin host: the host answers it without reaching the daemon. Action retry: a later identical call can succeed; ask-user: the user has to act first; fix-app: the application or its manifest has to change.

| Code | Origin | Meaning | Action |
| --- | --- | --- | --- |
| `ERR_APP_BAD_ARGS` | daemon | The call body is not JSON of the call's shape. | fix-app |
| `ERR_APP_CALL_BODY` | daemon | A calls.invoke body is outside 1 to 65536 bytes. | fix-app |
| `ERR_APP_CALL_FAILED` | daemon | The request was sent and timed out or did not answer ok. | retry |
| `ERR_APP_CALL_NO_OFFER` | daemon | Every offer of the call service was refused or unreachable. | retry |
| `ERR_APP_CALL_SERVICE` | daemon | A calls.invoke serviceId is not in the manifest or is not a call service. | fix-app |
| `ERR_APP_CONTENT_NOT_PICKABLE` | daemon | The root is no item of the user's Public library. | ask-user |
| `ERR_APP_CONTENT_RANGE` | daemon | A content.get length is outside 1 byte to 1 MiB or the offset is at or past the end. | fix-app |
| `ERR_APP_FRONTEND_UNPUBLISHED` | daemon | The front end is no Vault folder or its publication is not revealed. | fix-app |
| `ERR_APP_GOODS_BUSY` | host | A goods order sheet of this application is already open. | retry |
| `ERR_APP_GOODS_CANCELLED` | daemon | The user closed the goods order sheet without ordering. | ask-user |
| `ERR_APP_GOODS_SERVICE` | daemon | A goods serviceId is not in the manifest or is not a goods service. | fix-app |
| `ERR_APP_GRANT_STALE` | daemon | The granted manifest is no longer the name's current manifest, so the user must grant again. | ask-user |
| `ERR_APP_JOB_CANCELLED` | host | The user closed the job order sheet without ordering. | ask-user |
| `ERR_APP_JOB_INPUT` | daemon | A jobs.order input is outside the application's readable set, or the params exceed 65536 bytes. | fix-app |
| `ERR_APP_JOB_UNKNOWN` | daemon | The order is not one this application placed. | fix-app |
| `ERR_APP_MANIFEST_BOUNDS` | daemon | A manifest field is outside the v1 bounds. | fix-app |
| `ERR_APP_MANIFEST_NAME_MISMATCH` | daemon | The manifest the name resolves to carries another name. | fix-app |
| `ERR_APP_MANIFEST_NONCANONICAL` | daemon | The manifest bytes are not the one canonical encoding. | fix-app |
| `ERR_APP_MSG_FULL` | daemon | The application's peer or group table is full. | fix-app |
| `ERR_APP_MSG_STORE` | daemon | The daemon could not read or write the application's message store. | retry |
| `ERR_APP_NAME_LAPSED` | daemon | The application's name is past its active term. | fix-app |
| `ERR_APP_NOT_FOUND` | daemon | The name has no registry row, or the front end has no such file. | fix-app |
| `ERR_APP_NOT_GRANTED` | daemon | The user has not granted the application. | ask-user |
| `ERR_APP_PAY_ALLOWANCE` | daemon | There is no open sub-escrow, or the payment exceeds what it has left. | ask-user |
| `ERR_APP_PAY_BUSY` | host | A payment or order sheet of this application is already open. | retry |
| `ERR_APP_PAY_CANCELLED` | host | The user closed the payment or subscription sheet without paying. | ask-user |
| `ERR_APP_PAY_ESCROW_OPEN` | daemon | The application already has an open sub-escrow. | fix-app |
| `ERR_APP_PAY_TERMS` | daemon | The payment's merchant, offer id, amount or text versions do not encode. | fix-app |
| `ERR_APP_PICK_BUSY` | host | A content picker sheet of this application is already open. | retry |
| `ERR_APP_PICK_CANCELLED` | host | The user closed the content picker without picking. | ask-user |
| `ERR_APP_SCOPE_NOT_GRANTED` | daemon | The user did not grant the call's scope. | ask-user |
| `ERR_APP_SCOPE_UNSUPPORTED` | daemon | The call is not one the SDK v1 serves to an application. | fix-app |
| `ERR_APP_SIGNIN_DOMAIN` | daemon | The sign-in message's domain is not the application name. | fix-app |
| `ERR_APP_SIGNIN_MESSAGE` | daemon | The sign-in message is not an EIP-4361 message for the application address in printable ASCII. | fix-app |
| `ERR_APP_STREAM_BAD_ENCODING` | daemon | A stream entry does not decode to its one canonical form. | retry |
| `ERR_APP_STREAM_BAD_NAME` | daemon | A stream entry's name is not a normalized application name. | fix-app |
| `ERR_APP_STREAM_BAD_SIGNATURE` | daemon | A stream entry's signature does not verify. | retry |
| `ERR_APP_STREAM_CHAIN_FORK` | daemon | A stream entry takes a sequence number already used or names another previous entry. | retry |
| `ERR_APP_STREAM_CHAIN_GAP` | daemon | A stream entry skips a sequence number. | retry |
| `ERR_APP_STREAM_FULL` | daemon | The stream already holds its last entry. | fix-app |
| `ERR_APP_STREAM_NO_RECOVER` | daemon | No signer can be recovered from a stream entry's signature. | retry |
| `ERR_APP_STREAM_PAYLOAD` | daemon | A stream payload is empty or over 1024 bytes. | fix-app |
| `ERR_APP_STREAM_WRONG_NAME` | daemon | A stream entry carries another application's name. | retry |
| `ERR_APP_STREAM_WRONG_OWNER` | daemon | A stream entry is signed by another owner. | retry |
| `ERR_APP_SUB_CANCELLED` | daemon | The subscription was cancelled, withdrawn or has expired. | ask-user |
| `ERR_APP_SUB_FUNDS` | daemon | The period voucher exceeds the subscription's unsigned balance. | ask-user |
| `ERR_APP_SUB_OPEN` | daemon | The application already has an active subscription to that merchant and offer. | fix-app |
| `ERR_APP_SUB_UNKNOWN` | daemon | No subscription of this application has that escrow, or its opener is not yet on chain. | retry |
| `ERR_APP_UPDATE_ARCH` | daemon | The client update check names an architecture that makes no valid artifact platform. | fix-app |
| `ERR_APP_UPDATE_CHANNEL` | daemon | The client update check names a channel other than play or direct. | fix-app |
| `ERR_APP_UPDATE_VERSION_CODE` | daemon | The client update check's versionCode is not one canonical unsigned decimal. | fix-app |
