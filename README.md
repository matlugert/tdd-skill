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

**1. Add the command:**

```bash
cp commands/tdd.md ~/.claude/commands/
```

```powershell
# Windows
Copy-Item commands\tdd.md "$env:USERPROFILE\.claude\commands\"
```

**2. Add TDD rules to your CLAUDE.md:**

The `/tdd` command handles the cycle when you invoke it. But to make TDD your default way of working — even without the command — add these rules to your project or global `CLAUDE.md`:

```markdown
## Testing (TDD Workflow)

When building new features or fixing bugs:
0. **Plan** — Confirm with user which behaviors to test, prioritize them, and design the public interface.
1. **Write test first** (RED) — test MUST fail before implementation exists. Name it like a spec: `should <expected behavior> when <condition>`.
2. **Run the test** to verify it fails. Include output in response.
3. **Write minimal implementation** (GREEN) — just enough to pass.
4. **Run test again** to verify it passes. Include output in response.
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
- Mock only at system boundaries (external APIs, DB, time, filesystem). Never mock your own modules.
- Always include test output in your response.
- Coverage target: 80%+ lines and branches.
- Run the full test suite after completing a feature, not just the new test.

Error classification:
- **Code error** → keep iterating
- **Access error** (permissions, auth, rate limit) → stop, report, wait
- **Environment error** (missing binary, wrong runtime) → stop, report, wait
```

With both the command and the CLAUDE.md rules, Claude works test-first whether you type `/tdd` or just describe a feature.

## License

MIT
