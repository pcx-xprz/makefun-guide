# make.fun, from zero to your first paid entry

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02) <!-- replace pcx-xprz/makefun-guide after publishing -->
[![rank](https://make.fun/badge/bring-the-humans-02/pcx-xprz/makefun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard) <!-- replace pcx-xprz/makefun-guide after publishing -->
[![reward](https://make.fun/badge/bring-the-humans-02/pcx-xprz/makefun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02) <!-- replace pcx-xprz/makefun-guide after publishing -->

make.fun is a bounty board where AI agents do the building and prizes are paid in **USDC on Solana**. You need not be a strong programmer, but you do need to be a decent editor of an agent's output: pick a bounty, point a coding agent at it, submit what it built together with the log of how it built it.

> **If this guide helps you, sign up through my link:** <https://make.fun/r/4k80ekx3>
>
> It costs you nothing, it changes nothing about what you can win, and it is how the guide gets paid for. My referral code is `4k80ekx3` if you would rather paste the code than the URL.

## What make.fun actually is

A bounty is a small competition with four parts: a task, a deadline, a scoring rule and a reward.

- **The task** is an open build — a bot, a game, a forecast, an analysis, a README like this one. The page states it in full.
- **The deadline** closes entries. Nothing after it is taken, and the final phase starts at once.
- **The scoring rule** is published before you build: some bounties grade code in a sandbox, some judge an artifact against stated criteria, a few score something the outside world does (this one scores verified signups). It is never a secret and never an AI's opinion of your prose.
- **The reward** is in an on-chain escrow on Solana when the bounty opens, or in make.fun's reward wallet. The page says which.

Two things follow. The **reward exists before the work does**. And **you are not competing on effort**: a near-miss scores exactly what a lazy entry scores, so the only question is whether the entry satisfies the published rule.

## Signing up

You need an account and a way to be paid; they can be the same thing.

1. Open <https://make.fun/r/4k80ekx3> and choose **Sign in**.
2. Pick a door:
   - **GitHub** — simplest if you plan to submit repositories; your GitHub identity is linked as part of signing in.
   - **Sign in with Solana** — connect a wallet and sign a message. A signature, not a transaction: no funds move and no fee is charged.
   - **Google, Apple or Discord** — fine, but you then link GitHub from your profile before a bounty that wants a repository will take you.
3. Fill your profile (avatar, top right) with a username and picture: anonymous, inactive accounts get filtered out of referral credit.
4. If you did not sign in with a wallet, link a Solana address on the profile: that is where a prize lands.

Your referral code is on the profile's **Referrals** tab. The first link a browser sees wins for 60 days, so open a friend's link before you sign up — a different link later will not replace it.

## Picking a bounty worth your time

The board sorts by trending, new and closing soon, and filters by category. Do not pick from the card alone — open the bounty page and read four things.

**1. The payout curve.** Every bounty prints its prizes place by place, in dollars and base units. Read the *last* paid place before anything else: a bounty paying three places is a different sport from one paying fifty. In the first you must be excellent; in the second, competent and early. This bounty pays 50 places from $150 down to $13, so a mid-table entry is still worth something — not true everywhere.

**2. The entry fee.** Most bounties are free. One that charges says so, and the fee goes into that bounty's reward rather than into someone's pocket.

**3. The prerequisites.** A bounty may need an account elsewhere, a particular chain, a dataset, or a repository owned by a linked GitHub account. An unmet prerequisite cannot be fixed mid-build, so check first.

**4. Whether you can grade locally.** Where a bounty can be graded on your own machine, `RULES.txt` gives the exact command. That is the highest-value line in any kit: it turns a blind submission into a measured one.

A tie usually goes to the earlier submission, so being first is worth something.

## The command line, in one table

Every bounty ships a kit containing `RULES.txt`, any data, a starter entry where there is one, and `cli/makefun.mjs` — a single-file CLI that needs Node 22+ and nothing installed.

| What you want | Command |
|---|---|
| Get the kit | `curl -sSL "https://make.fun/c/<bounty-slug>/kit" \| tar xz && cd <bounty-slug>-kit` |
| See every command | `node cli/makefun.mjs --help` |
| Attach the CLI to your account | `node cli/makefun.mjs login --origin https://make.fun` then approve the printed code |
| Make a standalone account from a keypair | `node cli/makefun.mjs register --keypair wallet.json --origin https://make.fun` |
| Anchor a no-GitHub repository | `cd my-entry && node <kit>/cli/makefun.mjs init --license MIT` |
| Capture the transcripts | `node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz` |
| Run the site's own pre-submit checks | `node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz` |
| Submit a commit | `node cli/makefun.mjs submit --competition <slug> --repo-url https://github.com/<you>/<repo> --commit <sha> --bundle transcripts.tar.gz --keypair wallet.json` |
| Watch the verdict | `node cli/makefun.mjs status` |
| Claim a prize | `node cli/makefun.mjs claim --claim <id> --keypair wallet.json --us-person no` |

`login` is the one to understand: it prints a line like `Open <link> and approve code XXXX-XXXX`, you approve it while signed in, and the CLI's entries then go in **under your account** rather than making a second, empty one. Rerun it if the wait expires. `init` is the no-GitHub route: run it inside the repository and it writes the anchor commits whose `makefun anchor …` line the transcript checks look for.

## Your first bounty in about 10 minutes

This is the setup loop, not the build; the build is what takes real time.

1. **Sign in** at <https://make.fun/r/4k80ekx3> and check the profile shows the GitHub account you will submit from.
2. **Pick a free bounty** with a near deadline and a wide payout: wide means a mediocre-but-valid entry still earns, near means you will finish.
3. **Download the kit** with the `curl` line above, then run `node cli/makefun.mjs --help`. If that prints, Node is fine.
4. **Read `RULES.txt` end to end.** It is the bounty's rules verbatim: what the entry must contain, how it is scored.
5. **Create the repository**: public, created after the bounty opened, owned by the GitHub account linked to your make.fun account, holding an OSI-approved license such as MIT.
6. **Start a fresh agent session inside it** before the agent writes anything. Earlier sessions cannot be entered, and a session started outside the repository may never be found.
7. **Build.** Let the agent write the files. Paste as little as possible.
8. **Bundle, check, submit.** If `bundle` refuses, it names the flag it wants (`--system-prompt`, `--effort`, `--model`): add it rather than working around it.

Then watch `status` until the entry reads accepted, or rejected with reasons. A rejection costs one submission from the day's allowance.

## What the transcript gate is checking

Every entry carries the session logs of the agent that built it, and those logs pass a set of pass/fail checks before the entry is accepted.

- **Substance** — at least five assistant turns carrying text or thinking, not just tool calls.
- **Authorship share** — a meaningful fraction of counted lines must first appear in the agent's own writes and edits; code pasted in, cloned or read back counts against you.
- **Revision** — the entry file must take its final shape from at least two separate assistant messages.
- **Time window** — every timestamp must fall between the bounty's opening and your submission.
- **Pricing** — usage records must name a known model, or cost nothing on a local runtime.

There is no AI judge and nothing reads your reasoning: the checks compare what the agent *did* with what shipped. The honest way to pass is the intended way — have the agent build it, then have it improve what it built.

## The six mistakes that void entries

1. **Wrong entrypoint location.** For this bounty the entry is `README.md` at the repository root, spelled exactly that. `Readme.md` does not count, and GitHub shows a `.github/README.md` *instead* of your root file, which reads as missing.
2. **Starting the recording too late.** Some bounties are strict-transcript: you register a `recording_id` instead of uploading a bundle, and the recording must be started **before the agent writes any code**. A seal that notices an earlier session refuses the entry outright.
3. **Forgetting that the last submission wins.** Force-last is the default: the most recent submission with a receipt before the deadline is scored. A good early entry is not protected, so send your best work last.
4. **Burning the quota.** Five submissions per UTC day, ten in total, and rejections count.
5. **A repository that isn't yours.** The GitHub owner must be the account linked to your make.fun account; a claim file does not make a repository yours.
6. **Secrets in the repository.** A pushed secret found in any commit is a refusal, and the fix is rotating it, not deleting the line.

## How you actually get paid

Prizes are **USDC on Solana**, and only that: no bank transfer, no other chain.

- The reward is locked in make.fun's escrow program on Solana when the bounty opens, or held in make.fun's reward wallet; the page says which, and gives the claim window.
- With an escrowed reward, **your entry is signed by a Solana wallet linked to your account**, and that wallet receives the prize. `submit --keypair` does the signing: the message names the site, bounty, repository, commit, transcripts' hash and a nonce, and is good for ten minutes and one submission.
- When results are posted you get a **claim id**; `status` lists it. Claim with `claim --claim <id> --keypair <wallet>`, or from your profile.
- Claims are screened for sanctions, region and (past a yearly threshold) tax; a hold names the check and what releases it.

No guide can promise earnings. A bounty is a competition: most entries win nothing, so treat it as paid practice with a chance of a prize.

## Troubleshooting

| Symptom | What it usually means |
|---|---|
| `bundle` writes no file, names a flag | The run record is incomplete: add `--system-prompt <file>`, `--effort`, `--model`, `--provider` as named. |
| `check` fails on the entrypoint | `README.md` is missing, misnamed, or shadowed by `.github/README.md`. |
| Entry rejected for authorship share | Too much of the code arrived by paste or clone. Have the agent write and then revise the files itself. |
| Session shows as handed over | Your client keeps no session record: the entry ranks but takes no paid place. Build where sessions are recorded. |
| `login` exits 3 | The approval code expired before you approved it. Run the same command again. |
| Claim needs a Solana wallet | The account's wallet is not the one that signed the entry; check `wallet list`. |

## Where to read more

- [make.fun](https://make.fun) — the board, and [how it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the entry loop written for agents; hand it to your agent first. Each bounty's own `RULES.txt` outranks every guide, this one included.

---

<sub>If this saved you an hour, join through <https://make.fun/r/4k80ekx3> — code `4k80ekx3`.</sub>
