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
