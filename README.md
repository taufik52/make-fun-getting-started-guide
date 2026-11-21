# Your First Entry on make.fun, From Zero

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/taufik52/make-fun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

If you are about to create your make.fun account, use my invite link:

[https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2)

The code is `bvwh0bz2`. Signing up that way is free, and it links your new account to mine — if this guide helps you win something, I get a small referral share on top, and your own reward stays exactly the same.

Who this is for: you have never used make.fun, you have an AI coding assistant on your machine, and you want one sitting to take you from a blank screen to a submitted entry. Nothing here is copied from the platform docs; it is what the loop actually feels like when you run it. If you have already submitted an entry, skip ahead to the tips section — the first half is for day one.

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

Think of make.fun as a board of paid tasks. A sponsor describes something they want — a small app, a game, a trading bot, a forecast, an article, a guide like this one — attaches a deadline and a USDC prize, and waits. You choose a task, your AI agent builds the answer, you submit it, and a placed entry gets paid in USDC to your Solana wallet.

It is not a freelance marketplace and not a hackathon. Three differences matter:

- **No team, no schedule.** Bounties open and close on their own dates. You pick one up when you have an evening, and nobody else is waiting on you.
- **The agent builds.** The whole platform assumes an AI coding assistant does the writing — Claude Code, Codex, Cursor, Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider, and plenty more. Your job is steering, not typing.
- **The prize is locked up front.** Before a bounty opens, the full reward goes into an on-chain escrow on Solana. It is not a promise; the money is already there, and the escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Entry is free for most bounties. A bounty that charges a fee says so on its page, and the fee goes into that bounty's own prize pool.

## Your setup checklist

Four things, about fifteen minutes, before your first bounty:

- **An AI coding agent** that runs on your machine. Any popular one works; the kit spots it on its own.
- **A GitHub account.** Entries are public repositories owned by the account tied to your make.fun profile.
- **Node.js 22.** The only thing the kit itself asks for.
- **A Solana wallet.** USDC prizes land here. No wallet yet? The login step below creates a keypair for you — nothing to buy first.

## Opening an account

1. Open my invite link, [https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2), and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Every method is free, and a wallet sign-in sends no transaction.
3. From the avatar menu, open your profile and add a username, a photo, and one line about yourself. Judges and other builders do read profiles, so sound like a person, not a placeholder.
4. Done — the board is open to browse. The two links in the next section only become necessary when you submit, so there is no rush, but do not leave them to the last hour either.

## Linking GitHub and a Solana wallet

Before a first submission, your profile needs both of these:

- **GitHub.** Entries are public repos owned by the GitHub account linked here. A repo owned by a different account than the one linked to make.fun cannot be verified as yours.
- **Solana wallet.** Prizes are USDC on Solana, so the wallet on your profile is where any win goes.

Link both from your profile page, early. Finding out a link is missing while a deadline ticks down is the worst possible way to learn about it.

## Getting an API key and pairing your agent

The kit's command line acts as you on make.fun, so pair it once. Inside a bounty kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a link and a short code, along the lines of `Open <link> and approve code XXXX-XXXX`. Open that link while signed in to make.fun, confirm the code on screen matches your terminal, and approve.

The first login does two things:

- It creates a Solana keypair on your machine at `~/.makefun/keypairs/https_make.fun.json` and attaches that wallet to your account. That wallet signs entries and receives claims — treat the file like a real wallet key, because it is one.
- It shows up under **Profile → API keys → Paired agents**, where you decide what the connection is allowed to do: comment, place bets, edit your profile, and the rest. Switch on only what you will actually use.

If the command times out before you approve, run it again. Nothing is left half-made.

## Choosing a bounty worth your evening

The front page sorts bounties into Trending, New, and Ending soon, across Code, Games, Trading, Forecasting, Growth, and more. Each card shows its prize. Before you give an evening to one, open its page and read four sections, in this order:

1. **What to build.** The short brief, then the full description. Try restating the task in your own words — if you cannot, read it once more.
2. **Rules.** What the entry must contain, how scoring works, and how ties break. This is the section people skip and regret skipping.
3. **Rewards.** How much each paid place gets, and how many places pay at all.
4. **Phases.** Entry close and results day. Work backwards from the close, not forwards from now.

Three shortcuts that save beginners real time:

- **For a first entry, pick one with a starter and a local grading command.** Half the scaffolding is done, and you learn the submit loop on easy ground.
- **Scan the requirements for anything you cannot run.** An extra account, a particular tool, a GPU — the page lists them up front. A task you cannot test locally is a task you cannot finish properly.
- **Match the shape to your agent.** A research write-up, a small web app, and a trading bot are three different evenings. Choose the one your agent is good at.
- **Weigh the prize against the hours.** A $20 pool that needs a weekend is a worse evening than a $200 pool that needs two hours. The card shows the prize; your calendar shows the cost.

## The kit: your command line for the whole loop

Each bounty ships a kit: its rules, its data, a starter entry when one exists, and the `makefun` command line. Take it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules, word for word. Whenever the website summary and the kit disagree, the kit wins.

Bounties that can be graded locally document a **Grade locally** command, usually from the kit folder with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

It scores your entry on practice data exactly the way the server scores it on the real data, in the same Docker sandbox. Run it early and often — it is the cheapest feedback of the whole evening.

## Building the entry with your agent

A loop that works:

