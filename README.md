# claude-tutor

A Claude Code skill that teaches you a subject the way a good private tutor would. It first figures out what you already know, then teaches in small steps and quizzes you after each one.

The method and most of the rules come from [LearnHarness](https://github.com/amosblomqvist/learnharness), a desktop app by Amos Blomqvist. I wanted the same kind of teaching inside Claude Code without running a separate app, so I adapted its agent prompts into a skill. If you'd rather have a proper UI with a knowledge graph, use the original.

## How a course goes

You start by saying what you want to understand. "Understand transformers" could mean a dozen different things, so the first few questions are about the goal itself. After that it quizzes you on whatever the goal depends on (for backprop that's derivatives, the chain rule, matrix shapes and so on). It starts near the hard end of each topic and moves down when you miss, until it knows where your knowledge actually stops.

Then it draws a plan as a mermaid graph, with a few basic facts at the bottom and your goal at the top, and waits for you to OK it. Teaching follows the plan, but the plan gets redrawn whenever your answers show it guessed wrong about you.

Every step has the same shape. You're asked to guess what comes next; the tutor explains, starting from your guess; then a check question makes you use the idea on a case you haven't seen. If you miss the check, it goes back and fixes that step before moving on.

Practice happens in a separate session. The problems mix topics on purpose, and hints come one at a time: the first ones only point at something in the problem, and the last one shows the step. Anything you missed comes back later in a different form.

Build sessions are for code. You write something real, say an MLP with backprop done by hand, writing the tests first. The tutor reviews it against ub-mode (see below) one issue at a time. It won't rewrite your code for you.

With every answer you give a confidence percentage and a few lines of your reasoning. The reasoning is what it learns the most from. A wrong answer at 90% confidence gets a lot more attention than a wrong guess at 30%.

## Install

As a plugin, from inside Claude Code:

```
/plugin marketplace add Kratosyan7/claude-tutor
/plugin install tutor@claude-tutor
```

Or copy the skill folder by hand:

```bash
git clone https://github.com/Kratosyan7/claude-tutor
cp -r claude-tutor/plugins/tutor/skills/tutor ~/.claude/skills/tutor
```

### ub-mode

If you'll be writing code, install Uncle Bob's [ub-mode](https://github.com/unclebob/ub-mode) skill too:

```bash
git clone https://github.com/unclebob/ub-mode
mkdir -p ~/.claude/skills/ub-mode && cp ub-mode/SKILL.md ~/.claude/skills/ub-mode/
```

The tutor follows it in the code it writes (demos, model solutions) and uses it as the standard when it reviews yours. Without it there's a short set of TDD rules built in. I can't include ub-mode in this repo because it has no license. Its companion tools, [crapper](https://github.com/unclebob/crapper), [dryer](https://github.com/unclebob/dryer) and [mutator](https://github.com/unclebob/mutator), are optional; the tutor runs them if they're installed.

## Usage

```
/tutor probe I want to be able to derive backpropagation by hand
/tutor teach
/tutor build an MLP in numpy with hand-written backprop
/tutor practice
```

You don't have to name a phase. Saying "teach me how TCP congestion control works" is enough to start it. It answers in the language you write in.

## Where your progress goes

Everything is plain markdown in `~/learning/<subject>/`, so you can open and edit it yourself:

| File | Contents |
|---|---|
| `learner-map.md` | Your goal, and for each topic what you know solidly, where you start getting it wrong, and any misconceptions |
| `propositions.md` | What you've been taught, written as short claims and the chains of reasoning between them |
| `sessions/*.md` | One file per session with the plan, the questions, and your answers |
| `practice-log.md` | How each idea has held up in practice |

Each new session reads these files first and continues from where you left off.

## Files

```
.claude-plugin/marketplace.json
plugins/tutor/.claude-plugin/plugin.json
plugins/tutor/skills/tutor/SKILL.md          # core rules: tone, accuracy, questions, progress files
plugins/tutor/skills/tutor/references/
  probe.md                                    # finding what you already know
  teach.md                                    # planning and the guess/explain/check cycle
  practice.md                                 # practice sessions and hints
  code.md                                     # working with ub-mode, code review, build sessions
```

## License

AGPL-3.0-only, same as LearnHarness (see [LICENSE](LICENSE)). [NOTICE.md](NOTICE.md) lists the files this was adapted from and what was changed.
