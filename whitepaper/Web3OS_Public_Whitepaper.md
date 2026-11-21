# Web3OS — Public Whitepaper

> **web3os.space: a decentralized operating system built up from storage on its own chain. Persistent storage first, then applications, then CPU, GPU and AI services, all settled natively on Web3OSChain.**
> This is the **minimal-disclosure public edition**: vision, capabilities, tokenomics, per-role usage and risk/compliance only. It **omits internal module architecture, consensus/security implementation, and operational secrets** (those remain private; the protocol core is BSL 1.1-licensed — auditable, each version converting to full open source no later than four years after its release). The authoritative, precise rules are the full whitepaper and on-chain governance.
>
> **Currently in testnet; token and parameters may change. This is not investment advice; digital assets are high-risk.** Features marked *(planned)* are specified but not yet live; the full whitepaper's Appendix I lists what has landed.

---

## 1. What is Web3OS

### From storage to an operating system

**Web3OS (web3os.space) is a decentralized operating system, and storage is its starting point.** An operating system needs persistent storage before anything else: applications, their state and their users' files must survive restarts, operators leaving and companies closing. Blockchains settle value well but do not keep data; cloud drives keep data but one company owns it. web3os.space starts where both stop:

1. **Persistent storage (live on testnet).** Files are compressed and encrypted on the device, erasure-coded across independent storage nodes, and paid only against storage proofs the chain checks.
2. **Applications on that storage *(being built)*.** Every application is a content-addressed service image whose code and data live in the same storage; messaging is the first platform service.
3. **Memory, CPU, GPU and AI *(being built; GPU container passthrough is in the code, the public market is planned)*.** Compute and hosting are leases of the same kind, paid from escrow per period served, so applications and AI workloads run on the network the way files are stored on it.
4. **Virtual and augmented reality, the Web3 metaverse *(planned)*.** 3D assets are stored as content, shared worlds run on regional hosting leases and rendering on GPU leases, so VR and AR applications use the same storage, payments and leases; web3os.space will build such applications itself.

**Its own chain is the second advantage.** Web3OSChain is a sovereign chain, not a contract on someone else's: every payment, creator share, storage reward and lease settles natively on it, and the rules change only by on-chain governance.
- **No gas to think about for everyday use.** Search, browse and preview are free within a daily quota per account. Downloads are paid per chunk with off-chain signed vouchers settled in one claim, so a download is not a stream of fee-paying transactions, and the discovery cost is inside the price (§13.2, no separate gas charge).
- **One coin.** Any chain fee is paid in WEB3OS, never ETH; withdrawing to Ethereum needs no ETH either, because the bridge charges the Ethereum gas in WEB3OS.

The rest of this section describes what runs today: the storage network and the marketplace on it.

Web3OS is today a **community-run network drive ＋ media/knowledge marketplace**. You can store files, find data, and buy/sell video, music, documents, games, and software. **No single company runs it** — people around the world ("miners") run it on their own disks and machines, so **no single party can delete lawful content, and censorship is hard; illegal content is removed under the published rules (§14), and a Private file that shares bytes with removed content loses them.**

- **How search works:** built-in AI scores content by *value* — good content surfaces by merit, **not ads or keyword SEO**.
- **You control your data:** private data is encrypted on your device; miners only see ciphertext (encrypted, but not zero-knowledge secret; see section 7 below).
- **Free account, tokens only when paying:** browsing/searching/previewing is free but needs an account (created on your device in the app, or a wallet you connect), because every search uses the network's resources; no ID. You need a little token only to download or to earn by uploading.

The native token **Web3OS** lives on Web3OS's own chain, **Web3OSChain**, and is used for payments, staking, mining rewards, and governance; wrapped copies can move to Ethereum for trading.

### Where the idea comes from: from seeding credit to a usable token

Web3OS started from a simple question about file sharing: **why do people keep sharing a file after they already have it?**

**BitTorrent (BT)** proved that strangers can move huge files to each other with no central server: everyone who downloads a piece also uploads it to others. But BT has no reward for staying. Once people finish a download they close the client, nobody keeps the file online, and sooner or later the file dies.

**Private trackers (PT)** fixed that with credit. An invite-only site records how much each member uploads and downloads. Members who keep files online ("seeding") earn **upload credit** or bonus points, and they need that credit to keep downloading. Seeding becomes worth something, so files on good PT sites stay alive for years.

PT credit still has limits:
- **It is locked inside one site.** You cannot move it, sell it or use it anywhere else.
- **You cannot buy it.** Someone with no spare disk or bandwidth has no fair way in.
- **One administrator controls it.** The site can change the rules, wipe balances or shut down, and every point is lost with it.
- **It relies on what each client reports.** A client that lies about its upload numbers can inflate its credit.
- **Creators get nothing.** The credit rewards people who share a file, never the people who made it.

**Web3OS keeps the PT principle and turns the credit into a token you can actually use.** People who keep files stored and online, and who deliver downloads, earn **Web3OS**, the network's native token. The token is:

| PT upload credit | WEB3OS token |
| :-- | :-- |
| Earned by seeding on one site | Earned by storing and delivering files for the whole network |
| Counted from client self-reports | Paid only against storage proofs the chain checks |
| Spent only on that site's downloads | Spent on any paid download, storage, compute or `.web3os` names |
| Cannot be bought or transferred | Transferable once the liquidity pool is built and deep enough (until then earned coins are for use on the network only, see "Launch liquidity" in section 3); from then on anyone without spare disk can buy it to pay for downloads |
| Rules and balances set by an admin | Rules public and on chain, changed only by community governance |
| Creators earn nothing | Creators receive the largest share of every paid download |

In short: **seeding earns credit, and in Web3OS that credit is a token you can trade, buy and spend on downloads.** It is a utility token for using the network, not a promise of profit (see the honest note below and §6–§7).

### Why take part — what each role gets you (in everyday words)

Think of Web3OS as a **town library, a market and a court run by the townspeople themselves**. Nobody owns the building; everyone who helps keep it running gets something back. You start as a visitor and add roles when you want to.

| If you are… | You do | What you get | What it costs or risks |
| :-- | :-- | :-- | :-- |
| **A visitor** (Role 1) | Search, browse and preview | Results ranked by value, not by who paid for ads; a free daily quota; no ID | Nothing but a free account |
| **A buyer** (Role 2) | Pay to download a file | You pay the creator and the people who deliver it, not a middleman; a refund path if the file is a virus, a degraded variant or not as described; purchases can move into your own encrypted vault | The price of the file; a small deposit when you file a refund claim, lost only if the claim is abusive |
| **A creator / uploader** (Role 3) | Publish your videos, music, documents or software | The largest share of every paid download, paid automatically on chain; free publishing within your allowance; AI previews and classification; subtitles in the original language and English made on your own devices, translated live into each reader's language on their device *(planned)*; protection against copycats, because deposits and juries stand between you and false accusations | Publishing can't be undone; earnings wait in escrow until you register as the copyright holder; cheating (malware, fakes, re-cuts) costs your earnings and your reputation |
| **A miner** (Role 4) | Lend spare disk space and bandwidth | Tokens for keeping files safe and online, plus a fee for every download you deliver; the delivery fee comes from real usage, not only from new coins | A disk and a connection that stay up; a stake that is cut only by an adjudicated case outcome, while a missed or false storage proof costs the pay |
| **A compute / hosting provider** (Role 4b) *(planned)* | Rent out a GPU or run other people's containers | Pay drawn from the customer's escrow for every period you serve | A stake, burned only for proven resource fraud; repeated outages end the lease and lower your reputation |
| **A staker / voter** (Role 5) | Lock tokens with a validator | A say in fees, rules and how the shared fund is spent; a floating yield (never a fixed, guaranteed rate) | Locked tokens; their price can fall; vote weight is capped so no single account rules |
| **An app developer** (Role 7) | Build apps, alone or with an AI coding assistant | No server to run; sign-in, storage, payments and messages built in; your share of every sale or subscription in your app, paid automatically | Your time; the storage of your app's files is paid like any other file |
| **A juror / reporter** (Role 6) | Judge disputes the AI can't settle, or report bad files | A reward for careful rulings; valid reports raise your reputation; a safer market for everyone, including you | A deposit that is lost for careless or malicious work |

