# /tdd

One failing test at a time. No exceptions, no shortcuts.

A Claude Code command that guides strict test-driven development: RED (write a failing test) → GREEN (minimal code to pass) → REFACTOR (clean up) → REPEAT. Every cycle is visible — you see the actual command, exit code, and test output.

```
/tdd add user authentication    → plans behaviors, then builds them test-first
/tdd fix the cart total bug     → writes a test that reproduces the bug, then fixes it
/tdd                            → asks what to build
```

## What it does

1. **Plans first.** Agrees on behaviors and public interface with you before writing anything.
2. **Detects your stack.** Reads your project's package manifest and uses whatever test runner is already there. Handles monorepos.
3. **Establishes baseline.** Records existing suite state before starting so pre-existing failures don't confuse RED/GREEN signals.
4. **One cycle at a time.** Writes one test, runs it targeted (not full suite) to confirm failure, writes minimal code, runs full suite to confirm nothing regressed. Then asks what's next.
5. **Shows proof.** Every step includes the actual command, exit code, and relevant output. Not summaries.

## What it won't do

- Write production code before a failing test exists
- Write more code than needed to pass the current test
- Skip showing real test execution output
- Batch multiple tests before implementing

## Install

**1. Add the command** (global or project-local):

```bash
# Global — available in all projects
cp commands/tdd.md ~/.claude/commands/

# Project-local — available in one project
cp commands/tdd.md .claude/commands/
```

```powershell
# Windows — global
Copy-Item commands\tdd.md "$env:USERPROFILE\.claude\commands\"

# Windows — project-local
Copy-Item commands\tdd.md ".claude\commands\"
```

**2. Make TDD the default** (recommended):

The `/tdd` command handles the cycle when you invoke it. To make TDD the default for *all* coding — even without the command — add these rules to your project or global `CLAUDE.md`:

<details>
<summary>Suggested CLAUDE.md rules (click to expand)</summary>

```markdown
## Testing (TDD Workflow)

When building new features or fixing bugs:
0. **Plan** — Confirm which behaviors to test, prioritize them, and design the public interface.
1. **Write test first** (RED) — test MUST fail before implementation exists. Name it like a spec: `should <expected behavior> when <condition>`.
2. **Run the new test** to verify it fails. Show the command and output.
3. **Write minimal implementation** (GREEN) — just enough to pass.
4. **Run the full suite** to verify nothing regressed. Show the command and output.
5. **Refactor** if needed, re-run tests to confirm nothing broke.

**One RED-GREEN cycle at a time.** Never batch multiple tests before implementing. Start with the simplest happy path, then progress to edge cases and error scenarios. After each cycle, ask what behavior to add next.

Per-cycle checklist:
- [ ] Test describes behavior, not implementation
- [ ] Test uses public interface only
- [ ] Test would survive an internal refactor
- [ ] Code is minimal for this test
- [ ] No speculative features added

Rules:
- NEVER write implementation before a failing test exists.
- Tests come from the spec/requirements, not from the implementation.
- Mock at system boundaries (external APIs, DB, time, filesystem). Avoid mocking your own modules.
- Always show the actual command, exit code, and relevant output.
- Run the full test suite after completing a feature, not just the new test.

Error classification:
- **Code error** → keep iterating
- **Access error** (permissions, auth, rate limit) → stop, report, wait
- **Environment error** (missing binary, wrong runtime) → stop, report, wait
```

</details>

With both the command and the CLAUDE.md rules, Claude works test-first whether you type `/tdd` or just describe a feature.

## License

MIT
