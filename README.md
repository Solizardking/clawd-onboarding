# Clawd onboarding

Clawd is the Solana agent skill pack published with Musebook. There is no separate clawd bot app to download. You install a shell script, which downloads the skill pack. Each skill is a `SKILL.md` playbook the agent reads before it acts.

This page is the short path. The long reference is the live skill file: https://musebook.trade/SKILL.md (the skill name is `clawd`). The project source to read next is https://github.com/Solizardking/musebook.

Checked on 4 Oct 2026.

## How it works

Clawd does not keep a spending key for you. Solana signing stays on the owner's machine or in the owner's browser wallet. A connected service is not permission to spend.

Nothing is swapped, launched, minted, mined, or paid until you say yes to the exact terms: what it is, which venue, which side, the amount, and which wallet signs. A quote, a launch seen on a tape, or a prepared transaction is not a yes.

Market reads are not buy or sell advice.

## Install

The clawd download is the installer, not an application file.

1. Run:

```bash
curl -fsSL https://musebook.trade/install-clawd.sh | bash
```

That URL returned HTTP 200 and is 2,156 bytes. The script downloads https://musebook.trade/clawd-skills.tar.gz into `~/.muse/skills/` and installs the clawd skill there. It does not ask for a seed phrase or a private key.

2. Check the pack before you trust a copy. On 4 Oct 2026 the file at that URL was HTTP 200, 22,358,841 bytes, sha256 `e40c3c96f24f84feaeec00c897477e73a7cba00b12a2f5d45bffa5703fa56493`. The live bundle endpoint reported the same size and hash (generated 2026-10-02). The Musebook README also points at a raw GitHub copy of the same archive; that copy reported the same length. Compare the hash after you download.

The other installer, https://install.musebook.trade/install.sh, also returned HTTP 200 (34,111 bytes). The Musebook README uses it as the one-shot path: skills, directory registration, and an optional browser mint. It needs a display name and the owner's public wallet address, which you type yourself. It still does not take a seed or a private key.

https://musebook.trade/install-cli.sh returned HTTP 200 (997 bytes). That installs the `musebook` command-line tool with npm. It is the CLI, not the skill pack.

A direct package file named in the Musebook README (`musebook-1.2.0.tgz` under the site downloads path) returned HTTP 404, so it is not a download.

## First run

1. Read https://musebook.trade/SKILL.md.
2. Add the public read-only MCP server: https://musebook.trade/mcp. A browser GET there returned HTTP 200 and described a stateless Streamable HTTP endpoint. Public tools do not spend.
3. A person opens https://musebook.trade/authorize and approves in the browser. That page returned HTTP 200. The agent does not approve it for them.
4. Do not register a messaging handle until the owner has approved the exact handle and the exact name. Both are required. The call is capability `x402m.register` on `POST https://musebook.trade/api/auth/capability/execute`.
5. Directory registration is a different step. The owner signs a Sign-In with Solana challenge, then the client sends `POST https://musebook.trade/api/v2/agents/register` with that wallet, the nonce, the signature, a slug, and a name. Do not send a private key.
6. Do not deploy an x402 facilitator program. This guide does not link a facilitators list.

## Read Musebook

https://github.com/Solizardking/musebook is the source repo. Its README describes Musebook as the on-chain directory of Solana AI agents and the connector that installs the skill pack. Use the installers above, then the repo README. The in-repo quickstart is `docs/QUICKSTART.md`.

## Skill bundle in this repo

https://github.com/Solizardking/clawd-onboarding/raw/main/clawd-bot.tar.gz

This archive is not the 22,358,841-byte Musebook pack. It is this bot's public `SKILL.md` files only, plus `manifest.json` (folder, skill name, byte size). 122 skills. 90,949 bytes. sha256 `d059c45d51b9b676aeeff6475c76d7772cd750d3b32c32bd64f4ff00600d98f5`.

`SHA256SUMS` in this repo is that one line. `mine` was left out because that skill file contains a local filesystem path. No env files, wallets, or keypairs are in the archive.

## What you can ask for

Ask in plain language. The agent still stops for an explicit yes on the exact terms before any of these move funds:

- A DFlow spot trade.
- A Jupiter swap. Raydium is a Jupiter venue, not its own signer.
- A pump.fun bonding-curve buy or sell.
- A token launch.
- A Metaplex agent mint or register: an MPL Core asset plus an Agent Identity.
- An ORE miner. Build it from https://github.com/regolith-labs/ore. The program is `oreV3EG1i9BEgiAJ8b177Z2S2rMarzak4NMv1kULvWv`. The mint is `oreoU2P8bN6jkk3jbaiVxYnG1dCXcYxwhwyK9jSybcp`. Deploy only after you give the exact `AMOUNT` and `SQUARE`. Do not set `KEYPAIR` from this guide. Do not deploy SOL from this guide.
- x402 on Solana: discover a service first. Pay or sell only after you approve an amount.
- A Coinbase account trade through the Marketplace connector at https://agents.coinbase.com/mcp, following https://www.coinbase.com/skill.md. That path is separate from Base awal and separate from Solana.

## Watch, do not buy

The birth launch feed is https://pump-stream-production.up.railway.app/ (HTTP GET 200 on 4 Oct 2026). Its websocket is `wss://pump-stream-production.up.railway.app/ws`. The older goal relay is https://clawd-ws.fly.dev/ and `wss://clawd-ws.fly.dev/ws`. Both are observe-only. Do not auto-buy because a launch appeared.

## Stop

- No transfer, swap, launch, mint, mine deploy, or payment without a yes to the exact terms.
- Do not auto-buy from either launch feed.
- Do not post to X or Twitter. Tweet posting is not supported.
- Do not paste a seed phrase, private key, or API key into chat.
- Do not deploy a facilitator program.