**Why this is better than a normal platform:** there is no company in the middle that can delete lawful content or your files at will (illegal content is removed under the published rules, and a Private file sharing bytes with removed content loses them), change the payout split overnight or sell your attention to advertisers. The rules are public, the money moves automatically, and anything that costs someone money or reputation is decided by fixed rules plus a human jury, never by an AI alone.

**Honest note:** nothing here promises a profit. Token prices move and can go to zero, rewards depend on how much the network is actually used, and several features are still *(planned)*. The full rules for each role are in §4, the penalties in §5 and the risks in §6–§7.

---

## 2. Capabilities (plain language)

Web3OS's built-in AI assistant automatically:

- **Understands your files:** detects video/music/image/document/game; generates previews, classification, original-language and English subtitles, and **live translation into your language on your own device** *(planned)*.
- **Guards safety:** scans when you publish — **known viruses and trojans, disguised file types, duplicates and known illegal content are blocked by deterministic checks** and never get listed; brand-new malware can still slip through.
- **Protects buyers:** if you buy a virus/degraded-variant/not-as-described item, you can dispute it: automatic checks are deterministic detectors, never an AI guess, and the rest goes to a **human jury**.
- **Protects honest uploaders:** obvious bad files are blocked before yours, so you're not lumped in with them; and to falsely accuse you, someone must post a deposit and risks a reputation penalty — so frivolous reports don't pay.

**Honest limits of AI:** AI is good at catching *known* bad things and *obvious* impersonation/duplication; **brand-new malware or sophisticated re-cuts (re-editing, speed-changing, inserting ads to resell)** may slip past → those go to a **human jury**. **Any final decision involving money or penalties is made by "rules ＋ human jury", never AI alone** — to prevent a fooled AI from punishing you.

Capability areas (without disclosing internals): decentralized storage & delivery, GPU compute and container hosting, value-oriented search & discovery, multilingual subtitles/translation, content safety & dispute arbitration, an optional decentralized compute market, and decentralized naming.

---

## 3. Tokenomics

| Item | Detail |
| :-- | :-- |
| Token / standard | **Web3OS**, native to Web3OSChain (wrapped on Ethereum through an audited bridge), decimals **9** |
| Total supply (fixed cap) | **1,000,000,000 WEB3OS (1B)** |
| Price | No reference or target price; the market sets it. $0.20 is only the cold-start settlement price used until the liquidity pool is deep enough (**not a price promise**); mainnet launches with no token sale offered to anyone, and the project sells no Web3OS at launch with one disclosed exception: it sells coins from the small necessary-fees slice (0.5%), at the market price, to pay its audit, legal and set-up bills (see "Necessary fees" below). The protocol-owned liquidity vault sells nothing and holds no liquidity position, and no other project funds are converted to other assets. Building the liquidity pool and selling by the vault can be switched on only by a governance vote held after written legal opinions for the US and the EU. Until that pool is built and deep enough, the coins the network pays you are for use on the network only and cannot be sent to another account (see "Launch liquidity" below) |
| Allocation (mainnet intent) | **~80% mining reserve** (earned over the curve) / **genesis premint 4%** — protocol-owned liquidity seed 2.5%, security-bounty bucket 1% (3M cap, the rest burned at genesis), necessary fees 0.5%; nothing sold at launch except part of the necessary-fees slice, to pay the project's bills / **remainder ~14–16% (ecosystem·team·treasury·growth) streamed gradually from the curve — vesting·governance·timelock, NOT a genesis bag** |
| Release | 80% mining reserve released on a **curve that only declines and never ends: 10% less each year by default; each year the chain suggests the cut from the past year's price (0–20%) and the community confirms it by vote**; **non-mining buckets are all vesting ＋ governance control ＋ timelock**, milestone-bound, no early dumping |
| Inflation control | **Burn-Mint Equilibrium (BME):** above the durability floor, zero verified demand → zero minting; adaptation can only reduce issuance, never over-issue → net issuance bound never broken |
| Staking yield (stake bonded to a validator only: own bond or delegation) | **Floating, not a fixed guaranteed rate** (target range set by governance); paid from the existing emission curve, **no out-of-curve issuance → non-inflationary** |
| Network revenue | Public download fees, prepaid Private storage, decentralized compute and container hosting, `.web3os` domain registration/renewal |

**Testnet has exactly the same supply as mainnet: a fixed 1,000,000,000, the same curve and the same 4% genesis premint; on testnet the premint only funds the test faucet and the validators' starting stake, and test tokens have no value.** Mainnet uses a **genesis premint of 4%** earmarked solely for the protocol-owned liquidity seed (2.5%), the security-bounty bucket (1%; 3M cap, the rest burned at genesis) and necessary fees (0.5%); a later CEX listing is funded by a governance vote from the treasury stream; team/treasury/growth are **streamed from the curve (vesting·governance·timelock), not a genesis bag**; the ~80% mining reserve releases over the curve.

**In plain language — what the genesis premint is for.** When the network goes live, almost no coins exist yet — miners earn them slowly, year after year. But a few things need coins on day one, or the network can't run or be traded, so a **small starting batch (4%)** is pre-made and used **only** for three launch needs:

1. **Liquidity (2.5%, the biggest slice).** To trade Web3OS there must be a pool holding coins on *both* sides (Web3OS + USDC). Without it, one buy spikes the price and you can't sell back. This batch builds that pool, and no ETH or stablecoin has to be raised for it: after the legal opinions and the vote, the vault places the whole batch in the pool as Web3OS only, from the opening price upward. Whoever pays USDC into the pool receives Web3OS from it, each coin a little dearer than the one before, and the USDC stays in the pool as its other side, where later sellers are paid from it; nobody at the project receives it. The vault has no withdrawal key; the signers' Safe can remove liquidity only after the time lock and only to the chain treasury escrow or the winter-reserve account (anti-rug).
2. **Security-bounty bucket (1%).** Pays validated security reports and bug rewards under published terms and a coin severity schedule fixed in advance, up to 3M; the rest is burned at genesis. Testnet tokens have no value and earn nothing on mainnet by themselves: testnet validators and miners earn from mainnet epoch 0 under the same rules as everyone else.
3. **Necessary fees (0.5%).** Security audits (CertiK/Hacken), the legal opinion, the legal entities, on-chain deployment gas and project infrastructure. **Plain disclosure: this is the one slice the project itself may sell.** Auditors, lawyers and registries bill in dollars, and the project has no other money to pay them, so the project sells coins from this slice, and only this slice, to pay those bills. Each sale pays one published bill of an outside party, is recorded on chain before it happens, stays under a cap per week set by a governance vote, and is made at the market price in a public pool that is deep enough, which cannot exist before the stage-2 pool is built (see "Launch liquidity" below), so in stage 1 nothing is sold and these bills are paid from grants and equity; there is no fixed price, no discount, no promise of any return, and no marketing. The project has not yet received a lawyer's opinion on these sales in the United States or the European Union; it has asked for one first. The rules bind the signers of this slice by published policy, not by code, so a breach would be visible on chain but not blocked. These sales add coins to the market that would otherwise stay locked or be burned (at most 0.5% of the total supply over the life of the slice). Nothing else is sold by the project at launch.

There is no exchange-listing batch: a later CEX listing is funded from the treasury stream by a governance vote. The team, treasury and growth budgets get **no big bag at launch** — see next.

**In plain language — what "streamed from the curve (vesting)" means, with an example.** *Vesting* = coins unlock a little at a time on a fixed schedule, not all at once. *Streamed from the curve* = the team/treasury/growth share is minted **gradually over years (like a salary drip)**, never pre-printed into a wallet that could be dumped on you.

> **Example.** The team share is 8% (80,000,000). Instead of getting 80M on launch day, it **vests linearly over 347 weekly epochs (about 80 months) from launch, with no cliff** — about **1M per month**. So insiders **cannot dump a giant bag at listing** — their payout is tied to building the project for years. The mining reserve works the same way: ~80% is released to miners **slowly, each year less than the year before (10% less by default)**, not minted up front.

