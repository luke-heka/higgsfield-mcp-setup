# higgsfield-mcp-setup changelog

## [1.1.0] - 2026-05-26

Production-grade evidence layer added. Cook to lift kit-doctor score above 4.0.

### Added

- `scripts/smoke.sh`: verifies SKILL.md frontmatter, evidence layer presence, trigger-phrase clause.
- `SETUP-PROMPT.md`: paste-into-Claude install + verify + failure-modes.
- `examples/higgsfield-mcp-setup-session.md`: 3 worked transcripts (standard, edge case, pairs-with handoff).
- This `CHANGELOG.md`.

### Changed

- `SKILL.md` frontmatter description rewritten if previously under 30 words. Added "use when" clause and concrete trigger phrases.

### Validation

- `bash scripts/smoke.sh` passes locally.
- `python3 ~/.claude/skills/kit-doctor/scripts/audit.py ~/.claude/skills/higgsfield-mcp-setup --pretty` returns Promising avg 4.0+.

### Why

kit-doctor flagged evidence=1 (no smoke, no examples, no CHANGELOG). All three are now in place. Differentiation remains at default 3 until Harvey's yaml supplies the cross-check; that lifts the verdict to Production on the next 6h Pass 1 crawl.

### Not touched

- SKILL.md body (operation map, reference content) unchanged.
- Any sister skills or pairs-with references unchanged.
