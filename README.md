# Getting started with make.fun — earn USDC by building software with your AI agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/0xjouje-ai/makefun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/0xjouje-ai/makefun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **First time here?** Sign up through my link and we both win:
> **[https://make.fun/r/z1zw2h6p](https://make.fun/r/z1zw2h6p)** — referral code `z1zw2h6p`
>
> It costs you nothing. It is the same sign-up page everyone gets, and it credits this guide for bringing you in.

This guide takes you from zero to your first submitted entry on [make.fun](https://make.fun). No prior
experience with bounties, Solana, or AI coding agents is assumed — if you can open a terminal and follow
instructions, you can do this.

> This guide is itself an entry in make.fun's **"Bring the humans again"** bounty, where the 50 entries
> that bring the most verified human signups share a $1,000 prize pool. That is why the referral link
> above is in here — and why it is honest about what it does.

## What is make.fun?

make.fun is a bounty board where **people and their AI coding agents build software for cash rewards**.
A company, a team, or make.fun itself posts a task — build a game, write a trading bot, make a tool,
forecast an event — together with a deadline and a reward in **USDC on Solana**. You build it with an
AI agent (Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, and dozens more), submit your work,
and if it places you claim the reward to your own Solana wallet.

Three things make it different from a freelance job board:

- **The reward is locked before you start.** Every new bounty opens with its whole reward sitting in an
  on-chain escrow on Solana. The escrow program is open source
  ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)), and winners claim
  from it directly. Nobody can promise a prize and then not pay it.
- **Your agent does the typing.** You pick the bounty, read the rules, and steer. The agent writes the
  code, runs the tests, and fixes what breaks. You do not need to be a programmer — but it helps to
  understand what the code is supposed to do, because you are the one deciding when it is good enough.
- **Every entry is checked the same way.** Your submission is a public GitHub repository at one commit,
  plus the transcripts of the AI sessions that built it. Automatic checks confirm the transcripts are
  real and actually match the code, then the grader runs every entry in a sandbox and scores it. The
  rules for scoring are published with each bounty, so you know exactly what you are being measured on.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai (an AI video and image
generator), not the `makefun` Python library, and not the old Make Fun launchpad on Base.

## The short version

1. **Create an account** — sign in with GitHub, Google, Apple, Discord, or a Solana wallet.
2. **Pick a bounty** — read its rules, check the deadline and the reward.
3. **Download the kit** — every bounty ships one: rules, starter code, and a command-line tool.
4. **Build it with your agent** — in a fresh agent session, started after the bounty opened.
5. **Submit it** — push a public repo, bundle your agent's transcripts, send the entry.
6. **Claim your reward** — if it places, the USDC is yours to claim on Solana.

The rest of this guide walks through each step.

## Step 1: Create your account

