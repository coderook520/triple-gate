# Triple Gate

Quality enforcement for Claude Code. 6 AI cops review every build before it ships.

## what it does

When you type `/police`, Claude reviews its own work through 4 phases:

1. **Self-Drafts** -- writes 3 drafts, each one fixing weakness categories from the last
2. **Security + Quality** -- 2 Opus agents review in parallel (credential leaks, injection, error handling, edge cases)
3. **Integration + Failure Modes** -- 2 more Opus agents check for dependency conflicts, race conditions, what breaks when things go wrong
4. **Final Audit** -- 2 Opus agents verify the implementation matches the plan and check long-term maintainability

Nothing ships until all 6 cops pass. If they reject, Claude fixes and resubmits. Loop until clean.

## install

```bash
mkdir -p ~/.claude/skills/police
cp SKILL.md ~/.claude/skills/police/SKILL.md
```

That's it. Open Claude Code, type `/police`, and it activates on your next build.

## what it catches

- Credential leaks in code
- SQL injection, XSS, command injection
- Missing error handling
- Race conditions
- Broken imports and dependency issues
- Silent failures
- Config conflicts
- Technical debt
- Deviations from the approved plan

## requirements

- Claude Code with Opus model access (cops are Opus agents)
- That's it for basic use

## advanced setup (optional)

The SKILL.md references optional hardening features (GPG emergency override, append-only learning log, credential scrubber, budget gates). These require additional setup described in the file. The core review system works without them.

## license

MIT
