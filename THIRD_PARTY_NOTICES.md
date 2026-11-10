# Third-party notices

## Claude Code Game Studios

The game-development framework at the root of this repository is a copy of
[Claude Code Game Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) by
Donchitos, used under the MIT License reproduced at the end of this file.

- **Version:** 1.3.0, upstream commit `abc0de79d6ceb0b5d7aa693945849b3937afbe6a`
  (2026-11-09), copied on 2026-11-10.
- **Copied paths:** `.claude/`, `CLAUDE.md`, `project.yaml`, `UPGRADING.md`, `.gitignore`,
  `.gitattributes`, `.worktreeinclude`, `docs/`, `studio-tests/`, and the starter files under
  `design/`, `production/` and `src/`.
- **Not copied:** the upstream `README.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, `SECURITY.md`,
  `LICENSE` (its text is below) and `.github/`. They describe the upstream project rather
  than this repository.
- **Changed here:** as imported, every file's content is identical to upstream. The one
  difference is the executable bit, set on each `.sh` file in `.claude/hooks/` and
  `.claude/scripts/` so that agents can run them directly (see `AGENTS.md`).
- **Added beside it, not part of the framework:** `AGENTS.md`, `tools/chrome-as-root` and
  this file.

### Upgrading

Follow `UPGRADING.md`. This repository shares no git history with the template, so use its
Strategy A2 (selective checkout). A2 replaces `.claude/` wholesale, which resets the
executable bits. Restore them before committing:

```bash
chmod +x .claude/hooks/*.sh .claude/scripts/*.sh
```

Then update the version and commit recorded above.

### License

```text
MIT License

Copyright (c) 2026 Donchitos

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
