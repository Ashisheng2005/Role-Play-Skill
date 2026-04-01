# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code **plugin/skill** that transforms Claude into family member roles (mom, dad, grandma, grandpa, teacher, sister, brother, younger_sister). When the user calls out their configured character, Claude responds in that role's personality and communication style.

**Note**: This is not a typical code project with build/test commands. It's a configuration-driven skill.

## Architecture

```
.claude-plugin/
├── plugin.json       # Plugin manifest (name: "roleplay", skills: ["roleplay"])
└── marketplace.json  # Marketplace config for plugin discovery
skills/roleplay/
├── SKILL.md                    # Skill behavior definition
└── references/
    ├── personality.md          # Character config - change `name` to switch roles
    └── examples/               # Optional tone learning samples
```

**Plugin Installation**: Add to `~/.claude/settings.json` under `extraKnownMarketplaces`:
```json
"extraKnownMarketplaces": {
  "roleplay": {
    "source": {
      "source": "directory",
      "path": "/path/to/RolePlaySkill"
    }
  }
}
```

## Character Switching

The **only file you need to modify** is `skills/roleplay/references/personality.md`. Change the `name` field:

| name | Character | Call User |
|------|-----------|-----------|
| `mom` | Loving, nurturing mother | 孩子, 宝贝 |
| `dad` | Authoritative, direct father | 儿子, 闺女 |
| `grandma` | Doting, wise grandmother | 孙儿, 孙女 |
| `grandpa` | Wise, stoic grandfather | 孙儿, 孙女 |
| `teacher` | Patient, educational teacher | 同学 |
| `sister` | Gentle, intellectual older sister | 弟, 妹 |
| `brother` | Steady, reliable older brother | 弟, 妹 |
| `younger_sister` | Playful, mischievous younger sister | 哥, 姐 |
| `custom` | Fully customizable | User-defined |

## How It Works

1. User invokes `/roleplay` or speaks a trigger word (e.g., "妈！", "爸！")
2. SKILL.md reads `personality.md`
3. Finds the `name` field to determine the character preset
4. Applies any custom override fields in the config
5. Reads `examples/` directory for tone learning samples
6. Responds in character with appropriate warmth, authority, and nagging levels

## Commands

- `/roleplay` — Activate role-play with the configured character
- Trigger words ("妈！", "爸！", "奶奶！", etc.) auto-activate the skill

## Key Files

| File | Purpose |
|------|---------|
| `.claude-plugin/marketplace.json` | Marketplace manifest for plugin discovery |
| `.claude-plugin/plugin.json` | Plugin manifest - name, version, skills array, commands |
| `skills/roleplay/SKILL.md` | Skill behavior definition and character presets |
| `skills/roleplay/references/personality.md` | Active character config (modify `name` to switch) |
| `skills/roleplay/references/examples/` | Tone learning samples (optional) |
