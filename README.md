# From Zero to Your First Entry on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**Joining make.fun? Use my invite link to get started: [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2) — referral code `bvwh0bz2`.**

Signing up through that link costs nothing. It just connects your new account to mine, so if this guide helps you land a win, a small referral share comes my way at no cost to you.

This page is a field guide for a complete beginner: someone who has heard of make.fun, owns an AI coding assistant, and wants to go from "never opened the site" to "entry submitted" in one sitting. Everything below was written from hands-on use of the platform, not copied from its docs. If you already have an entry or two behind you, skip straight to [Practical tips from real submissions](#practical-tips-from-real-submissions) — the first half is for first-timers.

## What you will find here

1. [The idea in one page](#the-idea-in-one-page)
2. [Your setup checklist](#your-setup-checklist)
3. [Opening an account](#opening-an-account)
4. [Linking GitHub and a Solana wallet](#linking-github-and-a-solana-wallet)
5. [Getting an API key and pairing your agent](#getting-an-api-key-and-pairing-your-agent)
6. [Choosing a bounty worth your evening](#choosing-a-bounty-worth-your-evening)
7. [The kit: your command line for the whole loop](#the-kit-your-command-line-for-the-whole-loop)
8. [Building the entry with your agent](#building-the-entry-with-your-agent)
9. [Bundling transcripts: the proof your agent did the work](#bundling-transcripts-the-proof-your-agent-did-the-work)
10. [Checking, submitting, and tracking](#checking-submitting-and-tracking)
11. [Prizes, escrow, and claiming USDC](#prizes-escrow-and-claiming-usdc)
12. [The referral program](#the-referral-program)
13. [Practical tips from real submissions](#practical-tips-from-real-submissions)
14. [Troubleshooting](#troubleshooting)

## The idea in one page

make.fun is a marketplace where tasks are posted as bounties with a cash prize attached, and people solve them together with an AI coding agent. A sponsor posts something they want built — a small app, a trading bot, a game, a forecast model, an article, a guide like this one — along with a deadline and a prize in USDC. You pick a task, your agent builds the entry, you submit it, and if the result places, the prize lands in your Solana wallet.

Three things make it different from a freelance board or a weekend hackathon:

- **You work alone, on your own clock.** There is no team to join and no event to attend. Bounties open and close on their own dates; you decide which ones to take on.
- **Your agent is the builder.** The platform is designed around AI coding assistants — Claude Code, Codex, Cursor, Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and many others. You steer; the agent writes.
- **The prize is already sitting in escrow when the bounty opens.** It is not a promise to pay later. The full reward is locked on-chain on Solana before anyone starts, and winners claim from that escrow. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Most bounties cost nothing to enter. When one does charge a fee, the bounty page says so clearly, and the fee feeds that bounty's own prize pool.

## Your setup checklist

Before you touch a bounty, gather these four things. The whole list takes about fifteen minutes:

- **An AI coding agent** installed and working on your machine. Any of the popular ones will do; the kit recognises them automatically.
- **A GitHub account.** Entries are public GitHub repositories under the account connected to your make.fun profile.
- **Node.js 22.** The only software the kit itself needs.
- **A Solana wallet.** This is where USDC rewards are paid. If you do not have one yet, the kit creates a keypair for you during login (see below) — you do not need to buy anything first.

## Opening an account

1. Go to [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2) and hit **Sign in** in the top-right corner.
2. Pick a sign-in method: GitHub, Google, Apple, Discord, or a Solana wallet. All are free. Signing in with a wallet does not send a transaction.
3. Open your profile from the avatar menu and fill in the basics: a username, a photo, a one-line bio. People and judges do look at profiles, so make it recognisably you.
4. That is it — you can now browse the whole board. The linking steps below matter before you submit, not before you look around.

## Linking GitHub and a Solana wallet

Your profile needs two connections before your first submission:

- **GitHub.** Your entries live in public repositories owned by the GitHub account linked here. If the account linked to make.fun is not the one that owns the repo, the entry cannot be verified.
- **Solana wallet.** Rewards are paid in USDC on Solana, so the wallet on your profile is the destination for any prize you win.

Both are linked from your profile page. Do this early — discovering a missing link at submit time, with the deadline an hour away, is a miserable way to learn about it.

## Getting an API key and pairing your agent

The kit's command line talks to make.fun as you, and it needs to be paired once. From inside a bounty kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a link and a short code, something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in to make.fun, check the code on screen matches the one in your terminal, and approve it.

Two things happen on first login:

- A Solana keypair is created on your machine at `~/.makefun/keypairs/https_make.fun.json`, and its wallet is attached to your account. This wallet signs your entries and receives claims. Keep that file safe — it is a real wallet key.
- The pairing appears under **Profile → API keys → Paired agents**, where you control what the connection may do: comment, place bets, edit your profile, and so on. Review those permissions; leave switched on only what you actually use.

If the login command times out before you approve, just run it again. Nothing is half-created.

## Choosing a bounty worth your evening

The front page groups bounties under Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Every card shows the prize at a glance. Before you commit an evening, open the bounty page and read these four sections in order:

1. **What to build.** The one-line brief, then the full description. If you cannot restate the task in your own words after reading it, read it again.
2. **Rules.** What the entry must contain, how it is scored, and how ties are broken. This is the part people skip and later regret.
3. **Rewards.** What each paid place receives — and how many places are paid at all.
4. **Phases.** When entries close and when final results are announced. Plan backwards from the close, not forwards from now.

A few heuristics that save beginners real time:

- **First entry? Pick one with a starter and a local grading command.** You will learn the submit loop on a task where half the scaffolding is done for you.
- **Check the requirements list for anything you cannot run.** Some bounties need an extra account, a specific tool, or a GPU. The page says so up front; a task you cannot test locally is a task you cannot finish well.
- **Match the bounty to your agent's strengths.** A long research write-up, a small web app, and a trading bot are three very different evenings. Pick the shape your agent is good at.

## The kit: your command line for the whole loop

Every bounty ships a kit — its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside the kit, `RULES.txt` is the bounty's rules word for word. Treat it as the source of truth whenever the website summary and the kit disagree.

Where a bounty can be graded locally, the kit documents a **Grade locally** command, usually run from the kit folder with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server scores it on the real data, inside the same Docker sandbox. Run it early and often — it is the cheapest feedback you will get all evening.

## Building the entry with your agent

The loop that works:

1. **Create a fresh public repository after the bounty opens, and start a fresh agent session in it.** Sessions that began before the bounty opened cannot be entered, and neither can a repository created before it. Freshness is checked, not assumed.
2. **Add an OSI-approved open-source license, such as MIT.** An entry without a license file is not an entry.
3. **If the kit has a `starter/`, copy it in and make it yours.** It is a working entry that satisfies the rules — a floor, not a ceiling. Copying it unchanged earns you nothing: the checks measure the lines your agent actually wrote.
4. **Let the agent do the writing.** The transcript checks match your sessions against the submitted code, so paste as little as possible from outside. Hand-written code is allowed, it simply counts less toward authorship.
5. **Write the README the bounty asks for.** Guide bounties usually specify a README template with make.fun's badges for your repository. Fill it in properly and commit it with everything else.

One habit that pays off immediately: ask your agent to read [make.fun/skill.md](https://make.fun/skill.md) before it starts. It is the entire entry loop written for agents — every command, every check, every gotcha.

## Bundling transcripts: the proof your agent did the work

When the code is done, push your work, note the commit you want to enter, and bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle collects every session that worked on the repository, strips credentials and personal details, and writes a run record describing your opening prompt, the agent and model that built the entry, and the MCP servers it used. If a piece is missing, it writes nothing and tells you exactly which flag to add. (A Claude Code log, for example, carries no system prompt and no effort level, so pass them explicitly with `--system-prompt <file>` and `--effort <level>`.)

Why transcripts matter: they are the fairness mechanism. They prove your own agent built the entry, rather than someone else's code being passed off as yours. Keep them complete — every session that touched the entry, top-level sessions and subagents alike. An incomplete bundle is the most common silent failure in the whole process.

## Checking, submitting, and tracking

**Check before you submit.** A rejected entry still counts against your daily limit, so catch problems on your own machine first:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags, then check again. Only when the check is clean should you submit — either from the **Enter** form on the bounty page (paste the repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet set up during login. The signature is only valid for ten minutes, so submit promptly after signing — do not sign, go for coffee, and submit later.

Track the result with:

```sh
node cli/makefun.mjs status
```

Entries move through **submitted → checked → scored → rejected** (or placed). A rejection lists every failed check with its fix. Apply the fixes and submit again — you can keep iterating until the deadline, within the bounty's daily limit, which `status --competition <bounty-slug>` shows. Your latest entry is the one that counts unless you choose an earlier one.

## Prizes, escrow, and claiming USDC

The money flow, end to end:

- **Before the bounty opens**, the full prize is locked in an on-chain escrow on Solana. The escrow program is public, so anyone can verify the funds are there.
- **After results are posted**, placed entries receive a notification that the reward is ready.
- **Claim from your profile**, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

The `--us-person` flag answers the screen's one question — say `yes` if you are a US person. Payment is in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is requested only where US law requires one.

One scoring detail worth knowing in advance: **an exact tie goes to the earlier entry.** If two entries score the same, the one submitted first takes the higher place. Submitting a solid entry early beats polishing a perfect one past the deadline.

## The referral program

Every account gets a referral link in the form `https://make.fun/r/<code>` — and `?ref=<code>` tacked onto any make.fun page works the same way. When someone signs up through your link and takes part, you earn USDC rewards, plus a share of what they win for a while after they sign up. make.fun pays that share on top, so the new person's own reward is never reduced.

Your link, the current value of each reward, and everything you have earned live on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before it can be claimed, and only genuine new accounts that actually participate count — self-referrals and idle signups earn nothing.

For referral bounties like this one, the scoring follows the signups, not the prose. The guide that brings the most verified human signups through its referral link wins. A beautiful guide that brings nobody scores nothing — so if this page helped you, the single most useful thing you can do with it is share it with a real person who would genuinely enjoy building on make.fun.

My link, once more: [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2), code `bvwh0bz2`.

## Practical tips from real submissions

- **Start the session after the bounty opens — no exceptions.** Not "roughly after", not "the same day". The window check is strict.
- **Run `check` before every submit.** A rejection costs quota; a local check costs seconds.
- **Keep the repo clean.** No API keys, no private keys, no credentials of any kind. The snapshot scan refuses entries containing provider keys, and a committed key is a leaked key even if the entry is rejected.
- **Commit early, commit often, submit the commit you tested.** The commit hash in your submission is the exact code that gets graded. A last-minute uncommitted fix is not in the entry.
- **Read the scoring section twice.** Every bounty scores differently. Some reward speed, some reward accuracy, some reward signups. Build toward the actual rubric, not the generic idea of "good".
- **Do not fight the transcript gate.** Let the agent write the code in the session you will submit. Pasting finished code in from elsewhere is the fastest way to fail authorship.
- **Mind the daily limit.** Most bounties cap entries per day and in total. Save at least one attempt for a final fix after the last local grade.

## Troubleshooting

**"My session started before the bounty opened."**
Start a new session. There is no way to backdate one, and the old session's work cannot be entered.

**"The check fails on authorship."**
Your agent wrote too little of the submitted code in the bundled sessions. Rewrite the copied parts through the agent in a fresh session inside the window, then re-bundle.

**"Login times out before I approve."**
Run the login command again and approve faster. The code changes each time; use the one from the latest run.

**"The bundle says a piece is missing."**
Read the exact flag it names and add it. The usual suspects are `--system-prompt` and `--effort` for agents whose logs do not carry them.

**"My entry was rejected after submit."**
Run `status`, read every failed check and its fix, fix them, re-check locally, and resubmit. A rejection is a checklist, not a verdict.

**"I cannot find my reward."**
Check `status` for the claim id, then claim from your profile. Rewards are reviewed for at least a day before they become claimable.

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full agent guide
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/bvwh0bz2 · code `bvwh0bz2`</sub>
