# Installing PUA Skill for Codex

Force AI to exhaust every possible solution before giving up. Installs via native skill discovery (`~/.codex/skills/`).

Codex-ready skills in this repo:
- `pua`
- `p7`
- `p9`
- `p10`
- `pro`
- `yes`
- `pua-en`
- `pua-ja`

Not supported in Codex:
- `loop` / `pua:loop`
- Claude-only hook workflows (`PreCompact`, `SessionStart`, `Stop`)

## Prerequisites

- Git

## Installation

### macOS / Linux

```bash
# 1. Clone the repo
git clone https://github.com/tanweai/pua.git ~/.codex/pua

# 2. Create skill symlinks (enables auto-discovery)
mkdir -p ~/.codex/skills
for skill in pua p7 p9 p10 pro yes pua-en pua-ja; do
  ln -s ~/.codex/pua/codex/$skill ~/.codex/skills/$skill
done

# 3. Install /prompts:pua router
mkdir -p ~/.codex/prompts
ln -s ~/.codex/pua/codex/prompts/pua.md ~/.codex/prompts/pua.md

# 4. Restart Codex
```

### Windows (PowerShell)

```powershell
# 1. Clone the repo
git clone https://github.com/tanweai/pua.git "$env:USERPROFILE\.codex\pua"

# 2. Create skill junctions (enables auto-discovery)
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills"
$skills = "pua","p7","p9","p10","pro","yes","pua-en","pua-ja"
foreach ($skill in $skills) {
  cmd /c mklink /J "$env:USERPROFILE\.codex\skills\$skill" "$env:USERPROFILE\.codex\pua\codex\$skill"
}

# 3. Install /prompts:pua router
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\prompts"
cmd /c mklink "$env:USERPROFILE\.codex\prompts\pua.md" "$env:USERPROFILE\.codex\pua\codex\prompts\pua.md"

# 4. Restart Codex
```

## Verify

Type `$pua` in a Codex conversation. If the skill is loaded, you'll see it activate.

Other direct calls:
- `$p7`
- `$p9`
- `$p10`
- `$pro`
- `$yes`
- `$pua-en`
- `$pua-ja`

Or check directly:
```bash
# macOS / Linux
ls ~/.codex/skills/pua/SKILL.md
ls ~/.codex/skills/p7/SKILL.md

# Windows PowerShell
Test-Path "$env:USERPROFILE\.codex\skills\pua\SKILL.md"
Test-Path "$env:USERPROFILE\.codex\skills\p7\SKILL.md"
```

## Trigger Methods

| Method | Command | Requires |
|--------|---------|----------|
| Auto trigger | No action needed, matches by description | SKILL.md |
| Direct call | Type `$pua` / `$p7` / `$p9` / `$p10` / `$pro` / `$yes` | SKILL.md |
| Manual prompt router | Type `/prompts:pua` or `/prompts:pua p9` | SKILL.md + prompts/pua.md |

## Supported Codex Skills

| Skill | Path |
|-------|------|
| Chinese core | `codex/pua/SKILL.md` |
| P7 | `codex/p7/SKILL.md` |
| P9 | `codex/p9/SKILL.md` |
| P10 | `codex/p10/SKILL.md` |
| Pro | `codex/pro/SKILL.md` |
| Yes | `codex/yes/SKILL.md` |
| English (PIP) | `codex/pua-en/SKILL.md` |
| Japanese | `codex/pua-ja/SKILL.md` |

`loop` is intentionally excluded here because the current implementation depends on Claude hook machinery and `.claude` state files.

## Update

```bash
cd ~/.codex/pua
git pull
```

The symlink/junction automatically picks up the latest version — no reinstall needed.

## Uninstall

### macOS / Linux

```bash
rm ~/.codex/skills/pua
rm ~/.codex/skills/p7
rm ~/.codex/skills/p9
rm ~/.codex/skills/p10
rm ~/.codex/skills/pro
rm ~/.codex/skills/yes
rm ~/.codex/skills/pua-en
rm ~/.codex/skills/pua-ja
rm ~/.codex/prompts/pua.md
rm -rf ~/.codex/pua
```

### Windows (PowerShell)

```powershell
Remove-Item "$env:USERPROFILE\.codex\skills\pua"
Remove-Item "$env:USERPROFILE\.codex\skills\p7"
Remove-Item "$env:USERPROFILE\.codex\skills\p9"
Remove-Item "$env:USERPROFILE\.codex\skills\p10"
Remove-Item "$env:USERPROFILE\.codex\skills\pro"
Remove-Item "$env:USERPROFILE\.codex\skills\yes"
Remove-Item "$env:USERPROFILE\.codex\skills\pua-en"
Remove-Item "$env:USERPROFILE\.codex\skills\pua-ja"
Remove-Item "$env:USERPROFILE\.codex\prompts\pua.md"
Remove-Item -Recurse "$env:USERPROFILE\.codex\pua"
```
