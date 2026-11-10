# Notice

This project is a derivative adaptation of the agent system prompts from
[LearnHarness](https://github.com/amosblomqvist/learnharness) by Amos Blomqvist,
licensed under the GNU Affero General Public License v3.0 only.

Source files adapted:

- `src/agent/system-prompt.md`
- `src/agent/prompts/teacher/*.md`
- `src/agent/prompts/prober/*.md`
- `src/agent/prompts/practice/*.md`
- `src/agent/prompts/shared/*.md`

Changes made:

- Condensed and merged into one Claude Code skill (`tutor`) with three phase references (probe, teach, practice).
- Replaced the app-specific tools (quiz/explain, `plan_init`, `probe_done`, `problem`/`conclude`,
  research/pdf/demo/visual jobs, knowledge-graph readers) with Claude Code equivalents:
  `AskUserQuestion`, mermaid in chat, plain-markdown learner state in `~/learning/<subject>/`,
  web search and subagents, HTML / script / notebook demos.
- Made the pronouns gender-neutral and generalized the doctrine beyond a single subject.
- Added examples.

This project as a whole is distributed under the same license; see [LICENSE](LICENSE).

## ub-mode

`references/code.md` is original to this project. It describes how the tutor works with
[ub-mode](https://github.com/unclebob/ub-mode) by Robert C. Martin, a separate skill that this repository
neither includes nor redistributes. At the time of writing ub-mode is published without a license.
Install it separately from its repository.

## socratic-tutor

Parts of `SKILL.md` and of `references/teach.md`, `references/probe.md` and `references/practice.md` are adapted
from the `socratic-tutor` skill in [janestreet/agent_skills](https://github.com/janestreet/agent_skills)
(`socratic-tutor/SKILL.md`): the intent guard, the 0–5 level scale and its promotion rules, the progress map,
repairing a wrong answer with narrower questions, pushing back on right answers, unannounced review,
the final assessment, and the learner commands. They were rewritten to fit this skill's file-based state and phases.
That skill is distributed under the following license:

```
The MIT License

Copyright (c) 2026 Jane Street Group, LLC <opensource-contacts@janestreet.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