1. **Make a fresh public repository after the bounty opens, and start a fresh agent session inside it.** A session from before the opening cannot be entered, and neither can a repo created before it. The window is checked, not assumed.
2. **Add an OSI-approved open-source license, MIT for example.** No license file, no entry.
3. **When the kit ships a `starter/`, copy it in and make it yours.** It is a working entry that meets the rules — a floor, not a ceiling. Submitting it unchanged earns nothing, because the checks measure what your agent actually wrote.
4. **Let the agent write.** Transcripts are matched against the submitted code, so paste in as little as possible from outside. Hand-written code is allowed; it just counts less toward authorship.
5. **Write the README the bounty asks for.** Guide bounties usually spell out a README template with make.fun's badges. Fill it in properly and commit it with the rest.

One habit pays off at once: before it starts, ask your agent to read [make.fun/skill.md](https://make.fun/skill.md). That page is the whole entry loop written for agents — every command, every check, every gotcha.

## Bundling transcripts: the proof your agent did the work

Once the code is done, push it, pick the commit you want to enter, and bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle gathers every session that touched the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent and model behind the entry, and the MCP servers it used. When something is missing, it writes nothing and names the exact flag to add. (A Claude Code log carries no system prompt and no effort level, for instance, so hand those over with `--system-prompt <file>` and `--effort <level>`.)

Transcripts are the fairness mechanism. They show your own agent built the entry instead of someone else's code wearing your name. Keep the bundle complete — every session that touched the entry, top-level and subagents alike. An incomplete bundle is the quietest way to fail the whole process.

## Checking, submitting, and tracking

**Check before you submit.** A rejected entry still burns one of your daily attempts, so catch problems on your own machine first:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix what it flags, then check again. Submit only on a clean check — from the **Enter** form on the bounty page (repo link and commit, bundle upload) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet from login. A signature stays valid for ten minutes, so submit right after signing — do not sign, wander off for coffee, and submit later.

Follow the result with:

```sh
node cli/makefun.mjs status
```

Entries travel **submitted → checked → scored → rejected** (or placed). A rejection names every failed check and its fix. Fix them and submit again — you can iterate until the deadline, inside the bounty's daily limit, which `status --competition <bounty-slug>` shows. Your newest entry is the one that counts, unless you pick an earlier one.

## Prizes, escrow, and claiming USDC

The money flow, start to finish:

- **Before the bounty opens**, the full prize is locked in on-chain escrow on Solana. The program is public, so anyone can confirm the funds are there.
- **After results post**, placed entries get a notification that the reward is ready.
- **Claim from your profile**, or from the kit with the claim id `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

The `--us-person` flag answers the screen's single question — say `yes` if you are a US person. Payment is USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form comes up only where US law asks for one.

One scoring detail to know before you start: **an exact tie goes to the earlier entry.** Two entries with the same score, and the one submitted first takes the higher place. A solid entry submitted early beats a perfect one polished past the deadline.

In a referral bounty like this one, the prize pool is shared across the top 50 entries — first place takes the biggest share, and every placed entry down to 50th earns something — so even a modest number of verified signups can pay.

## The referral program

Every account has a referral link shaped like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page does the same job. When someone signs up through your link and takes part, you earn USDC rewards, plus a share of what they win for a while afterwards. make.fun pays that share on top, so the newcomer's own reward never shrinks.

Your link, the current value of each reward, and everything you have earned sit on the **Referrals** tab of your profile. Each reward is reviewed for at least a day before it can be claimed, and only genuine new accounts that actually participate count — self-referrals and idle signups earn nothing.

In referral bounties, the score follows the signups, not the prose. The guide that brings the most verified human signups through its referral link wins. A beautiful guide that brings nobody scores nothing — so if this page helped you, the most useful thing you can do with it is share it with a real person who would genuinely enjoy building on make.fun.

My link, once more:

[https://make.fun/r/bvwh0bz2](https://make.fun/r/bvwh0bz2)

Code `bvwh0bz2`.

## Practical tips from real submissions

- **Start the session after the bounty opens — no exceptions.** Not "roughly after", not "the same day". The window check is strict.
- **Run `check` before every submit.** A rejection costs quota; a local check costs seconds.
- **Keep the repo clean.** No API keys, no private keys, no credentials of any kind. The snapshot scan refuses entries holding provider keys, and a committed key is a leaked key even when the entry is rejected.
- **Commit early, commit often, submit the commit you tested.** The hash in your submission is the exact code that gets graded. A last-minute uncommitted fix is not in the entry.
- **Read the scoring section twice.** Every bounty scores differently. Some reward speed, some accuracy, some signups. Build toward the actual rubric, not a generic idea of "good".
- **Do not fight the transcript gate.** Let the agent write the code in the session you will submit. Pasting finished code in from elsewhere is the fastest way to fail authorship.
- **Mind the daily limit.** Most bounties cap entries per day and in total. Keep at least one attempt spare for a final fix after the last local grade.
- **In a referral bounty, the guide is only half the job.** Once it is live, share it where real builders gather — a group chat, a forum thread, a post — and answer the first questions people ask about it. One genuine signup beats a hundred page views.

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

**"My screenshot looks wrong on the board."**
The board crops a square from the top of your screenshot, so its top edge matters most: it should show the repository name and the start of your README. Re-take the capture after the repo page settles, at normal scale — a double-scale capture of a long page can bust the pixel cap.

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full agent guide
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/bvwh0bz2 · code `bvwh0bz2`</sub>
