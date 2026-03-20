# OpenClaw Adaptation Notes

This branch adds an OpenClaw-oriented adaptation layer for selected PUA skills.

## Goals

- Keep the original multi-platform repo intact enough to remain understandable
- Make the most reusable skills easier to use in OpenClaw
- Remove assumptions that only make sense in Claude/Codex/Cursor-specific flows
- Add missing local `references/` directories where skills previously depended on `skills/pua/references/*`

## Included in this branch

### Adapted for OpenClaw
- `skills/pua`
- `skills/p7`
- `skills/p9`
- `skills/p10`
- `skills/sb-leader`

### What changed
- Rewrote descriptions to mention OpenClaw-friendly triggers and use cases
- Added OpenClaw-specific wording around:
  - `sessions_spawn`
  - `sessions_send`
  - `subagents`
  - persistent-agent and subagent workflows
- Copied required reference files into each skill's own `references/` folder so they are self-contained
- Reduced reliance on platform-specific slash-command assumptions

## Not adapted here
- `hooks/` (Claude-style hooks; better rewritten natively for OpenClaw)
- `skills/pro` (too tightly coupled to remote platform logic, `~/.pua/`, feedback upload, registration, etc.)

## Rationale

OpenClaw benefits most from prompt/workflow skills that are:
- local-first
- self-contained
- tool-mapped to OpenClaw runtime primitives
- not dependent on external SaaS state

This branch is meant to be a practical OpenClaw-ready extraction step, not a full platform rewrite.
