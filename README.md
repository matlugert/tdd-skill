# /tdd

One failing test at a time. No exceptions, no shortcuts.

A Claude Code command that enforces strict test-driven development: RED (write a failing test) → GREEN (minimal code to pass) → REFACTOR (clean up) → REPEAT. Every cycle is visible — you see the failing output, the passing output, and what changed.

```
/tdd add user authentication    → plans behaviors, then builds them test-first
/tdd fix the cart total bug     → writes a test that reproduces the bug, then fixes it
/tdd                            → asks what to build
```

## What it does

1. **Plans first.** Agrees on behaviors and public interface with you before writing anything.
2. **Detects your stack.** Reads your project's package manifest and uses whatever test runner is already there.
3. **One cycle at a time.** Writes one test, shows you it fails, writes minimal code, shows you it passes. Then asks what's next.
4. **Shows proof.** Every RED and GREEN step includes actual test output. No "trust me, it works."

## What it won't do

- Write production code before a failing test exists
- Write more code than needed to pass the current test
- Mock your own modules (only system boundaries)
- Skip showing test output
- Batch multiple tests before implementing

## Install

```bash
cp commands/tdd.md ~/.claude/commands/
```

```powershell
# Windows
Copy-Item commands\tdd.md "$env:USERPROFILE\.claude\commands\"
```

## License

MIT
