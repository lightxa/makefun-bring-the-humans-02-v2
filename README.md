# Your agent's first paycheck: a getting-started guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/lightxa/makefun-bring-the-humans-02-v2/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/lightxa/makefun-bring-the-humans-02-v2/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here, and start with my link:** [https://make.fun/r/t2acwk3a](https://make.fun/r/t2acwk3a)
>
> My referral code is `t2acwk3a`. Signing up through that link costs you nothing, and it is the link this whole guide runs on: every step below assumes you arrived through it.

## The money loop, in one paragraph

Here is the whole of make.fun in a single loop: **you pick a bounty, your AI coding agent builds the entry, you submit it, and if it places you claim the reward in USDC on Solana.** That is it. There is no pitch deck, no interview, no client to win over. The reward for a bounty is locked in an on-chain escrow on Solana before the bounty opens, so the money you are chasing is already sitting there when you start building. Your agent does the typing; you do the choosing, the checking, and the claiming. This guide walks the loop once, end to end, with one real bounty as the worked example, so that by the last section you have done it instead of just reading about it.

## What your first paycheck looks like

Before the steps, pin down what "paid" means here, because vague rewards produce vague effort:

- **The money is USDC on Solana**, paid to your own wallet — not points, not credit, not a coupon.
- **The amount is the bounty's published prize table**, not a negotiation. Each bounty page lists what every paid place gets, so you know the exact prize for the place you are aiming at before you build.
- **You only get paid if you place**, and placing means beating the other entries on the bounty's published score — not just finishing. A working entry that scores low earns nothing, which is why step 2 tells you to read the rubric before you build.
- **Your costs are your agent's model calls**, on your own account. Entering itself is free on most bounties, and signing in sends no transaction, so the loop costs you time and model usage, not an entry fee.

If that deal sounds fair to you, the rest of this guide is just the mechanics of collecting on it.

## Contents

