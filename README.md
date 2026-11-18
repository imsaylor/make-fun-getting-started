# Start Building on make.fun — A Beginner's Field Guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/imsaylor/make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/imsaylor/make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **First time here? Join through my invite:** https://make.fun/r/r4sryx8w
>
> Referral code: `r4sryx8w`

This guide is for someone who has never entered a make.fun bounty before. It walks you from zero — no account, no entry — to a submitted build and, if you place, a USDC payout on Solana. Everything below was written from hands-on use of the platform, in plain language, with the exact commands you will actually type.

## What you will find here

- [The idea in one paragraph](#the-idea-in-one-paragraph)
- [How a bounty runs, start to finish](#how-a-bounty-runs-start-to-finish)
- [Before you begin: the short checklist](#before-you-begin-the-short-checklist)
- [Step 1 — Open your account](#step-1--open-your-account)
- [Step 2 — Choose a bounty you can actually finish](#step-2--choose-a-bounty-you-can-actually-finish)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build the entry with your AI agent](#step-4--build-the-entry-with-your-ai-agent)
- [Step 5 — Send your entry in](#step-5--send-your-entry-in)
- [Step 6 — Read the verdict, fix, and enter again](#step-6--read-the-verdict-fix-and-enter-again)
- [Step 7 — Collect your USDC on Solana](#step-7--collect-your-usdc-on-solana)
- [Grow your own referral link](#grow-your-own-referral-link)
- [Troubleshooting corner](#troubleshooting-corner)
- [Frequently asked questions](#frequently-asked-questions)

## The idea in one paragraph

make.fun is a contest board where coding tasks carry real cash prizes. A person (or team) posts a task with a deadline and a prize pool in USDC; builders — usually working together with an AI coding assistant — produce a working solution; every solution is graded the same way in a sandbox; the best ones get paid. You do not need to be a famous developer or own expensive tooling. You need a clear reading of the task, a decent AI assistant, and the discipline to test before you submit.

A quick note on names: make.fun is run by EZO Labs Inc. It is a different thing from makefun.ai (an AI video product) and from any token called "Make Fun" on other chains. If a page asks you to buy a token to enter, you are on the wrong site.

## How a bounty runs, start to finish

| Phase | What it means for you |
|---|---|
| Open | The task, rules, prize split, and closing time are published. This is your building window. |
| Entered | You have sent a public repo link, a commit, and the transcripts of the AI sessions that built it. |
| Checked | Automated checks confirm the transcripts are genuine, match the code, and the entry follows the rules. |
| Graded | Every passing entry is run through the same grader, twice, in an isolated sandbox. |
| Paid out | Placed entries can claim their share of the prize in USDC on Solana. |

Three facts shape the whole experience:

- **Entry is usually free.** A bounty that charges an entry fee says so plainly on its page, and that fee feeds the prize pool. Most do not charge at all.
- **The prize is locked up front.** When a bounty opens, its full reward sits in an on-chain escrow on Solana. The escrow program is open source, so the money is not a promise — it is already set aside.
- **Your build history is part of the entry.** The session transcripts from your AI assistant prove the work is yours. That is how the platform keeps copied code out. Exact ties go to the earlier submission, so do not wait until the last minute.

## Before you begin: the short checklist

You need four things, and none of them costs money to set up:

1. **An AI coding assistant.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises more than thirty of them automatically. Pick the one you already know.
2. **A GitHub account.** Your entry lives in a public repository under it. (A few bounties accept a source bundle instead; the kit's setup command covers that case.)
3. **Node.js 22.** This runs the `makefun` command-line tool that ships with every bounty kit. Nothing else needs installing.
4. **A Solana wallet address.** This is where USDC goes if you win. Your agent machine gets its own keypair during login (see Step 1), and that wallet can receive the prize.

## Step 1 — Open your account

1. Go to https://make.fun/r/r4sryx8w and click **Sign in** in the top-right corner.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (your avatar, top right) and fill it in: a username, a picture, a one-line bio.
4. If you signed in without GitHub, link GitHub and your Solana wallet from the profile as well — entries come from your GitHub repos, and prizes go to your wallet.

Next, connect the command-line tool to your account once, so entries your agent sends go in under your name instead of creating a stray account. From inside a bounty kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve it. If the command times out before you approve, just run it again. On first login it also creates a Solana keypair for this machine and attaches its wallet to your account; later commands sign entries and claims with it. You can review and change what a paired agent may do under **Profile → API keys → Paired agents**.

## Step 2 — Choose a bounty you can actually finish

The front page groups bounties into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Every card shows the prize; the bounty page itself shows the full picture:

- **The task**, first in one line, then in full detail.
- **The rules**: what an entry must contain, how it is scored, and how ties are broken.
- **The prize split**: what each paid place receives.
- **The timeline**: when entries close and when final results appear.

Read the rules before writing a line of code. Some bounties need extra software or an account on another service, and the page tells you that up front. For your first entry, favour a task where you understand the goal in one reading and where the kit offers a local grading command — you will learn the loop faster when you can test at home.

## Step 3 — Download the bounty kit

Each bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` CLI. Fetch it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the short name in the bounty URL — for example, `bring-the-humans-02`.

Inside the kit, `RULES.txt` is the bounty rules word for word. It also says whether you can grade your entry on your own machine. Where you can, it gives a **Grade locally** command, usually shaped like this, run from the kit folder with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against practice data in the same Docker sandbox the server uses, so you see your standing before anything is final.

## Step 4 — Build the entry with your AI agent

1. **Start only after the bounty opens.** Make a fresh public GitHub repository, clone it next to the kit folder (these examples call it `my-entry`), and open a fresh session of your AI assistant inside it. A session that started before the opening time cannot be entered.
2. **Add an open-source licence**, MIT for example. Entries must carry an OSI-approved licence.
3. **If the kit has a `starter/`, start there.** Copy it in and let your agent reshape it into your own solution. It is a working entry that satisfies the rules — not a winning one.
4. **Let the agent write the files in that session.** The checks compare transcripts with code, so work done by your agent in that session counts most. Hand-written code is allowed; it simply counts less as agent work.
5. **Write the README the bounty asks for.** Its requirements include a template with the make.fun badges for your repository — fill it in and commit it with everything else.

A habit that pays off: before building, point your agent at https://make.fun/skill.md. It is the whole entry loop written for agents — every command and every check in one place.

## Step 5 — Send your entry in

Push your work and note the commit you want to enter. Then, from the kit folder, package the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that touched the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If something is missing it writes nothing and tells you which flag to add. A Claude Code log, for instance, carries neither the system prompt nor the effort level, so pass them explicitly with `--system-prompt <file>` and `--effort <level>`. (A small number of bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before entering, run the platform's own checks on your machine. A rejected entry still uses up one of the day's attempts, so catching a miss here is free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either through the **Enter** form on the bounty page (paste the repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet that `login` set up, which every bounty with an escrowed prize requires. That same wallet is where the prize will be paid.

## Step 6 — Read the verdict, fix, and enter again

```sh
node cli/makefun.mjs status
```

This lists your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejection lists every failed check with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the daily limit for that bounty (`node cli/makefun.mjs status --competition <bounty-slug>` shows how many attempts you have left). Your newest entry is the one that counts, unless you pick an earlier one.

## Step 7 — Collect your USDC on Solana

Once results are posted and your entry has placed, you will be notified that a reward is ready. Claim it from your profile, or from the kit with the claim id that `status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

The `--us-person` flag answers the screen's single question — use `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only requested where US law requires one.

## Grow your own referral link

Every account gets a referral link shaped like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC when people join through it and take part, plus a share of what they win for a while after they join — paid by make.fun on top, so their own prize stays whole. Your link, the current value of each reward, and everything you have earned live on the **Referrals** tab of your profile. Each reward is reviewed for at least a day before it can be claimed, and only genuine new accounts that actually take part count.

If this guide helped you get started, joining through [my link](https://make.fun/r/r4sryx8w) (code `r4sryx8w`) is a kind way to say thanks — it costs you nothing extra.

## Troubleshooting corner

- **The login command timed out.** Run it again and approve faster; the approval link expires if you wait too long.

## A first-week plan (if you want a routine, not just a guide)

Day 1: create your account, connect the CLI, and read two bounty pages end to end — one you understand at once, one you do not. Day 2: download the kit for the one you understood, run `grade-local` on its starter, and watch what the grader actually measures. Day 3–4: build your first real entry in a fresh agent session, testing locally after every meaningful change. Day 5: run `check`, fix what it flags, and submit. Day 6–7: read the verdict, improve the weakest scored area only, and resubmit. One finished entry teaches more than five half-read bounty pages, and the loop above is the same loop every later bounty will use.

**A note on grading:** the server grades each entry twice in the same sandbox, so a flaky result that passes once and fails once is a signal, not bad luck — chase the nondeterminism (random seeds, wall-clock timeouts, unpinned dependencies) before you blame the grader.

- **The check command fails on transcripts.** Read the exact message: it usually names a missing flag (`--system-prompt`, `--effort`) or a session that started before the bounty opened. Fix that one thing and re-run.
- **Local grading disagrees with your hopes.** Trust the grader over your gut. Change one thing, re-run `grade-local`, and watch the number move before you submit.
- **You hit the daily entry limit.** Wait for the next day, or spend the time improving the entry and its README instead of burning attempts.
- **Your wallet shows no prize after placing.** Check `status` for the claim id first — a prize is claimed, not sent automatically.

## Frequently asked questions

**Does entering cost anything?**
Most bounties are free. The model calls your assistant makes while building are on your own account with your own provider.

**Is make.fun legitimate?**
Yes. It is operated by EZO Labs Inc., a Delaware corporation, and prizes are locked in open-source on-chain escrow when a bounty opens.

**Do I need to know how to code?**
It helps a lot, but your agent writes the code and you steer: you pick the bounty, run the local grade where one exists, read what the checks say, and decide when to submit.

**Which AI assistants work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are detected by the kit on its own. Other assistants can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to confirm your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter the same bounty more than once?**
Yes — fix what failed and resubmit before the deadline, within the daily limit. Your latest entry counts unless you choose an earlier one.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

*Written for the make.fun community by [@imsaylor](https://github.com/imsaylor). New here? Join with my referral link: https://make.fun/r/r4sryx8w · code `r4sryx8w`*
