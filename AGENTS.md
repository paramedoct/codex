# global agent guide

## working style

- keep the main command flow easy to read
- prefer minimal mvp implementations over broad abstractions
- make output readable for operators first
- design changes so they can later support automated checks and recorded output

## shell compatibility

- keep shell code compatible with `bash`
- avoid bash 4+ features such as `mapfile`, associative arrays, and `readarray`
- prefer simple loops and explicit data collection over version-specific helpers

## shell format

- use `#!/usr/bin/env bash` for executable bash entrypoints
- order entrypoints as shebang, `set -euo pipefail`, startup variables, one blank
  line, then helpers or sourced modules
- derive a repository root with
  `ROOT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"`
- load multiple modules with `source_modules \` and one path per continued line
- declare `local` variables at the top of a function
- keep function bodies compact without blank lines between adjacent statements
- keep exactly one blank line between top-level function definitions
- keep one blank line before the final `main "$@"` call
- place inline `shellcheck` suppressions immediately above the affected command

## documentation

- keep durable development instructions in this `AGENTS.md`
- do not add a `docs/` directory
- do not modify or commit `README.md` unless the user explicitly asks

## naming and output

- keep user-facing log messages lowercase except for standard acronyms
- prefer readability over clever formatting
- keep lines within 88 characters when practical
- prefer short names when their meaning is clear

## commits

- make small, meaningful commits with one logical change each
- use lowercase google-style titles such as `add: ...`, `fix: ...`, or
  `refactor: ...`
- prefer a title without a body unless more detail is necessary
- split or narrow a commit whose title feels broad
- amend the last commit before push when only its message needs correction

## decision rule

when choosing between abstraction and momentum, prefer the version that keeps today's
command flow readable with the fewest moving parts.
