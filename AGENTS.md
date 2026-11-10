# Agent instructions

## Game work goes through Claude Code Game Studios

[Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) 1.3.0 is
installed at the root of this repository: 78 skills and 49 studio agents under `.claude/`,
with `CLAUDE.md` as its master configuration. The repository owner's standing instruction is
to **use it for every task that creates, changes, grows, tests or ships a game**. Do not
build a game by hand outside its skills, even when the request names no skill, unless the
request itself says to work without the framework.

Read `CLAUDE.md` first, then read and follow the skill the request calls for:

| The request | Skill |
|---|---|
| "Make me a game", a game idea or mechanic to try, a change to a game built here | `.claude/skills/prototype/SKILL.md` |
| No idea yet, wants concepts | `.claude/skills/brainstorm/SKILL.md` |
| Unsure where to begin | `.claude/skills/start/SKILL.md` |
| "What next?", stuck, or nothing above fits | `.claude/skills/next-step/SKILL.md` |
| `/name …` typed by the user | `.claude/skills/name/SKILL.md`; the rest of the line is its arguments |

A skill names the further files it needs (`references/`, `.claude/docs/`, `.claude/genres/`).
Read them when it says to, not before.

## What differs from Claude Code

The skills are written for Claude Code. On this platform:

- **Run the framework's scripts directly, never through `bash`.** The workspace policy
  refuses `bash <file>` and scripts fed on standard input. Every `.sh` file in
  `.claude/scripts/` and `.claude/hooks/` is committed executable, so where a skill says
  `bash .claude/scripts/page-shot.sh …`, run `.claude/scripts/page-shot.sh …`.
- **Skill preambles.** A line of the form `` !`command` `` near the top of a `SKILL.md` is a
  command Claude Code runs before the skill loads. Run it yourself from the repository root
  and read its output as part of the skill. `${CLAUDE_SKILL_DIR}` is the skill's own folder,
  so `bash "${CLAUDE_SKILL_DIR}/../../hooks/yaml-helper.sh" resolve_config --keys a,b`
  becomes `.claude/hooks/yaml-helper.sh resolve_config --keys a,b`. `$ARGUMENTS` is what the
  user typed after the skill's name, and `$CLAUDE_PROJECT_DIR` is the repository root.
- **`CLAUDE.md` imports.** Its `@path` lines are files Claude Code loads along with it. Read
  them as part of `CLAUDE.md`.
- **Browser checks.** Agents run as root here, and Chrome will not start as root without
  `--no-sandbox`, which the framework does not pass. Put
  `PAGE_SHOT_BROWSER="$PWD/tools/chrome-as-root"` in front of every command that opens a
  browser: `page-shot.sh`, `one-shot-run.sh`, `one-shot-check.sh`, `test-run.sh`, and a grown
  project's Playwright tests, which take their browser from `page-shot.sh --which`. A
  `not_assessed` row saying the browser stopped without a picture means it was left off.
- **Questions.** `AskUserQuestion` is this platform's question tool (`ask_user_question`).
  An unanswered question is not an answer: wait for it, as the skills say.
- **Studio agents.** `subagent_type: <name>` means the agent defined in
  `.claude/agents/<name>.md`. Start a general-purpose subagent, tell it to read that file and
  work as that agent, and put everything else it needs in its prompt, because it cannot ask
  questions. The file's frontmatter (`tools`, `model`, `maxTurns`) is not enforced here; its
  body is the brief. A skill started "with the Skill tool" is read the same way as any
  other: open its `SKILL.md`.
- **Hooks.** `.claude/settings.json` belongs to Claude Code: do not count on its hooks or
  permission rules running here. `.claude/hooks/session-start.sh` prints the session summary
  on demand.
- **Git.** The framework's commits and tags go on this thread's branch, never on the default
  branch, and pushing and pull requests follow the platform's rules. Tags stay in this
  workspace: a new thread starts without them.
- **Handing a game over.** The person cannot double-click a file in this sandbox. Where a
  skill tells them to open the game, share it through the platform's Preview (its
  `preview-workflow` skill says how) together with the screenshots the checks took.

Where the framework and the platform disagree, the platform's rules win. The rest of the
framework stands.

Where the framework came from, its licence and how to upgrade it: `THIRD_PARTY_NOTICES.md`.