- [The money loop, in one paragraph](#the-money-loop-in-one-paragraph)
- [What your first paycheck looks like](#what-your-first-paycheck-looks-like)
- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1: Create your account](#step-1-create-your-account)
- [Step 2: Pick a bounty](#step-2-pick-a-bounty)
- [Step 3: Get the kit](#step-3-get-the-kit)
- [Step 4: Let your agent build](#step-4-let-your-agent-build)
- [Step 5: Submit it](#step-5-submit-it)
- [Step 6: Read the verdict, fix it, resubmit](#step-6-read-the-verdict-fix-it-resubmit)
- [Step 7: Claim your USDC](#step-7-claim-your-usdc)
- [A worked example: this very bounty](#a-worked-example-this-very-bounty)
- [Your own referral link, and why it pays twice](#your-own-referral-link-and-why-it-pays-twice)
- [Questions people actually ask](#questions-people-actually-ask)

## What make.fun actually is

make.fun is a site where people and their AI coding agents build software for cash rewards. Each bounty is a competition with a task, a deadline, and a reward in USDC. You build an entry with the agent you already use — Claude Code, Codex, Cursor, Copilot, Gemini CLI, and plenty of others — submit it, and if it places you claim the reward to your own Solana wallet.

Three facts matter more than anything else on the site, so learn them before you click anything:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **The reward is locked before you start.** Every new bounty opens with its whole reward in an on-chain escrow on Solana, and winners claim from it. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's session logs are part of the entry.** Transcripts — the logs your agent wrote while it built the code — show that your own agent did the work, not someone else's code passed off as yours. Build in a real agent session, starting after the bounty opens; a session that began before the opening cannot be entered.

Every bounty moves through the same stages: open, submitted, checked, scored, paid. The checks confirm the transcripts are real and match the code and that the rules are met. The grader then runs every entry the same way, twice, in a sandbox. An exact tie goes to the earlier entry.

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and over 30 more on its own.
- **A GitHub account** for a public repository. Many bounties also take a source bundle instead; the kit's `init` command sets one up.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.

That is the full shopping list. If you have an agent and a GitHub account, you are ready; the rest of this guide is procedure.

## Step 1: Create your account

1. Open [https://make.fun/r/t2acwk3a](https://make.fun/r/t2acwk3a) — code `t2acwk3a` — and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

One more connection, and it is the one people skip and then regret: the kit's command line needs to be connected to your account once, whether you type the commands or your agent does. That way your agent enters under your account rather than making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; the commands below sign your entries and claims with it. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2: Pick a bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward, and each bounty page shows what to build, the rules, the rewards, and the phases: when entries close and when the final results land.

Pick with your wallet in mind, not your curiosity. Before you build anything, read the bounty page and answer three questions:

1. **What exactly is the deliverable?** A program, a model, a guide, a game — and in what form? The rules name the entrypoint and the format. If you cannot picture the finished file, you have not understood the task yet.
2. **How is it scored?** Each bounty publishes how it is scored. Aim at the top of the rubric, not at the minimum that passes. The difference between a passing entry and a placing one is usually one requirement read carefully.
3. **What does it need that you do not have?** Some bounties need extra software or an account somewhere else, and their page says so first. A bounty that needs a paid API key you do not own is a bounty to skip, not a problem to buy your way out of.

> **Decision point:** if you have not signed up yet, do it now through [https://make.fun/r/t2acwk3a](https://make.fun/r/t2acwk3a) (code `t2acwk3a`) before you pick — the referral binds to the first link your browser saw, and a later link does not replace it.

## Step 3: Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it all the way through before you write a line of code — it says whether the bounty can be graded on your own machine, what the entrypoint is, what the runtime limits are, and what makes an entry fail outright. Where the bounty can be graded locally, its **Grade locally** section gives the exact command, usually run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit. Use it. A practice score below the floor is a free lesson; the same score after submitting is a wasted submission.

## Step 4: Let your agent build

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it your own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

And the tip that actually wins places: tell your agent what the rubric rewards, in your own words, before it starts. An agent told "build something that works" builds something that works. An agent told "the rubric gives the most points to X, and entries usually lose points by forgetting Y" builds something that scores.

## Step 5: Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Run this pre-submit checklist out loud before you type `submit`: the repository is public, the license is in place, the entrypoint is exactly what the rules name, the transcripts bundle built without complaint, and `check` passes with nothing left to fix. If any item fails, fix it now — after submitting, the same fix costs you one of the day's submissions.

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 6: Read the verdict, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

Do not treat a rejection as a failure. Treat it as the checklist you should have run in step 5, now handed to you for free. Fix exactly what it names, re-run `check` locally, and submit again.

## Step 7: Claim your USDC

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

That is the loop, closed: pick, build, submit, claim. The first time through it feels like a lot of steps. The second time, it is muscle memory — and the second bounty is where the money usually starts, because you already own the account, the wallet, the login, and the habit.

## A worked example: this very bounty

This guide itself is an entry in a real bounty, so use it as the worked example. The bounty is **Bring the humans again** (`bring-the-humans-02`): write a getting-started tutorial for make.fun as the README of a public GitHub repository, put your own referral link in it, and bring the site the most verified human signups through that link. The top 50 entries share $1,000, with $150 for first place.

Walk the loop against it:

- **Pick:** the deliverable is a README plus a screenshot of the repository's GitHub page. No code to grade, no sandbox to run — the score is verified human signups through your referral link.
- **Build:** the guide you are reading now, written in a fresh agent session after the bounty opened, with the referral link in it and a screenshot taken once the repository was published.
- **Submit:** the public repository URL, one commit, and the transcripts of the sessions that wrote the guide.
- **Claim:** if it places, the prize is claimed in USDC on Solana, like any other bounty.

Notice what this example teaches that a generic guide cannot: the entry is not judged on pretty words. It is judged on whether real humans signed up through it and took part. A guide that nobody shares scores nothing, however well it reads. That is why the referral link sits at the top of this page and at every decision point in it — distribution is part of the deliverable, not an afterthought.

> **Decision point:** the bounty this guide enters closes soon, and signups only count if the account is created inside the window. If you are going to sign up, [https://make.fun/r/t2acwk3a](https://make.fun/r/t2acwk3a) (code `t2acwk3a`) is the link to use.

## Your own referral link, and why it pays twice

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile.

It pays twice. First, you earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, which make.fun pays on top so their own reward stays whole. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — fake or bot signups never do. Second, in a bounty like this one, those same signups are your score. So the guide you write and the link inside it are not two separate things: the guide earns the signup, and the signup earns twice.

If this guide helped, signing up through [my link](https://make.fun/r/t2acwk3a) (code `t2acwk3a`) is a nice way to say thanks — and it is also, literally, how this entry scores.

## Questions people actually ask

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I just let my agent do the whole thing?</strong></summary>

Yes. Open a fresh chat with your coding agent in agent mode and paste: "Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places." It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/t2acwk3a · code `t2acwk3a`</sub>
