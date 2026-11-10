# Probe — measure before teaching

Two measurements, nothing else: **what they need to learn** (the goal) and **what they already know** (a precise map of their understanding). The whole lesson is planned from this map, so it must be precise. You never teach in this phase.

Strictly one question at a time: ask, wait, choose the next question from what the answer told you.

## 1. Read the persistent map

Read `~/learning/<subject>/learner-map.md` and `propositions.md`. A strand already held solid needs no re-probing; a strand marked fragile or misconceived does. If the files don't exist, just probe.

## 2. Make the goal concrete — `AskUserQuestion`

"I want to understand transformers" can mean ten different things (use the HF API? derive attention? read the paper? implement from scratch? know why it beat RNNs?). Which one changes everything. Interrogate until the goal is concrete and testable — what will they be able to do or explain at the end? If they don't know the terrain, record that the goal starts with orientation — don't draw the map for them here.

## 3. Reason out the strands

From the goal: what will the lesson depend on? Where would teaching start, and what must it build on? Each dependency is a **strand**, bounded by relevance only. E.g. for backpropagation: derivatives and the chain rule, multivariable chain rule, matrix shapes, what a forward pass and a loss are, gradient descent. For a Rust ownership goal: stack vs heap, references, lifetimes, move semantics.

## 4. Binary-search every strand

The edge of a strand is bracketed by a **floor** (something they reliably get right) and a **ceiling** (something they get wrong or don't know). Each next question is chosen from the evidence — verdict, confidence and thinking together:

- **Enter near the top, not the bottom.** An adult reaching for advanced material almost always holds school basics — open near the hardest thing the goal needs and let a miss walk you down. A "warm-up" at textbook basics wastes a question that could have moved an edge.
- **Strands inform each other.** A strand crushed at height means neighbors likely start high too — never open below what's already demonstrated.
- Right + confident → jump difficulty up sharply (bigger jump, fewer questions).
- Right but hesitant (low confidence, thin thinking) → fragile: step up gently and characterize the shakiness.
- Wrong → ceiling drops; narrow back to pin exactly where it sits.
- A miss is one coordinate, not a verdict — slip, gap and misconception look identical. Probe around it. **Misconceptions matter most**: dig into their extent before moving on.
- A strand that never breaks isn't done — escalate until it does.

Every question must move an edge: no filler, no re-asking what the last answer showed, never descending into bracketed territory. Questions saved are resolution spent on the nuanced ones that actually locate the edge.

Use the question mechanics and option craft from SKILL.md. Prefer applied questions ("what shape does `X @ W.T` have if…", "what happens to the loss if…") over definitions.

## 5. Conclude

When every strand is bracketed and the goal is concrete, write the result to `~/learning/<subject>/learner-map.md` (update in place; date it) — one entry per strand:

```markdown
### <strand name>  (probed YYYY-MM-DD)
- Level: <0–5, see SKILL.md; the probe can place a strand up to 4, never 5>
- Floor: <what they reliably hold, with the evidence>
- Ceiling: <where it breaks, with the evidence>
- Misconceptions: <specific wrong models + their own words>
- Fragile: <right but shaky>
- Build from: <the highest solid point teaching should start at>
```

Also record the concrete goal at the top of the file. Show the learner the progress map (SKILL.md) with the starting levels, one closing sentence, end the turn. Next session: teach (load teach.md).

## Grounding

If they reference their own course/notes/notebook, read it directly. Research sparingly — probing is measurement, not exploration.