**As emission shrinks — does the ecosystem keep going? Yes.** The declining emission is a **bootstrap subsidy, not the long-term engine.** Miner income stands on two legs: (1) **delivery miners are paid by real usage fees from day one** — every download pays a bandwidth fee, which has nothing to do with emission and lasts as long as people use the network; (2) **storage miners** keeping the durability floor are paid by floor minting within the curve; **whenever that falls short (a price drop, or the shrinking curve), the winter reserve tops it up by rule, only up to the reserve's balance — funded by fees, treasury yield, orphan-file shares and issuance set aside in good years, not by printing new tokens. This is a cost-compensation rule, not a guaranteed income for any miner.** As real demand grows, fee revenue replaces the shrinking emission; as emission shrinks the network runs on **download fees, Private-storage rental, compute usage and `.web3os` domain fees**. **BME** keeps it non-inflationary: above the durability floor, minting needs matching burns, and burned tokens never reopen minting capacity under the fixed 1B cap. This is the same "block-subsidy → transaction-fees" handoff mature networks use. **Honest caveat:** this only holds if real usage actually grows by then — if demand never shows up, fees won't replace the subsidy and miners leave. That adoption risk is the project's core bet (see §7). If both reserve legs run dry, the miner floor is only a published target: the protocol never prints above the curve to pay it, and it protects existing files by pausing new Public admissions and evicting extra cache copies first (§15.1).

### Who actually earns money (in plain words)

Every time someone pays to download a file, that **single payment is split four ways** — like a music-streaming payout, but on-chain and automatic:

1. **The creator (copyright owner)** gets the largest share — whatever is left after the others.
2. **The "delivery" host** who actually sent you the bytes gets a **bandwidth fee** — paid per download, like a courier paid per delivery.
3. **A small platform fund (the "treasury")** takes a fixed cut — this pays for **ongoing development, the search index, and ecosystem grants.**
4. **A small slice (about 4%) is burned** — removed from supply for good. This is what stops anyone from earning rewards by downloading their own files: a self-buyer loses money, about 7% of the price at the default settings.

Separately, the **"storage" hosts** — the people who keep your file safe and online even when nobody is downloading it — are paid by the network's **floor minting** for every file until the idle reclaim removes it, popular or not. That is **not** taken out of your download fee.

**So where do the developers/operators get paid?** Two ways — and *not* by secretly skimming your downloads:

