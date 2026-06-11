# proof-review

Adversarial verification skill for bugfix PRs. Reproduces the reported symptom under production-shaped load, enumerates every root cause, and measures whether the PR closes each one. Output is a verdict-first report where every finding carries a number.

The unit of review is the symptom, not the diff.

## Install as a Copilot CLI skill

```bash
git clone https://github.com/AndreaGriffiths11/proof-review.git ~/code/proof-review
ln -s ~/code/proof-review ~/.copilot/m-skills/proof-review
```

Update later with `git -C ~/code/proof-review pull`.

## Contents

- `SKILL.md` — the workflow the agent follows
- `references/report-template.md` — the verdict-first report shape
- `scripts/loadharness.mjs` — zero-dependency Node 18+ load driver

## Use

In Copilot CLI, ask the agent to "proof-review this PR" or "verify the fix under load" and point it at the PR.

The harness is also usable standalone:

```bash
node scripts/loadharness.mjs run \
  --url http://localhost:3000/your-endpoint \
  --concurrency 4,8 --requests 200 --timeout 12000 \
  --json before.json

node scripts/loadharness.mjs compare before.json after.json
```

## Scope

Currently shaped for HTTP services with connection pools. CLIs, libraries, build tools, and data pipelines are out of scope until the workflow grows branches for them.

## License

MIT