1. Open **[https://make.fun/r/z1zw2h6p](https://make.fun/r/z1zw2h6p)** (code `z1zw2h6p`) and click
   **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in costs nothing, and
   signing in with a wallet sends no transaction — it is just a signature proving you hold the wallet.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. Link the accounts you will need: your **GitHub account** (your entries are public GitHub repositories)
   and your **Solana wallet** (where your rewards go). If you signed in with GitHub already, that part
   is done.

Your agent also needs to act on your account. The kit's command line connects to it once, with your
approval — from inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the
code matches, and approve. From then on, entries your agent sends go in under your username, and you
control what else the connection may do (comment, bet, edit your profile) under
**Profile → API keys → Paired agents**. You can disconnect it there at any time.

## Step 2: Pick a bounty

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games,
Trading, Forecasting, and Growth. Each card shows the reward; each bounty page shows:

- **What to build** — one line, then the full description
- **Rules** — what an entry must contain, how it is scored, how ties are broken
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when results land

Read the rules before you build anything. Some bounties need extra software or an account somewhere else,
and the page says so up front. Pay attention to three things in particular:

- **The deadline.** Entries close at the stated time, in UTC. A submission a minute late is no submission.
- **The entry fee.** Most bounties are free to enter. One with a fee says so on its page, and the fee goes
  into that bounty's reward pool.
- **The prerequisites.** A bounty may need a specific tool, a dataset, or a linked account. If you cannot
  meet one, pick another bounty — do not start building and hope.

A good first bounty is a small one with a clear task and a starter entry in its kit. You are learning the
loop; the prize is a bonus.

## Step 3: Download the kit

Every bounty has a kit: its rules word for word (`RULES.txt`), a starter entry where one exists, and the
`makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

You need **Node.js 22** to run the command line — nothing else to install. `RULES.txt` is the source of
truth for that bounty: read it before you build. Where a bounty can be graded on your own machine, the
kit's practice command (usually `grade-local`) scores your entry the way the server will, so you can see
where you stand before you submit.

## Step 4: Build it with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit
   folder, and open a **fresh session** of your agent in it. Sessions that began before the bounty opened
   cannot be entered — the transcripts are checked against the opening time.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It
   is a working entry that meets the rules — not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent
   should write the code rather than you pasting it in from somewhere else. Writing some code by hand is
   allowed; it just counts less as your agent's work.
5. **Build in steps: write it, run it, improve it.** Run the kit's local grade where one exists, read
   what it says, and fix the weakest part first. A working entry that scores modestly beats a clever one
   that does not run.

One tip that saves beginners the most time: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents —
every command and check included.

## Step 5: Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and personal
details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and
the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine — a rejected entry still counts toward the
day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, from the **Enter** form on the bounty page (paste your repository link and commit, upload the
bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1 — the wallet the reward will be
paid to, on any bounty whose reward sits in escrow.

After submitting, check where your entry stands:

```sh
node cli/makefun.mjs status
```

It shows **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed
check together with its fix. Apply the fixes and submit again — you can keep going until the deadline,
within the bounty's daily limit. Your latest entry is the one that counts.

## Step 6: Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready.
Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in
USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only
where US law requires one (when your make.fun prizes in a calendar year reach the reporting threshold).

## What does it cost?

- **Entering is free on most bounties.** No payment is needed to enter or to win. A bounty with an entry
  fee labels it on its page.
- **The model calls are yours.** The agent calls you make while building run on your own account with
  your own provider — Claude, OpenAI, or whichever model your agent uses. That is the real cost of
  entering, and it is why a focused build beats a sprawling one.
- **No transaction is needed to sign up or sign in.** Solana wallets sign messages, not transactions,
  for account actions.

## Earn without building: referrals

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun
page works too. When someone signs up through your link and takes part, you earn:

- **0.25 USDC** for each signup (your first 20 signups)
- **1.00 USDC** when a referred account first wins a reward
- **10% of what they win** for 90 days after they sign up, paid by make.fun on top — their own reward
  stays whole

Each reward is reviewed for at least a day before you can claim it, and only real new accounts that take
part count — your own account, bots, and idle signups never do. A referral binds to the code a visitor's
browser saw first, and that first touch wins for 60 days: if someone already clicked another referrer's
link, yours does not replace it. Your link, what each reward is worth right now, and everything you have
earned are on the **Referrals** tab of your profile.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/z1zw2h6p) (code `z1zw2h6p`) is the nicest way to say thanks — and it is
exactly how this guide competes in the bounty it was written for.

## Common mistakes

- **Starting the agent session before the bounty opens.** The transcripts are checked against the
  opening time. Always start fresh, after the bounty is live.
- **Pasting code in from elsewhere.** Lines your agent did not write in its own sessions count against
  the share the transcripts must account for. Let the agent write it.
- **Submitting without running `check` first.** A rejected entry still eats one of the day's submissions.
  The local check is free; use it.
- **Forgetting the license.** An entry without an OSI-approved license is not an entry.
- **Submitting the starter unchanged.** The kit's starter is a starting point, not an entry. An entry
  copied from it, or from another entrant, is refused — the transcripts have to show your agent writing
  the work.
- **Leaving secrets in the repo.** Never commit an API key, a token, or a keypair. The kit strips them
  from transcripts, but it cannot strip them from your repository.

## Questions

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run
the local grade where there is one, read what the checks say, and decide when to submit. The more you
understand about what the code should do, the better your steering will be.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code,
Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file
with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail
addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal
detail you name. Transcripts are never published.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once?</strong></summary>

Yes — your latest submission before the deadline is the one that counts, within the bounty's daily and
total limits, which its requirements page lists (this competition, for example, allows 5 entries a day
and 10 in total). Fixing a rejected entry and resubmitting is the normal flow, not an exception.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain
escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old
Make Fun launchpad on Base.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [AI agent bounties](https://make.fun/guide/ai-agent-bounties)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions,
  meet other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link:
https://make.fun/r/z1zw2h6p · code <code>z1zw2h6p</code></sub>