- A **dedicated team budget (8% of all tokens)** that unlocks slowly, month by month, over 80 months (the vesting drip described above) — so the team is paid to **keep building**, not to dump tokens.
- The **platform-fund cut (#3 above):** because the treasury takes a small slice of *every* download fee, development keeps being funded by **real usage** — even long after the initial team budget is gone.

**What is "POL" (protocol-owned liquidity)?** To buy or sell Web3OS, there has to be an **"exchange pool"** holding coins on both sides. Most projects *rent* this pool from outsiders who can **yank it out at any moment** — and when they do, the price collapses and you can't sell (a "rug pull"). Web3OS instead **owns and locks** its own pool: the vault has **no withdrawal key**, and the signers' Safe can remove liquidity only after the time lock and only to the chain treasury escrow or the winter-reserve account, so once the pool is funded there is always somewhere to buy and sell, and the trading fees stay in the pool. A slice of the launch batch (the **"POL"** portion) is set aside as **protocol-owned trading liquidity**. At mainnet launch the vault does not sell Web3OS (the project's only sales are from the small necessary-fees slice described above, to pay its bills), and there is no pool at all: the coin cannot be bought, and coins paid by the network cannot be sent to anyone. The pool is built, and the vault adds half of the platform-fund cut to it each week, only if a governance vote, held after legal opinions for the US and the EU, turns that on.

**Launch liquidity: use first, trade later (ADR-246).** Mainnet opens in two stages.
- **Stage 1, no pool.** Everything the network pays you (mining, storage, hosting, message relay, creator shares, staking yield) is a utility coin: you can pay fees and gas, buy storage and downloads, post stake and collateral and stake for votes with it, but you **cannot send it to another account** or bridge it out, not even to a second account of your own. Nobody can buy the coin in this stage.
- **Stage 2, the project builds liquidity.** After written legal opinions for the US and the EU and a governance vote, the liquidity batch above is placed in one pool, and the official site and the wallet link to that pool. This is building liquidity, not a sale round: there is no fixed price, no buyers' list, no allocation and no deadline, and the USDC that buyers pay stays in the pool.
- **Then your coins unlock step by step.** Once buyers have paid enough USDC into the pool for it to pass the network's depth test (about USD 250,000 of USDC at the default setting), the lock starts to lift: one 26th of your earned coins each week, about six months in all. A week in which the pool is below the test unlocks nothing, and what was already unlocked stays unlocked. Coins you earned before the start and coins you earn during these months follow the same weekly steps, so nothing unlocks all at once.
- ⚠️ **No date is promised, and it may never happen.** If the opinions say no, the vote fails, or buyers do not come, earned coins stay use-only. The opening price is a voted number no market has tested, the pool gives no support below it, and the holders who vote on these settings are the same people whose coins are locked. If you stake earned coins and later buy coins, the bought ones are held until the schedule releases them or your stake is back. Do not mine expecting to sell on a known day.

> **Not investment advice.** Token prices are highly volatile and may go to zero. Assess for yourself and follow your local laws before participating.

---

## 4. Per-role manual

### Role 1 — Just browsing / searching (free, account needed)
- **Can do:** free browse/search/preview and see AI scores. (Full content/download needs token.)
- **Rules:** get an account first (searching uses network resources): create one on your device or connect a wallet you already have; free, pseudonymous (no ID; your account is public, and every paid read is recorded under it).
- **Penalties:** virtually none; the only case is **frantic query-spamming** gets the account temporarily rate-limited (a daily free quota per kind: 200 searches, 500 browses, 10 previews, ten times that when staked; then growing delays). Normal use is unaffected.

### Role 2 — Buyer / downloader
- **Can do:** download Public content with token, move purchases into your private vault (Private), prepay your own storage for a period you choose (renew before it ends, or the files are dropped after a short grace window) *(planned)*.
- **Rules:** **virus/degraded-variant/not-as-described/fake-HD/missing-parts** → refund claim **while the purchase is open** (claims gather for one week from the first claim), which counts toward a threshold (default 5% of the file's qualifying downloads and at least 20 buyers) before a jury decides; "previewed it and changed my mind" is **not** refundable; claims require a **small deposit** to deter abuse.
- **Outcomes:** valid claim → ✅ no penalty, refunded first; malicious/freeloading claim → 💰 deposit slashed ＋ 📉 reputation cut; repeat abuse → reputation drops, claim rights restricted.

### Role 3 — Uploader / creator (earn by uploading)
- **Can do:** upload media/docs/software, earn royalties on downloads, register as copyright holder; if someone else published your work, file a claim with your proof from its page ("This is my work") — a human jury decides contested cases, and if you win you choose to keep it up and collect, or take it down *(planned)*.
- **AI helps you:** auto classification/preview, plus subtitles and live on-device translation *(planned)*; only deterministic checks block a file, never an AI guess → if you're honest you're rarely mis-accused.
- **Key rules:** uploads land in your private vault; **publishing is one switch, off by default, and can't be undone**; publishing is free within the allowance (beyond it, a deposit; a choice of a small refundable bond or a device puzzle is *(planned)*); a published file nobody else downloads in full for a year, scored low or never scored, is removed for good after a 7-day notice; before then anyone can renew it by paying about a year of its storage cost; **until you register as the copyright holder, you get 1% of your file's earnings once your publication is opened and 99% waits in escrow** (26 weeks without a dispute, so the real owner's money cannot be taken by someone who only uploaded the work; the registered holder or a winning claimant then receives it weekly, and an escrow nobody claims goes to the public digital asset maintenance fund, never to the uploader); **payouts stop while an ownership claim or a report freeze is open**, and an upheld buyer refund case is paid from the escrowed share first; **no malware, no impersonating originals by re-format/re-cut, no not-as-described** (fake HD, fake full version, missing DLC).
- **Outcomes:** honest original/legal → ✅ normal royalties + AI value-add; low-value/borderline (first, minor) → ⚠️ warning; repeat → 📉 reputation cut; **impersonation/not-as-described** → 🚫 takedown + buyer refund + slash that file's reward + reputation cut (money flows to the true original creator); **bundled malware** → 💰 forfeit that file's reward and any publishing bond + 🚫 takedown + a strike + heavy reputation cut; **serious illegal** (weapons/explosives/bio) → the same + heavy penalty; **three strikes within a year** → publishing ends for good (ADR-205); **CSAM & zero-tolerance** → ⛔ instant ban + max slash + **permanent ban** (no "first warning").
- **Tip:** changing format/filename to dodge dedup is useless — AI looks at the **content itself**.

### Role 3b — Sponsor (pay so that everyone gets a work free) *(planned)*
- **Can do:** a publisher, or one advertiser the publisher names, locks coins on a Public work as a **promotion stake**. While the stake can pay, any account with a small balance and no strike takes the full work free, once a week; the stake pays the delivery and the network fee of every free copy.
- **What you lock, and for how long:** you choose the amount, a weekly budget and a **lock term** (between a network-set minimum and maximum). **Before the term ends you cannot take any of it back.** A top-up can make the term longer, never shorter.
- **The locked coins are spent:** every free copy reduces the stake. The weekly budget is your worst case per week, and accounts that are not real viewers can take all of it.
- **Yield (floating, not promised):** a few weeks of budget stay ready to pay copies and earn nothing. The rest is staked with the validator you pick and earns the network's ordinary staking yield, less that validator's commission; the yield is added to the promotion. **The yield changes every week, can be zero, and nobody promises or guarantees it.** There is no fixed rate. A small stake may have nothing staked at all.
- **Risk of loss:** if your validator is penalised by the network (slashing), part of the staked coins is destroyed. That loss is yours; nobody refunds it. An offline or jailed validator earns you nothing.
- **Who holds the coins:** the network's own rules, in an account no person or company has a key to. The project does not hold, lend or re-stake them and takes no share of the yield. The stake gives **no vote**.
- **What comes back:** after the term you may end the promotion and take back what is left. Staked coins return after the network's unstaking wait (about three weeks) and earn nothing while they wait. Before the term, coins come back only if the work itself leaves (reclaimed, banned, or moved to another holder by an ownership ruling) or as the small remainder below the cost of one copy.
- **Delisting:** when you withdraw, or when the stake can no longer pay for one more copy, **the work is no longer offered to new readers, free or paid**. It is listed again when it is funded again, or sold again after the publisher returns it to sale or the withdrawal has been paid out. A publisher who names an advertiser cannot end the promotion while that advertiser's stake can still pay for a copy. People who already own it keep it.
- **Advertising:** a work that contains paid placement must say so, naming who paid; the label shows before the first byte.

### Role 4 — Miner (provide disk, earn tokens)
- **Can do:** store files for the network on your disk and deliver reliably on download → earn tokens; storage collateral earns no staking yield (yield goes only to stake bonded to a validator).
- **At mainnet launch your rewards are utility-only:** you can use them on the network (fees, storage, stake, collateral, votes) but cannot send or sell them until the project's liquidity pool is built and deep enough; after that they unlock in weekly steps over about six months, pausing whenever the pool is too shallow. No date is promised (section 3, "Launch liquidity").
- **Rules:** you **must actually store and be able to deliver**; each round a public random draw picks pieces of the copies you hold, and you must prove on chain, within a short window, that you still have them (live on testnet, parameters under calibration).
- **Outcomes:** reliable → ✅ mining rewards; occasional dropout → ⚠️ lower score, less reward; missed or failed proof → 💰 the pay since your last proven round is forfeited and all your floor columns stop counting until you prove a later round; a missed or false proof slashes no stake, which is cut only by an adjudicated case outcome.

### Role 4b — Compute / hosting customer and provider *(planned)*
- **Customer:** rent GPU jobs or run your own containers on community machines; you fund an escrow up front, it is drawn per period, and what is not drawn comes back when you close. Keep your program's secrets in a small, capped **lease wallet**, so a leak costs at most the cap.
- **Provider:** offer your machine's containers or GPU, win leases by bidding, and earn from the escrow; you post a stake that is burned only for proven resource fraud, and repeated outages end the lease and lower your reputation.

### Role 5 — Staker / voter (governance)
- **Can do:** delegate stake to a validator to **vote** on rules, fees, and treasury use (above ~$100 equivalent); that stake also earns the staking yield. **Yield (floating, governance-set range) goes only to stake bonded to a validator**; juror, storage and hosting collateral earn their role pay.
- **How capital is bounded:** voting requires staking to a threshold (~$100 equiv., adjusts with price); **vote weight = stake × an age multiplier, capped per account** (stake counts linearly, so splitting across accounts never adds weight beyond the stake's own); **per-account vote cap**, so a single account cannot meet a vote's turnout bar alone, except in a small pool or right after a large drop in total stake; **the dev team caps at 20% combined, stepping to 10% and then 5% as on-chain handover conditions are met**, and **cannot use that weight to change the most core rules**.
- **Outcomes:** normal stake/vote → ✅ voting weight + decision-making (yield only on stake bonded to a validator); proposal spam → 💰 proposal deposit slashed; sock-puppet vote farming → 💰 slash + 📉 reputation cut (farming accounts is slow and expensive — not worth it).

### Role 6 — Juror / reporter (disputes)
- **Can do:** be **randomly drawn** as a juror to decide what AI can't (e.g., is this an impersonation); or **report** bad files. Correct rulings earn rewards; valid reports raise reputation.
- **Rules:** ruling **with the majority** earns; bad/outlier rulings are penalized; reports require a deposit, and **false reports forfeit it**.
- **Outcomes:** diligent & aligned → ✅ reward + reputation up; bad/outlier/committed but not revealed → 💰 juror deposit slashed + 📉 reputation cut (declining a seat by not committing costs nothing); valid report → 📈 reputation up; malicious report → 💰 report deposit slashed + 📉 reputation cut.

### Role 7 — App developer (people and AI coding assistants)
- **Can do:** build an application as a folder of static web files plus a manifest that declares its services, the scopes it asks for and the author's share of sales; publish both to the network and point a registered name at the manifest. The user's own node resolves the name, checks the user's grant and runs the front end in a sandboxed frame with no network access; every call goes through the node, which decides. One dependency-free SDK file (Apache 2.0) covers sign-in, content and streams, payments, subscriptions, compute jobs, metered calls, goods and messaging; the guide's examples come from the reference applications.
- **Rules:** an app's spending power is a capped allowance the user sets at the point of action, and larger purchases are confirmed again, so a scam or compromised app loses at most that allowance; the author share is capped by a governance parameter; apps run no code outside the sandbox and add nothing to consensus.
- **Outcomes:** sales, subscriptions and in-app purchases pay the author share automatically; a refused call returns a documented code the app handles.
- **For AI coding assistants:** the [developer guide](https://web3os.space/developers/guide) and the generated [call, scope and refusal reference](https://web3os.space/developers/reference) are the whole contract, in plain text; [llms.txt](https://web3os.space/llms.txt) is the entry point. Application logic is tested without a browser under Node's built-in test runner.
- **Status:** the guide and the reference are public. The developer kit (the SDK, a sample application and a local test node) is published once the remaining application interfaces land. Developer contact: contact@web3os.space.

---

## 5. Penalties & "behavior → consequence"

| Penalty | Plain meaning | Impact |
| :-- | :-- | :-- |
| ⚠️ Warning | A reminder, **nothing deducted** | Chance to fix; only repeats get real penalties |
| 📉 Reputation cut | Your "credit score" drops | Smaller vote weight, slower payouts, restricted features if severe |
| 💰 Slash bond/reward | Your posted bond or deposit, or your earned reward, is taken | Real money loss |
| 🚫 Takedown + refund | File removed network-wide, buyer refunded | Wasted upload + reputation loss |
| ⛔ Permanent ban | Account permanently expelled | Most severe; for CSAM & zero-tolerance illegal |

| Behavior | ⚠️ | 📉 | 💰 | 🚫 | ⛔ |
| :-- | :--: | :--: | :--: | :--: | :--: |
| Low-value/borderline upload (first) | ✅ | | | | |
| Same issue, repeated | | ✅ | | | |
| Impersonating the original | | ✅ | ✅ | ✅ | |
| Not as described (fake HD/missing) | | ✅ | ✅ | ✅ | |
| Bundled malware/adware | | ✅ | ✅ | ✅ | |
| Serious illegal (weapons/bio) | | ✅ | ✅ | ✅ | |
| CSAM & zero-tolerance | | | ✅(max) | ✅ | ✅ |
| Miner missing a storage proof (pay for that period forfeited) | | | ✅ | | |
| Buyer malicious refund abuse | | ✅ | ✅(deposit) | | |
| Juror bad ruling / false report | | ✅ | ✅(deposit) | | |
| Vote farming / sock-puppets | | ✅ | ✅ | | |

> **In one line:** honest work isn't penalized; mistakes get a chance to fix (warning); deliberate abuse costs reputation and deposits; serious illegality is taken down and banned. **Reputation can't be bought or transferred — cheating only hurts yourself.**

---

## 6. Registration & per-role risk

Two methods, **same account identity, same reputation/assets**, both pseudonymous (no ID; your account is public, and every paid read is recorded under it):
- **(A) Create an account on this device** (default) — the key is made on your device, a 12/24-word seed backup is offered, and a passkey unlocks the app on that device only (it is not a backup).
- **(B) Connect a wallet you already have** — one signature lets the app hold a short-lived session key (at most one epoch, ended by rotating your key) that signs free reads; payments always go through a confirmation you approve.

There is no social login and no key splitting (MPC). Recovery is only through **on-chain guardians** you choose, who can rotate your key but never spend *(planned)*.

| Role | Suggested | Risk |
| :-- | :-- | :-- |
| Browse/search | Either method | Skipping the seed backup = a lost device loses the account |
| Buyer | Either method; keep the seed backup offline | Lost seed and device = lost purchases |
| Uploader | Either method; **back up the seed before you earn** | Lost key = lost income |
| Miner | **Hardware wallet, or a device account with an offline seed backup** | Lost access = lost stake + income |
| Staker/voter | **Hardware wallet** | Lost access = lost stake |

**Rule of thumb:** **back up your seed offline; nobody, including Web3OS, can recover a lost key.** **KYC is a separate matter**: never required for an account; the only identity check is the registrar-verified copyright-party registration, and a future optional zero-knowledge personhood proof may carry only a capped bonus, with **no document disclosure**.

---

## 7. Compliance & risk disclosure (honest)

**Legal posture:** Web3OS is **content-neutral decentralized infrastructure**, like IPFS/BitTorrent; its economic layer **deliberately favors rightsholders** (opt-in attestation payouts, an upload of another person's work earns its uploader at most the 1% weekly promotion at the genesis setting), paired with tiered takedown governance and a personal-data removal path. It **does not advocate, design, or encourage** circumventing DRM or unauthorized distribution. Per-jurisdiction applicability is subject to **qualified legal counsel**; operators choose parameters and policy per their jurisdiction.

**KYC / privacy:** Web3OS **never collects or stores any identity documents** and does not run its own KYC; where compliance is needed (copyright-party registration), an accountable registrar checks the applicant's credential off chain and the chain records only the registration and a nullifier, never the document. Wallet↔real-identity binding data **never go on-chain and are never stored in plaintext by nodes**.

**License:** the protocol core is **BSL 1.1** (the source is not public yet: it is disclosed under BSL for audit once governance decides the launch is solid; restricted from commercial competition; each version's Change Date, when it converts to full open source, is no later than four years after release, the maximum BSL 1.1 allows), with an **emergency dead-man switch** (if `bslDeadManEpochs` pass without an executed governance proposal, the code converts early so the community can fully take over; no multisig holds this switch). This public repo is Apache-2.0 minimal material.

**Honest residual risks (cannot be fully eliminated; disclosed):**
- Private files are **encrypted, but not zero-knowledge secret**: the key is derived from the file, so anyone holding the same file (or guessing a short, predictable one) can confirm that a copy is stored on the network; no owner, uploader or file list is ever revealed, because Private content is never announced and nothing on chain links it to an account. **For true secrecy, encrypt a sensitive file yourself before uploading it, for example as a password-protected 7z or zip archive with AES-256 and a long random password; Web3OS cannot recover a lost password. Such a file stays Private: it can never be published or sold, because a buyer would have no password.**
- On an anonymous network, **metadata size/frequency fingerprints** may enable de-anonymization by advanced analysis; sophisticated heavy re-edits may evade fingerprints and human review.
- Key (seed) **loss is unrecoverable** unless on-chain guardians *(planned)* rotate it; your Private data key is backed up under your wallet, so the same wallet on a new device recovers your Private files.
- Auto-update vs decentralization is inherently tense: updates use reproducible builds ＋ signatures ＋ on-chain pinned hashes ＋ verify-before-run, and **never silently push** code.

**Investment risk:** this document is **not investment advice**. Web3OS is a utility token; price can be highly volatile or go to zero; testnet parameters may change. DYOR, follow local laws, and never invest more than you can afford to lose.

**Platform & regulatory posture:** The app runs on **Windows, Linux, Android and TV**. Native clients are **Desktop (Windows/Linux)** — full features (mining, sync, creation) — and **Android** (consumer client, phones and TV). **macOS and iOS are untested because the project has no Apple hardware: Mac and iPhone testers are wanted** (one test kit, one command, one result file; no node needed). **iOS is a limited web/PWA app, not on the App Store** in v1 (the consumer side plus Private upload and download, with no background sync and no native wallet), which avoids Apple's rule against using crypto to unlock content (Guideline 3.1.1) and its exchange-licensing rule (3.1.5). Android ships two ways: a **side-loadable full APK** (self-distributed, self-updating) as the canonical client, plus an optional **Play 'lite' build**; the wallet is **non-custodial** (exempt from Google Play crypto-wallet licensing) and buying and selling open the official Uniswap interface, an **external DEX** (we do not operate an exchange). Web3OS is designed as a **utility token**: it pays for and is earned by network services, and it is **not offered as an investment**. Its legal classification in any country has not been confirmed by a regulator or by counsel. Listing starts with **permissionless DEXs**; any **centralized-exchange** listing is a later step requiring a legal opinion, contract audits and a disclosed market maker. EU (MiCA) and per-country obligations are subject to qualified local counsel.

---

## 8. Miner onboarding guide (testnet stage)

> **Now in testnet — install bundles and signing are still being released**; the following is the **intended flow**, with official download links announced in the public repo later. Testnet tokens have no value.

**Get the install bundle (after release):**
1. Download the official release for your OS (Linux or Windows; no macOS release until Mac testers have run the test kit) from the **GitHub Releases** page of the public site repo `Web3OS-space/web3os` (binaries only; the link is on the site's testers page).
2. **Verify authenticity (important):** a testnet kit must match the `SHA256SUMS` file published with its release; a mainnet bundle's **hash** must match the **on-chain pinned release hash** with a valid **governance signature**, and once the source is disclosed, advanced users can recompute the hash via **reproducible build**. **Any "Web3OS install bundle" not verified this way is to be treated as counterfeit.**

**Set up the node (conceptual):**
- Pick a **storage root** (more space, more uptime → better rewards) and a **bandwidth cap**.
- Check your **upload** speed, not only download: deliveries go to holders that answer quickly, and a request that a slow holder does not answer in time moves to the next holder of the same chunk, which earns the delivery. The paid floor role needs an SSD.
- Join the network via **public seed nodes** (config ships with the bundle).
- Set a **miner wallet** (seed/hardware wallet, back up offline) to receive mining rewards.
- Desktop runs as a **background daemon**: closing the window keeps serving blocks and earning.

**Rewards & duties:** reliable store + delivery → mining rewards; a public random draw picks pieces you must prove on chain (live on testnet, parameters under calibration), and **a missed proof forfeits the pay since your last proven round** (see §4 Role 4).

> Desktop (Windows/Linux) is the full node (mining/sync/creation). Android is a consumer client on phones and TV (side-load full APK + optional Play lite). macOS and iOS are untested (no Apple hardware; testers wanted); iOS is a limited PWA, not on the App Store (v1).

### Compared with other disk-mining networks

If you farm Chia or run Filecoin, Storj or Sia, you already have most of what Web3OS needs: spare disk, an always-on machine and a stable connection. The paid floor role reads its disk at random about 270 times per second for every TB it holds, so that part needs an SSD; hard disks serve cache copies. On Web3OS that disk holds real files that people pay to store and download, not placeholder data.

Legend: ✅ strength · ⚠️ trade-off or partial · ❌ weakness · ➖ not offered or not applicable.

| | **Web3OS** | Chia | Filecoin | Storj | Sia | Arweave |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| What your disk holds | ✅ Real user files, as encrypted chunks | ❌ Plots (cryptographic filler, no user data) | ⚠️ Client data or committed-capacity sectors | ✅ Real user files, as encrypted pieces | ✅ Real renter files | ✅ Replicas of the permanent weave |
| Setup before earning | ✅ None for normal data: no plotting, no sealing (a light sequential seal only on durability-floor columns, live on testnet) | ⚠️ Plotting (CPU/GPU, temp space) | ❌ Heavy sealing (GPUs, large RAM, fast NVMe) | ⚠️ Vetting period | ⚠️ Host setup, collateral | ⚠️ Packing the data you mine |
| Hardware | ✅ SSD for the paid floor, any disk for cache copies; stable connection; no GPU | ⚠️ Disks; plotting rig | ❌ Server-class sealing rig | ✅ Disk + connection | ✅ Disk + connection | ⚠️ Fast disks |
| How you prove storage | ⚠️ A public random draw picks chunks you hold, proven on chain within a short window (live on testnet), plus delivery speed | ✅ Proof of Space and Time | ✅ PoRep + PoSt (heavy, formal) | ⚠️ Audits by satellites (operator-run) | ✅ Storage proofs per contract | ✅ Proofs of random access |
| How you earn | ✅ Storage pay + a fee for every download you deliver (real usage, not only new coins) | ⚠️ Block-win lottery (pools smooth it) | ✅ Block rewards + deal fees | ✅ Per TB stored + egress | ✅ Contract payments | ⚠️ Block rewards |
| Stake / collateral | ✅ A stake, cut only by an adjudicated case outcome (a missed or false storage proof forfeits pay, no slash) | ✅ None | ⚠️ FIL pledge, penalties for faults | ⚠️ None (part of early payouts withheld) | ⚠️ Collateral per contract | ✅ None |
| Also rent out compute? | ✅ Yes, on Linux: container hosting (Web3OS hosting can also place deployments on Akash) | ➖ No | ➖ No | ➖ No | ➖ No | ➖ No |
| Maturity | ❌ **Testnet, pre-launch** | ✅ Mainnet | ✅ Mainnet | ✅ Mainnet | ✅ Mainnet | ✅ Mainnet |

The other columns reflect each network's general design; check their own docs for current details. The full comparison, with Web3OS's honest drawbacks, is in §10.

### Join the public testnet

- **Who:** anyone who will keep one node online for a few weeks, report bugs and say where things were confusing.
- **How to join:** send a private message on Telegram to [@Web3OS_AI_bot](https://t.me/Web3OS_AI_bot) starting with "Miner"; we reply privately (no Telegram account: contact@web3os.space). Questions go to the [Telegram group](https://t.me/Web3OS_Official).
- **Requirements:**
  - Linux (Ubuntu) is best: it runs storage and can also rent out compute. Windows runs storage only for now.
  - Assign as much spare disk as you like. Web3OS uses only that space and never touches your plots or other data.
  - A stable connection; home is fine. Your node address is never published.
- **What you get:**
  - Early access and a direct line to the team.
  - Testnet tokens from the faucet (no value), to try uploads, downloads and hosting.
  - Bug reports and successful testnet attacks are recorded and rewarded after mainnet by a community vote (see section 11); security problems are reported privately as described there.
  - No airdrop and no allocation for testnet participants: mainnet earnings follow the normal mining and staking rules.
  - No payment during the testnet. Web3OS has no reference or target price and nothing here is an offer to sell. Test data is deleted at every testnet reset.
- **How:**
  - The install bundle is being finished.
  - Sign up by Telegram private message as above, with your OS, the disk you can spare and your upload speed. No other personal data is needed to join.
  - The install steps and an invite follow when the bundle is released.

### Try to break the rules (testnet)

**It's testnet — tokens have no value — so this is the time to hit it hard.** We invite miners and users to **find bugs and try to cheat the rules** inside the app and the chain, never against a computer you do not own, especially around **deposits/withdrawals/settlement (ramps)**:
- **Test tokens:** once per account, at the fund step after your seed backup, the testnet faucet sends test tokens on chain (no value); the app shows the amount granted or the wait. *(The faucet does not exist on mainnet.)*
- **Fair game:** over/abnormal withdrawals, fake-download reward farming, miners faking storage, sock-puppet farming, refund-gaming, oracle price manipulation, ramp-spread arbitrage, **filing false reports on fake *or real* files, spamming governance proposals/votes or raising genuinely contested votes** — deliberately triggering the **deterministic-detector ＋ human-jury / governance-vote flow** to see if it can be fooled or flooded. **The harder, the better.**
- **The deterrents are part of the test:** false reports and spam proposals **forfeit their deposit ＋ cut reputation** by design — testnet proves whether that actually holds (if it doesn't, that's a bug — report it).
- **Governance really can change the rules (explicit disclosure):** fees, revenue splits, thresholds and parameters are **decided by community vote** — **no one (including the team) can change them unilaterally**. **On testnet you're welcome to launch genuine *or* malicious proposals/votes** and try to break the governance defenses: vote weight = **stake × age multiplier** (linear in stake), **per-identity vote cap**, **team aggregate cap (20% → 10% → 5% at handover gates, excluded from core-clause votes)**, **immutable core clauses (supermajority + timelock)**, proposal deposits. **Can money / sock-puppets / vote-flooding buy governance? Show us.**
- **Report** bugs, problems and every way you found to cheat as a [GitHub issue](https://github.com/Web3OS-space/web3os/issues/new?template=bug_report.yml), which enters the bug ledger of section 11, (what happened, the steps, and where: Windows, Linux, Android or TV); security problems privately as in section 11.
- **Why it helps you too:** WARNING-and-above events (especially ramps) are summarized into a **CSV** for AI/team analysis and parameter calibration. **The harder you hit it, the safer launch is.**
- **Rules:** attack within testnet only; **no real PII, no real-world harm outside testnet** (that's illegal and out of scope).

---

## 9. For investors (read the risks first)

> **This section is not investment advice and not an offer.** Web3OS is a **utility token** (payments/staking/mining/governance), **not a security**. **It is testnet now — testnet tokens have no value (test swaps use test USDC only) and do not represent mainnet terms.** Digital assets can be highly volatile or go to zero. DYOR, follow local laws, never invest more than you can afford to lose.

To follow the project, the [X account](https://x.com/Web3OS_space) carries the news; discussion happens in the [Telegram group](https://t.me/Web3OS_Official). There is no presale and no private token sale; nothing on this site is an offer to sell coins or shares.

### 9.1 How to buy (intended path after mainnet)
- On testnet, swaps *(planned)* use **test USDC only** and the tokens have no value; at mainnet launch (stage 1) the coin **cannot be bought anywhere**, and anyone offering it then is not selling the real thing. In stage 2, after the legal opinions and the vote, the project builds one liquidity pool for **wrapped WEB3OS** on **Uniswap** (Ethereum), which the official site and the wallet link to, with deposits and withdrawals to Web3OSChain through the app. That pool opens with Web3OS only: the price rises along the pool's curve as people buy, the first buyers get the lowest prices (bots included), and below the opening price the pool pays sellers only out of what buyers paid in.
- Intended flow: get a **self-custody Ethereum wallet** → hold a little ETH for gas and USDC → swap for Web3OS at the **correct mainnet token contract address** on a DEX.
- ⚠️ **The mainnet wrapped-Web3OS contract address will be announced via the official public repo and multiple channels; the testnet token on Web3OSChain testnet and its Ethereum Sepolia test pool are for testing only — never treat them as buyable assets.** Any "WEB3OS" token of unknown origin is counterfeit/scam.

### 9.2 DEX trading advice
- **Use a self-custody wallet** (seed/hardware); don't keep long-term holdings on exchanges.
- **Verify the contract address:** trust only the officially announced one — same-name fake tokens are rampant on DEXs.
- **Mind slippage/liquidity:** large orders into small pools slip hard → split orders, set sane slippage.
- **Anti-scam:** don't click unknown airdrops/links, don't approve suspicious contracts; the team never DMs you to "send tokens first".
- **Gas:** Ethereum transactions need a little ETH; withdrawing from Web3OSChain needs none, because the bridge charges the Ethereum gas in Web3OS.

### 9.3 Risk of funding via a KYC wallet/exchange
- Withdrawing from a **KYC'd centralized exchange** to chain links **your real identity ↔ your on-chain address and subsequent activity** (**de-anonymization**); the exchange may also **freeze withdrawals**.
- For privacy: use a **DEX + self-custody wallet**; use a **separate, non-KYC address** for sensitive use.
- Web3OS itself **never collects identity documents**; but your **funding source** (a KYC exchange) is your own de-anonymization risk point, unrelated to the protocol.

### 9.4 FDV vs circulating market cap (don't be fooled by FDV)
- **FDV (fully-diluted valuation) = total supply × market price** (1B × whatever the market pays); Web3OS has no reference or target price.
- **But FDV is not market cap:** 80% is the mining reserve **locked and released on a declining curve (10% less each year by default)**, and non-mining buckets also vest → **early circulating is only ~10–20%**, so **circulating market cap is far below FDV**.
- Judge a project by **circulating supply / circulating market cap + unlock schedule**; **high FDV + low float = ongoing future sell pressure** — make sure you understand this.

### 9.5 Emission simulation curve (illustrative only; subject to governance & BME; not a promise)
The 800M mining reserve uses a **rigid declining** release: each year's release is below the last and it never ends. The default cut is 10% a year; at each year end the chain suggests a cut between 0% and 20% from the past year's price (a falling price means a bigger cut) and the community confirms it by vote, or the previous cut stays. The table assumes the default 10%. **Illustrative upper bound** (actual can be lower: above the durability floor, BME mints only against burns):

| Year | Annual emission (≈) | Cumulative mining (≈) | % of total |
| :-- | --: | --: | --: |
| 1 | ~80M | ~80M | ~8% |
| 2 | ~72M | ~152M | ~15% |
| 3 | ~65M | ~217M | ~22% |
| 5 | ~52M | ~328M | ~33% |
| 10 | ~31M | ~521M | ~52% |
| 20 | ~11M | ~702M | ~70% |
| 30 | ~4M | ~766M | ~77% |

- Non-mining is **not a genesis bag**: a **4% genesis premint** covers the protocol-owned liquidity seed, the security-bounty bucket and fees (each sub-bucket an on-chain group policy + timelock + labeled; unused returns to treasury/burn; POL: vault has no withdrawal key and the signers' Safe can remove liquidity only after the time lock and only to the chain treasury escrow or the winter-reserve account); team/treasury/growth are **streamed gradually from the curve** (vesting + governance control + timelock; the treasury is keyless; the fiat leg that backs the miner floor is held of record by the issuing company, and a segregated holding vehicle is with counsel).
- **BME:** above the durability floor, no verified demand → no minting; adaptation can only reduce, never over-issue → the table is an **upper bound**, real circulating can be lower.
- **Exact schedule/parameters are governed on-chain.**

> Reminder: **not investment advice. Everything may change in the testnet stage.**

---

## 10. How Web3OS compares — honest pros & cons

Web3OS is **not "another Filecoin."** Most decentralized networks do *one* thing — store blobs (Filecoin / Arweave / Storj / Sia), move files (IPFS / BitTorrent), or rent GPUs (Akash / io.net / Render). Web3OS combines **decentralized storage ＋ AI value-search ＋ a creator marketplace (royalties, and rights holders paid even when someone else uploads their work) ＋ optional compute** — which is its differentiator *and* its biggest execution risk.

### Positioning (2026)

Legend: ✅ strength · ⚠️ trade-off or partial · ❌ weakness · ➖ not offered or not applicable.

| | **Web3OS** | Filecoin | Arweave | Storj | IPFS / BitTorrent | Akash / io.net / Render |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Core | Storage ＋ **AI value-search ＋ content market** | Storage marketplace | **Permanent** storage | S3-style object storage | Addressing / transport | GPU compute |
| Storage proof | ⚠️ **PoFD (delivery-speed) ＋ on-chain proof of random targets** (ADR-224); sealing ＋ PoSt on floor columns only (ADR-172, live on testnet, parameters under calibration) | ✅ **PoRep / PoSt** (heavy, formal) | ✅ Endowment ＋ proofs | ⚠️ Erasure ＋ reputation (Satellites) | ❌ none native | ➖ |
| Retention | ⚠️ **Demand/value-driven** (cold low-value may be GC'd) | ⚠️ Contract-term | ✅ **Pay-once, forever** | ⚠️ Contract | ❌ best-effort | ➖ |
| Confidentiality | ⚠️ **Not ZK** (dedup tradeoff; self-encrypt option) | ✅ opaque encrypted blobs | ❌ public permaweb | ✅ client-side encrypted | ❌ public | ➖ |
| Search / discovery | ✅ **AI value scoring, multilingual** | ❌ none (blob CID) | ⚠️ gateway | ❌ none | ⚠️ DHT / keyword | ➖ |
| Creator economy / rights-holder pay | ✅ **Built-in** (royalties, attestation, jury) | ❌ no | ❌ no | ❌ no | ❌ no | ⚠️ Render: creator focus |
| Compute | ⚠️ Optional container hosting, nascent | ➖ | ➖ | ➖ | ➖ | ✅ Live GPU markets |
| Maturity | ❌ **Testnet, pre-launch** | ✅ Mainnet, ~2.1 EiB stored | ✅ Mainnet, years (permaweb) | ✅ Mainnet, S3 live | ✅ Mature | ✅ Live (io.net 300K+ GPUs) |

### Advantages

| | Advantage | What it means | Compared with |
| :-- | :-- | :-- | :-- |
| ✅ | **Value-search ＋ marketplace** | Content surfaces by AI-judged value (not ads/SEO), with creator royalties and rights holders paid even when others upload their works | Storage-only networks do not do this |
| ✅ | **Lower miner barrier** | PoFD ＋ audit, no SDR sealing or zk proofs; only floor columns carry a light sequential seal | Cheaper and faster to join than Filecoin |
| ✅ | **Space efficient** | Network-wide convergent dedup ＋ erasure coding (~1.4× for large files) | Instead of N× replication |
| ✅ | **Built-in AI value-add** | Multilingual subtitles/translation, content classification, safety scanning, deterministic detectors plus human-jury arbitration (AI summaries advise, never decide) | No incumbent bundles these |
| ✅ | **Non-inflationary tokenomics (BME)** | Burn-and-mint against real usage, a release that only declines, reputation-based Sybil resistance | Lottery or pure-inflation rewards |

### Honest disadvantages

| | Disadvantage | What it means | Mitigation |
| :-- | :-- | :-- | :-- |
| ❌ | **No track record — testnet, pre-launch** | Filecoin stores exbibytes, Arweave has years of permaweb, Storj/io.net are live; **Web3OS is unproven at scale — the single biggest risk** | A public testnet now; only running at scale can remove this |
| ❌ | **Early centralization** | One team runs most seed nodes and holds the ADR-184 duty seats and a capped team vote | The team cap steps down at on-chain conditions; governance runs on-chain from genesis |
| ⚠️ | **Not permanent like Arweave** | Cold, low-value, zero-download content can be garbage-collected by design | Prepaid Private storage keeps a file for the period paid, renewable; for pay-once-forever permanence, Arweave fits better |
| ⚠️ | **Lighter storage proof than Filecoin** | PoFD is delivery-driven; only durability-floor columns carry sealing and PoSt (ADR-172, live on testnet, parameters under calibration), with no full SDR PoRep — weaker formal durability assurance. In simulated attacks on the sealed lanes, a miner that recomputes missing data on each challenge could still drop about 12 % of a lane at the pinned graph degree. This is a measured lower bound, not a proven limit, pending the ADR-119 review | Per-miner sealed floor columns, random on-chain audits and erasure-coded repair; the per-challenge work bound is calibrated from these measurements before mainnet, and a missed or false proof forfeits the pay |
| ⚠️ | **Content is not zero-knowledge confidential** | The price of network-wide dedup | Self-encrypt for true secrecy (such a file stays Private) |
| ❌ | **Broad scope = execution risk** | Storage ＋ search ＋ marketplace ＋ compute ＋ naming is far more than a focused competitor (Storj = storage, Render = rendering) | None: the combination is the core bet itself |
| ❌ | **Compute layer is nascent** | Behind live io.net / Akash / Render | Can place deployments on Akash meanwhile |
| ⚠️ | **Bridge and regulatory exposure** | Wrapped-asset dependency (audited bridge standards only, never a self-built bridge); media/marketplace adjacency | Content-neutrality ＋ BSL ＋ takedown governance; mitigated, not eliminated |

> **Bottom line:** Web3OS's bet is "**AI value-search ＋ a creator marketplace on top of decentralized storage**", which no incumbent offers as one unit — but it must still prove it runs at scale, which the incumbents have done and Web3OS has not. Judge it as an **early-stage, high-upside, high-risk** project, not a drop-in replacement for a live network.

---

## 11. Brand, license, security and contact

### Brand
The Web3OS logo is free to use when referring to Web3OS, unaltered: [transparent PNG](https://web3os.space/token/web3os-logo.png) ([1024 px](https://web3os.space/token/web3os-logo-1024.png)) and, for places that do not take transparency, [white-background PNG](https://web3os.space/token/web3os-logo-white.png) ([1024 px](https://web3os.space/token/web3os-logo-white-1024.png)). The [token profile for exchange listing review](https://web3os.space/LISTING.md) summarizes the token on one page; where it and this whitepaper differ, this whitepaper governs.

### License
This whitepaper and the website are published under the [Apache License 2.0](https://web3os.space/LICENSE). The protocol core is licensed under BSL 1.1: auditable, and each version converts to full open source no later than four years after its release.

### Bug reports and rewards
Bugs are reported as a [GitHub issue](https://github.com/Web3OS-space/web3os/issues/new?template=bug_report.yml). The first reporter of a bug whose fix ships in a tagged release is entered in a public ledger with the issue, its severity, the fixing release and the reporter's GitHub username and numeric GitHub user id; the amount follows the severity (Critical 30,000, High 10,000, Medium 2,000, Low 300 WEB3OS; at most 1,000,000 in total for reports made before mainnet). After mainnet launch the whole ledger goes to one governance proposal and the community vote decides the payout in WEB3OS, which is held under the reward lock like every network reward (usable on the network, sendable only under the same rule that unlocks all rewards, with no date promised, ADR-246); the reporter puts the GitHub username in the Web3OS profile and posts the payout address in a comment on the issue from the GitHub account with the recorded user id, and the proposal names the commit of the ledger it pays. A comment edited by anyone but its author is not a claim; for a report sent by email, name your GitHub account in the email and claim on the issue the project opens after the fix. No payment to a party on a sanctions list; payment to US recipients waits for a legal opinion. Any tax on a reward is the recipient's own matter. Recording is a commitment, payment is not: the vote can change or refuse it. Project team members, project accounts and the project's AI agents are not eligible; testnet tokens have no value and convert to nothing.

Security problems are never posted publicly: email contact@web3os.space with SECURITY on the subject line, with the steps to reproduce and the impact; they enter the same ledger. Attacking the testnet rules from your own nodes and accounts is invited (section 8, "hit it hard") and enters the ledger like any bug; never test against a computer you do not own, including other people's testnet nodes, and never flood the network. Machine-readable contact: [security.txt](https://web3os.space/.well-known/security.txt).

### Join us
Sign-up for every group is private: send a private message on Telegram to [@Web3OS_AI_bot](https://t.me/Web3OS_AI_bot) that names the group and tells us about you (no Telegram account: contact@web3os.space). Questions and discussion: the [Telegram group](https://t.me/Web3OS_Official). News: [X](https://x.com/Web3OS_space). Bugs and problems: a [GitHub issue](https://github.com/Web3OS-space/web3os/issues/new/choose).

| Group | What it is |
| :-- | :-- |
| Testnet miners | Linux or Windows node kept online for a few weeks; see §8 |
| Application developers | Applications on the platform; see Role 7 |
| Testnet attackers | Try to cheat the testnet from your own nodes and accounts (§8 "hit it hard"); every way found enters the bug ledger (§11) |
| macOS and iPhone testers | The app is untested on Apple hardware; testers wanted |
| Investors and partners | Follow X; no token sale, nothing here is an offer |

### Contact

**Official accounts (anti-scam).** The only official accounts are the Telegram group Web3OS.space ([t.me/Web3OS_Official](https://t.me/Web3OS_Official)), its bot [@Web3OS_AI_bot](https://t.me/Web3OS_AI_bot), [@Web3OS_space](https://x.com/Web3OS_space) on X (news only), the GitHub organisation [Web3OS-space](https://github.com/Web3OS-space) and mail addresses ending in @web3os.space. The project never contacts anyone first; it replies only in a conversation the other person started. It never asks for recovery words, private keys or passwords, never asks anyone to send coins and runs no presale or token sale; any account that does is not the project.
Web3OS Labs LLC provides web3os.space, the Web3OS app and this website. Postal address: Web3OS Labs LLC, 30 N Gould St Ste R, Sheridan, WY 82801, United States. Every address below reaches a person; languages: English, Chinese.

| Purpose | Address |
| :-- | :-- |
| Authorities and law enforcement (EU Digital Services Act Art. 11) | legal@web3os.space |
| Users (EU Digital Services Act Art. 12) | contact@web3os.space |
| Help with the app | support@web3os.space |
| Application developers | contact@web3os.space |
| Sign-up (miners, testers and attackers) | Private message on Telegram to [@Web3OS_AI_bot](https://t.me/Web3OS_AI_bot) (no Telegram account: contact@web3os.space) |
| Questions and discussion | [Telegram group](https://t.me/Web3OS_Official) |
| News | [X](https://x.com/Web3OS_space) |
| Security vulnerabilities (see Reporting a security problem above) | contact@web3os.space (SECURITY on the subject line) |
| Report illegal content or abuse (include the share link or content address) | abuse@web3os.space |
| Copyright notices and counter-notices | dmca@web3os.space |
| Privacy and personal data requests | privacy@web3os.space |

**Copyright notices.** Web3OS Labs LLC has designated a copyright agent under 17 U.S.C. 512(c), listed in the U.S. Copyright Office DMCA Designated Agent Directory as DMCA-1086677 (Copyright Agent, address above, dmca@web3os.space). The notice requirements, counter-notices and the Taiwan Copyright Act Chapter VI-1 procedure are on the [copyright notices page](https://web3os.space/copyright/). Repeat infringers may lose access; a knowingly false notice can make the sender liable for damages under 17 U.S.C. 512(f).

---

*Minimal-disclosure public edition. The full design/implementation/UI whitepaper, backend & consensus implementation, ops tooling, deployment scripts, datasets and models remain private. Version tracked by public-repo git history.*
