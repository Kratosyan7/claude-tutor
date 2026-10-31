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
