# claude-tutor

A tutor skill for [Claude Code](https://claude.com/claude-code). It doesn't just explain things. It finds where your understanding ends, plans a path from there to your goal, teaches one reasoning step at a time, and checks every step before building on it.

It's adapted from the agent prompts of [LearnHarness](https://github.com/amosblomqvist/learnharness), a desktop app built around the same method. You get its doctrine inside Claude Code, without the app.

## How it works

1. **Probe.** The tutor first pins down your goal. "Understand transformers" can mean ten things, and it asks until the goal is concrete. Then it binary-searches each topic the goal depends on to find what you reliably get right and where you start getting things wrong.
2. **Plan.** It draws a dependency map as a mermaid graph. At the bottom are a few facts you can accept as-is, and your goal sits at the top. You confirm the plan before any teaching starts, and the map changes when your answers show it was wrong about you.
3. **Teach.** Every step follows the same cycle: **predict → teach → check**. You try to guess the next step before it's explained. Each step is presented as something you could have discovered yourself, not as a decree. A check then makes you apply the idea, not recite it, and a missed check is repaired before anything is built on top of it.
4. **Practice.** Practice runs as separate sessions, with problems that interleave topics. Hints come one rung at a time (attention → pattern → candidate class → named idea → outline → worked step), and every miss is retested in a fresh form before the session ends.
5. **Build.** You apply what you learned by building something real in code, test-first, with you at the keyboard. The tutor reviews your code against [ub-mode](https://github.com/unclebob/ub-mode) one issue at a time, using the same hint ladder, and doesn't rewrite it for you.

Your answers carry a **confidence %** and your **thinking out loud**. The tutor treats your reasoning as its main signal, not just whether you got it right. A wrong answer given with high confidence is treated as a misconception to dig into.

## Install

### As a plugin (recommended)

In Claude Code:

```
/plugin marketplace add Kratosyan7/claude-tutor
/plugin install tutor@claude-tutor
```

### As a plain skill

Copy the skill folder into your user skills directory:

```bash
git clone https://github.com/Kratosyan7/claude-tutor
cp -r claude-tutor/plugins/tutor/skills/tutor ~/.claude/skills/tutor
```

### Recommended companion: ub-mode

For anything involving code, install Uncle Bob's [ub-mode](https://github.com/unclebob/ub-mode) skill next to this one:

```bash
git clone https://github.com/unclebob/ub-mode
mkdir -p ~/.claude/skills/ub-mode && cp ub-mode/SKILL.md ~/.claude/skills/ub-mode/
```

When ub-mode is installed, the tutor applies it to the code it writes for you, like demos and model solutions. It also uses ub-mode as the standard when it reviews your code and in build sessions. Without it, the tutor falls back to a short built-in set of TDD rules. ub-mode isn't bundled here because it ships without a license. Its quality-gate tools, [crapper](https://github.com/unclebob/crapper), [dryer](https://github.com/unclebob/dryer) and [mutator](https://github.com/unclebob/mutator), are optional and get used if they're installed.

## Use

```
/tutor probe I want to be able to derive backpropagation by hand
/tutor teach
/tutor build an MLP in numpy with hand-written backprop
/tutor practice
```

Or just say what you want to understand ("teach me how TCP congestion control works"), and the skill triggers on its own.

The tutor teaches in whatever language you write in.

## Your learning record

Everything is stored as plain markdown in `~/learning/<subject>/`:

| File | What's in it |
|---|---|
| `learner-map.md` | Your goal, plus each topic's floor, ceiling, misconceptions and fragile spots |
| `propositions.md` | What has been taught, as atomic claims and reasoning chains |
| `sessions/*.md` | One file per session: the plan, every question, your answers and confidence |
| `practice-log.md` | What each idea has demonstrated in practice: recall, discrimination, composition |

The next session picks up from this record instead of starting over. You can read it and edit it.

## Layout

```
.claude-plugin/marketplace.json
plugins/tutor/.claude-plugin/plugin.json
plugins/tutor/skills/tutor/SKILL.md          # core: philosophy, voice, accuracy, questions, state
plugins/tutor/skills/tutor/references/
  probe.md                                    # measuring the edge
  teach.md                                    # method, plan map, predict → teach → check, demos
  practice.md                                 # retrieval practice, hint ladder, retests
  code.md                                     # ensemble with ub-mode: tutor code, code review, build sessions
```

## License

[AGPL-3.0-only](LICENSE). This is a derivative of LearnHarness, see [NOTICE.md](NOTICE.md).
