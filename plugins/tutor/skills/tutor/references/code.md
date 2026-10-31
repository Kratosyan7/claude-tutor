# Code — the ensemble with ub-mode

Load this reference whenever code enters a session: code you write (demos, verification scripts, model solutions), code the learner writes, or a **build** session.

## The partner skill

[ub-mode](https://github.com/unclebob/ub-mode) is a separate skill of code-discipline rules: *First Make it Work → Then Make it Right → Practice* (TDD, data shape first, boundary and type discipline, root-cause fixes, behavior-level tests, refactoring under pinned behavior, small commits), backed by deterministic quality gates — [crapper](https://github.com/unclebob/crapper) (CRAP < 10), [dryer](https://github.com/unclebob/dryer) (duplication < 0.8), [mutator](https://github.com/unclebob/mutator) (mutation testing).

It is **not bundled** with this plugin (it ships without a license). Check whether it's installed: a `ub-mode` skill in the available skill list, or `~/.claude/skills/ub-mode/SKILL.md`. If installed, read its SKILL.md once when code first enters the session and apply it as described below. If not, use the short fallback at the end and mention once that installing ub-mode gives the full rule set.

**Division of authority.** The tutor doctrine owns *how the learner learns*; ub-mode owns *what good code is*. When they pull apart inside a learning session, the learner's understanding wins — e.g. ub-mode says ship the smallest edit, but a learner may need to write the naive version first to feel why the better design exists (Principle ii: make it feel discovered). When the learner is doing real work in their own codebase and not studying, ub-mode governs and the tutor stays out of the way.

## 1. Code you write

Demos, verification scripts, reference implementations, practice model solutions.

- Apply ub-mode at the scale of the artifact. Its *Make it Work* and *Make it Right* rules apply to anything you show; the heavy practice rules (worktree cleanup, push to main, CRAP/mutation gates) apply only when the code lives in a real project, not to a 40-line demo.
- Non-negotiables: it runs (tested before shown); any test checks behavior, not implementation; one decision lives in one place; the data shape is right before the logic.
- Code shown to the learner is teaching material: it models the discipline, and it uses nothing beyond what the step has taught — no clever tricks the learner would have to take on faith.

## 2. Code the learner writes

The tutor method governs; ub-mode supplies the standard.

- **Never rewrite their code wholesale.** A review locates the *one* violation that matters most right now and works on it; the next one waits.
- Use the hint ladder (practice.md §VI): R0 "look at where this function reads its input" → R1 "the same check happens in three places" → R2 "this is a boundary-discipline issue" → R3 name the ub-mode rule → R4 outline the change → R5 show it. One rung per request; the learner types the fix.
- A ub-mode principle the learner hasn't met is a proposition to teach, by the method: motivate it by showing the failure it prevents (a test that still passes when every function returns nothing; a crash fixed by a guard that hides it; a second run after a half-finished crash leaving a different state). Then check it with an applied question.
- Record taught principles in `~/learning/software-engineering/propositions.md` (or the project's own subject), with the session date.

## 3. Build sessions

A **build** session applies a subject by making something real — an MLP with hand-written backprop, a tokenizer, a small interpreter. It joins the arc after teaching: teach → build → practice.

1. **Agree the end state you can check** (`AskUserQuestion` if there's a real choice): what runs, what it outputs, which test proves it.
2. **Split into verifiable units**; show the units as a short mermaid map, like a plan map.
3. **Per unit, test-first, learner at the keyboard:**
   - The learner predicts and writes the failing test first, and states why it should fail.
   - They run it and confirm it fails *for that reason* (a wrong failure reason is a check miss — diagnose before going on).
   - They make the smallest change that passes; you check it with the review rules above.
4. **Build the lever when it's logistics, not material.** A test harness, a numerical gradient checker, a plotting helper — you may write these (the system absorbs logistics). Anything that *is* the subject being learned, the learner writes. When the subject is building levers itself, do one unit by hand together, then let them write the tool.
5. **Quality gates at unit end**, if crapper/dryer/mutator are installed and support the language: run them; each surviving mutant becomes a practice problem — "which test would kill this?" — not something you fix for them.
6. **Commits**: if the project is a git repo and the learner wants commits, one per verified unit, saying why, what changed, and how it was proved.

At session end, log the build in the session file: units done, what each test proved, principles that came up, misses and their classification.

## Fallback when ub-mode isn't installed

Write the failing test first and watch it fail for the expected reason; make the smallest change that passes; test behavior the way a caller sees it; validate data where it enters and trust it inside; fix the root cause, not the symptom; refactor only with behavior pinned by tests; one decision in one place.
