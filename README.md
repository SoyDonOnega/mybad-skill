# mybad

Agent skill `/mybad`: tries to prove you wrong on any claim, with data. Part of OneStack.

## What it does

Takes a claim, position or decision on any topic and does its honest best to refute it. It restates the claim in its strongest form and breaks it into checkable claims (empirical, causal, predictive, value). An isolated subagent then searches for disconfirming data first and supporting data second. The skill checks every figure (source, date, link, primary or secondary), redoes every calculation and returns a verdict per claim and overall: holds, weakened, wrong or unsettled, with confidence. It does not plan or implement anything.

## Usage

```text
/mybad Remote work lowers productivity in software teams
```

With no argument it takes the last claim you made in the conversation.

Output sections (in your language): Reviewer note → Verdict → Claim (strong version) → Claims table → Evidence (against, for, math, gaps) → What would change your mind → Sources.

## Install

From OneStack: `./sync-install.sh` — or copy this folder as `<skills dir>/mybad/`.

## Requirements

Web search and the ability to spawn an isolated subagent.

## Layout

- `SKILL.md` — the skill.
- `agents/mybad-refuter.md` — contract for the isolated refuter subagent.

## License

MIT — see `LICENSE`.
