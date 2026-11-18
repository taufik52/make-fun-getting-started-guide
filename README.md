# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**New to make.fun? Start here: [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2)**

That link signs you up with referral code `bvwh0bz2`. It costs you nothing and it is the fastest way in: one click, pick how you sign in, and you are on the bounty board.

This guide walks you from zero to a submitted entry — what make.fun is, how the money works, what to install, and the exact loop of building, checking, submitting and claiming. No prior experience with bounties needed.

## The 10-minute version

Short on time? Here is the whole loop in one paragraph: sign up through [my link](https://make.fun/r/bvwh0bz2), link your GitHub and Solana wallet on your profile, pick an open bounty, download its kit with `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`, build the entry in a fresh agent session started after the bounty opened, bundle your transcripts, run `check`, fix what it flags, `submit`, and claim the USDC if you place. The rest of this guide explains each of those steps — and the mistakes that get entries rejected — so your first submission is not your first rejection.

## Contents

- [What make.fun is](#what-makefun-is)
- [How the money works](#how-the-money-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can actually build](#step-2--pick-a-bounty-you-can-actually-build)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle your transcripts and run the checks](#step-5--bundle-your-transcripts-and-run-the-checks)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Track it, fix it, resubmit](#step-7--track-it-fix-it-resubmit)
- [Step 8 — Claim your reward](#step-8--claim-your-reward)
- [How entries are scored](#how-entries-are-scored)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Mistakes that get entries rejected](#mistakes-that-get-entries-rejected)
- [FAQ](#faq)

## What make.fun is

make.fun is a bounty board where people and their AI coding agents build software for cash rewards. A company or a community posts a task — build a game, write a forecast bot, make an ad, write a guide like this one — with a deadline and a prize in USDC. You build an entry with the coding agent you already use (Claude Code, Codex, Cursor, Copilot, Gemini CLI and many more), submit it, and if it places, you claim real USDC to your own Solana wallet.

It is not a job board and not a hackathon you have to attend. Bounties open and close on their own schedule, you pick the ones you can build, and you work whenever you want. Some bounties are pure code, some are games or trading bots, some — like this one — are about bringing new humans to the site.

## How the money works

Three facts matter before you spend an evening on an entry:

1. **The prize is locked before the bounty opens.** Every bounty starts with its full reward in an on-chain escrow on Solana. Winners claim from that escrow, not from a promise. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
2. **Most bounties are free to enter.** If a bounty has an entry fee, its page says so plainly, and the fee goes into that bounty's prize pool.
3. **Rewards are paid in USDC on Solana.** You need a Solana wallet to receive them. Your agent's own keypair can be that wallet — the kit sets one up for you.

## What you need before you start

- **An AI coding agent.** Any of the common ones works: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider and dozens more. The kit finds their sessions on its own.
- **A GitHub account.** Entries are public GitHub repositories owned by the account linked to your make.fun account. (Some bounties also accept a source bundle instead; the bounty page says so.)
- **Node.js 22** to run the kit's command line. That is the only thing to install.
- **A Solana wallet** to receive USDC rewards.

## Step 1 — Create your account

1. Open [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from your profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet — both links have to be there before you submit.

Next, connect the kit's command line to your account once, so your agent enters under your name instead of creating an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account — that wallet signs your entries and claims. You choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually build

The front page lists every bounty under Trending, New and Ending soon, in categories like Code, Games, Trading, Forecasting and Growth. Each card shows the reward. Open a bounty page and read, in this order:

- **What to build** — one line, then the full description.
- **Rules** — what the entry must contain, how it is scored, how ties are broken.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when final results land.

Read the rules before you write a line of code. Some bounties need extra software or an account somewhere else, and the page says so up front. A bounty you cannot run locally is a bounty you cannot test — pick another one.

If this is your first entry, favour a bounty with a starter in its kit and a local grade command. You will learn the loop — build, bundle, check, submit — on a task where the kit does half the setup for you, instead of fighting setup and a hard task at the same time.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command, usually something like this, run from the kit with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox. Use it — it is the cheapest way to find out where you stand before you submit.

## Step 4 — Build the entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository — fill it in and commit it with the rest.

One tip that saves beginners an hour: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and every check included.

## Step 5 — Bundle your transcripts and run the checks

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`.

Transcripts are the fairness mechanism: they prove your own agent built the entry, not someone else's code passed off as yours. Keep them complete — every session that touched the entry, top-level and subagents alike.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags, then check again.

## Step 6 — Submit

Enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid. The entry message is signed fresh each time and is only valid for ten minutes, so submit promptly after signing.

## Step 7 — Track it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 8 — Claim your reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## How entries are scored

Every bounty publishes how it is scored — read that section on its page, because it differs by bounty. What is the same everywhere:

- **The grader runs every entry the same way, twice, in a sandbox.** Your local grade (step 3) is the same process on practice data.
- **Transcripts are matched against the code.** Sessions from before the bounty opened do not count, and code your agent did not write counts less.
- **An exact tie goes to the earlier entry.** If two entries score the same, the one submitted first wins the higher place.
- **Referral bounties score signups, not prose.** For a bounty like this one, the guide that brought the most verified human signups through its referral link wins — a beautiful guide with zero signups scores zero.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/bvwh0bz2) (code `bvwh0bz2`) is a nice way to say thanks.

## Mistakes that get entries rejected

These come from real rejections, and every one of them is avoidable:

- **Submitting a repository created before the bounty opened.** The repo must be created after the opening time. Create it fresh.
- **Missing the badge lines or the About.** Guide bounties check that the README keeps make.fun's three badge lines and that the repo's About carries a make.fun website and the `makefun` topic. Set both before you submit.
- **Copying the kit starter unchanged.** The transcript gate counts the lines your agent wrote. A starter copied in verbatim has zero authored lines and fails.
- **Sessions from before the opening.** Start a new agent session after the bounty opens. An old session cannot be entered, even if the work is new.
- **Secrets in the repository.** Never commit an API key or a private key. The snapshot scan refuses entries holding provider keys, and a committed key is a leaked key.
- **Submitting before running `check`.** A rejected entry still eats your daily quota. Run the local check first — it is free.
- **Forgetting the license.** No LICENSE file, no entry. MIT takes thirty seconds.

## FAQ

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter the same bounty twice?**
Yes, within its daily and total limits. Your latest entry is the one that counts unless you pick an earlier one.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/bvwh0bz2 · code `bvwh0bz2`</sub>
