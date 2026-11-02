---
name: mybad
description: >-
  Tries to prove the user wrong on any claim, position or decision, on any topic: states
  its strongest version, breaks it into checkable claims, has an isolated refuter hunt
  for data that contradicts each one, checks the numbers and returns a verdict per claim
  with confidence. Built on data, not opinion. Use when the user runs /mybad with a
  claim, or asks to be proven wrong.
license: MIT
compatibility: Needs web search and the ability to spawn an isolated subagent.
argument-hint: "[claim, position or decision]"
disable-model-invocation: true
---

# Mybad

Takes what the user believes and does its honest best to prove it wrong, with data. Works on any topic: business, product, technology, science, economics, personal decisions. It does not agree by default and does not soften a clear result: if the claim survives the attack, it says so; if it falls, it says so. It does not plan or implement anything.

Paths in this file are relative to the skill root (the folder that contains this SKILL.md).

## When invoked

1. **Fix the claim.** Argument → that claim. No argument → the last claim, position or decision the user stated in the conversation; quote it. If none is clear, ask once.
2. **Steelman.** Restate the claim in its strongest, most precise form: scope, time frame, population, what "true" would mean in numbers. Attack this version, never a weaker one.
3. **Decompose.** Break it into 2–6 claims, each tagged:
   - `empirical` — a fact or magnitude that data can check;
   - `causal` — X causes or drives Y;
   - `predictive` — something will happen;
   - `value` — a judgment or preference that data informs but cannot settle.
   For each, write the falsifier: the data that would prove it wrong.
4. **Refute.** Spawn an isolated subagent with only `agents/mybad-refuter.md`, the steelman and the claim list. It searches for disconfirming data first, then for supporting data, and returns evidence per claim.
5. **Check the data.** For every number the refuter returns: it has a source, a date and a link; the source is primary or close to it (official statistics, datasets, filings, peer-reviewed studies, original reports) over press or blogs; units and definitions match the claim. Redo every calculation (ratios, growth, base rates, orders of magnitude) and show it. Drop or flag what fails.
6. **Verdict.** Per claim and overall: `holds` · `weakened` · `wrong` · `unsettled` (data missing or contradictory). Confidence high / medium / low, with the reason. For `value` claims: say which part the data moved and which part stays a choice.
7. Produce the output and stop.

## Rules

- Data over argument. Every factual statement carries a number or a fact, its source, its date and a link. No source → write "sin dato" / "no data" and lower the confidence; never fill the gap from memory.
- Never invent figures, studies, sources or quotes. Keep verified fact, calculation and inference apart, and label inference.
- Look for disconfirming evidence first: base rates, counterexamples, alternative explanations, confounders, selection and survivorship bias, reverse causation, small samples, outdated data, cherry-picked periods.
- Prefer the most recent data and say how old each figure is.
- Show the math. A calculation the reader cannot redo does not count.
- If the claim holds, say it holds. No invented objections to look tough; no hedging on a clear result.
- No role-play and no tone of rebuttal for its own sake: the target is the claim, not the user.
- Answer in the user's language.

## Output

```markdown
> Nota de revisión — búsquedas (fecha, número) · fuentes leídas · datos descartados en la verificación · límites

## Veredicto
**<holds / weakened / wrong / unsettled>** — confianza <alta / media / baja>. <One or two sentences: why.>

## Tesis (versión fuerte)
<steelman>

## Afirmaciones
| # | Afirmación | Tipo | Veredicto | Confianza | Dato clave |

## Evidencia
### 1. <claim>
- En contra: <figure> — <source>, <date> · <link>
- A favor: <figure> — <source>, <date> · <link>
- Cálculo: <the math>
- Sesgos o lagunas: …

## Qué te haría cambiar de opinión
- <the data point that would flip the verdict, and where to get it>

## Fuentes
- …
```

Translate headings into the user's language when not Spanish (Reviewer note · Verdict · Claim (strong version) · Claims · Evidence · What would change your mind · Sources).

## Resources

- `agents/mybad-refuter.md` — contract for the isolated refuter of step 4.

## Harness notes

- Isolated subagent: Claude Code `Agent` tool with `subagent_type: "general-purpose"`; other harnesses: their subagent or task tool. Without subagents, run the refuter as a separate pass that sees only its contract and inputs.
- Keep `agents/mybad-refuter.md` in this folder; never copy it into a harness agents folder (it would show in the slash menu).
