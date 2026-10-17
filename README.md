# Atlas

**The Atlas of Everything.**

What runs today: Atlas helps you learn. You open it in a browser, choose one of 100 subjects, and read short lessons with pictures and exercises you can try. You get facts that show their sources. The first page is a proof screen. It shows one claim from the atlas, where that claim came from, who stands behind it, how it was checked, what it links to, and its seal. The same claim is shown in full on a phone, in short on a watch, read aloud by voice, and in large type on a public screen.

The AI tutor that used to headline this page was dropped on 2026-10-15, by direction. Its eval harness and results stay in this repo as an archived experiment; see The proof, below.

## The need

This repo serves Layer 2: Learning. "The ability to learn what you need, when you need it, at a price that does not exclude you, from teaching that does not invent its facts." Atlas serves that need in a plain way: it records the source of what it teaches and shows its work, claim by claim.

Unmet, it looks like this: students who cannot pay for the tutoring that helps them pass, adults who cannot get training for a new job, and knowledge kept behind paywalls and hard words.

The full map: [The Ascent, a map of human needs](https://github.com/topsoilcommons/topsoilcommons/blob/main/NEEDS.md)

## What it is

Subjects range from physics and mathematics to plumbing, beekeeping, chess, and pastry. You can browse it like an atlas, a few pages at a time, instead of taking a full course. It is for people learning on their own, for teachers who need good material fast, and for anyone who wants a clear place to start a new topic.

### What is in here

- A React application (no framework, esbuild compiled) with an atlas browser, chapter views, interactive visualizations, a workshop, and learning paths. The demo entry point is a static proof screen (`index.html`); the full app sits behind it at `atlas.html`.
- A content pipeline (`tools/`): scripts that generate and enrich subject content with an LLM, weighted by explicit source reliability scores (`tools/source-weights.cjs`), and governed by a written grounding policy (`content/_grounding.md`). The position is simple: AI generated learning content should cite its sources, weight them by trustworthiness, and say so in the open.
- Vercel serverless functions (`api/`): a chat proxy, a claim endpoint, an ops digest, and a Stripe webhook. The chat proxy is hardened in the ordinary production ways: origin allowlist, app check, auth verification, per user rate limiting, and input validation, with the provider key kept server side (`lib/proxy-guard.js`).
- Supabase schema and seed tooling (`supabase/`): three migrations (foundation, security hardening, academic verification) and the full seed dataset.

### Run it locally

```bash
npm install
npm run build        # compiles the app to dist/sg-app.js
npm run dev          # serves the folder on http://localhost:3000
```

Without a build, open `index.html` with `?babel=1` and it falls back to in browser compilation for development. The content bundle (`content/_bundle.js`) is generated, not committed; rebuild it with `npm run build:content`.

Accounts, payments, and the tutor need environment configuration (Supabase project, Stripe keys, and an LLM provider key for the chat proxy). Everything else runs from the static bundle.

### Architecture, briefly

The front end is a set of JSX modules compiled in dependency order by `scripts/build.cjs`, each wrapped in its own scope to mirror how the app originally ran with in browser Babel. Content is data, not code paths: subject modules register lessons into a shared manifest, so adding a subject is adding a file. Server concerns live only in `api/` and `lib/`, so the static atlas can be hosted anywhere.

### Roadmap

- **LLM mode eval runs in CI (planned).** The harness already supports grading a live model against the same facts and gates; it needs an API key in CI secrets to run on a schedule.
- **Pedagogy cases in the eval set (planned).** Questions that test whether the tutor diagnoses a misconception and adapts an explanation to a stated level, not only whether its facts are right. This is where tutor evaluation is heading; see `docs/LANDSCAPE.md`.
- **Citation guard at answer time (planned).** Move from measuring citations after the fact to withholding any answer sentence that cannot resolve to a retrieved passage.

### Where this is headed

Direction, not shipped capability: the field is moving toward tutors that are auditable, where every claim traces to a source a teacher can inspect and the eval report is part of the product. Atlas is being built in that order on purpose: the grounding policy came first, the measurement second, and the generative layer stays on a leash held by both. The full scan behind this paragraph, with sources, is in `docs/LANDSCAPE.md`.

### The larger story

Atlas is learning, Layer 2 of the Ascent, in a body of work built on one thesis: technology should increase human capability without taking human agency away. The problem family Atlas serves is learning poverty and unequal education. The Ascent, in order:

- Ground, the body: [ground](https://github.com/topsoilcommons/ground)
- Still, the mind at peace: [still](https://github.com/topsoilcommons/still)
- Atlas, learning (Layer 2): this repo.
- Cohort, belonging: [cohort](https://github.com/topsoilcommons/cohort), how people find each other and build together.
- Graph, shared truth: [graph](https://github.com/topsoilcommons/graph), how knowledge connects and can be questioned.
- Machine, autonomy: [machine](https://github.com/topsoilcommons/machine), how the machine itself learns, from first principles.
- Lumen, trust and meaning: [lumen](https://github.com/topsoilcommons/lumen), how all of it stays safe, cited, and human governed.

The north star metric for this act, counted honestly once learners are using it and dated when reported: **learners reaching mastery in the atlas**. No number is claimed yet. Ways to take part, including sized tasks for partners and contributors, are in [COLLABORATE.md](COLLABORATE.md) and [CONTRIBUTING.md](CONTRIBUTING.md).

## The proof

The tutor eval described in this section is an archived experiment. The tutor was dropped as a product surface on 2026-10-15, by direction; the harness and its published numbers are kept exactly as they ran.

This is a working product, not a mockup. The app builds cleanly (`npm run build` compiles the full JSX source to a single bundle, 473 KB in the current tree), it passes a build smoke test and a scoped lint, and the content library ships in the repo: 93 content modules, a manifest of 100 subjects, and Supabase seed data covering 279 topics and 4,706 curated resources.

The tutor is measured, not just described. The eval harness in `tools/tutor-eval/` grades answers produced over the atlas content for groundedness (do the facts the atlas states appear in the answer) and citation presence, and it runs in CI as a regression gate with per axis thresholds and a committed baseline. Current verified baseline results, from a run on 2026-10-17: groundedness 0.922, citation rate 1.0, correct source rate 1 across 17 questions drawn from the atlas itself, with every expected fact self checked against its source file before scoring. The full per question table is committed at `tools/tutor-eval/results/baseline-report.md`.
The score trend over time is committed at `tools/tutor-eval/results/trend.md`. The same harness runs against a live model in LLM mode (`npm run eval:tutor:llm`); that mode needs an API key and has not been run yet, so no LLM numbers are claimed anywhere in this repo.

Stated plainly, here is what is not finished:

- The test coverage is a build smoke test plus the eval harness. There is no unit test suite for the app.
- Lint covers the server functions, the shared library, and the tooling. The browser app sources share state through window globals by design, so they are excluded from lint until the app is migrated to modules; the exclusion is documented in `eslint.config.cjs`, not hidden.
- Accounts and payments are wired to Supabase and Stripe, but they need live project keys to run; the code is here, the configuration is yours to supply.

## Live demo

The live demo is at [topsoilcommons.github.io/atlas](https://topsoilcommons.github.io/atlas/).

An earlier version of this project is live at [american-desi.github.io/supergravity](https://american-desi.github.io/supergravity/). This repository is the canonical source going forward.

## Contribute, human or agent

- Start with a good first issue in this repo, sized to finish in hours.
- Take the Eval Challenge against this repo's published tutor scores, and attach your run.
- Adopt the tutor or the atlas in real use and report back what happened, good or bad.

The full protocol: [The Open Table](https://github.com/topsoilcommons/topsoilcommons/blob/main/OPEN_TABLE.md). Verified work is credited in the public [Ledger](https://github.com/topsoilcommons/topsoilcommons/blob/main/LEDGER.md).

### Start with a prompt

For an AI agent, copy and paste this prompt to run the Eval Challenge:

```text
You are an agent contributing to Atlas. Run the Eval Challenge end to end.
Start by reading AGENTS.md, README.md, and CONTRIBUTING.md in this repo.
Run npm install, then npm test, then npm run lint, then npm run eval:tutor.
Compare your results with the published baseline in tools/tutor-eval/results/baseline-report.md and in the Proof section of README.md. Those published baseline numbers are the scores to beat.
If you find an improvement, attach the run that proves it, submit one improvement per pull request, state that you are an agent, and name your operator.
```

For a human, copy and paste this prompt to file a failure report:

```text
Open a failure report issue in this repo and include the input you gave the tutor.
Say what happened, and say what should have happened instead.
```

Its record is filed in [the Index](https://topsoilcommons.github.io/index/).

## License

MIT. Copyright (c) 2026 Josh Thomas. See [LICENSE](LICENSE).
