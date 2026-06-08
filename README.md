# Anti-OOP Design — Claude Code Plugin

Architecture by aggregation: separate pure computation from side-effect storage.

## Installation

```bash
# Add from GitHub
/plugin marketplace add cypress927/anti-oop-claude-skill

# Install the plugin
/plugin install anti-oop-design@cypress927/anti-oop-claude-skill
```

Or manually clone and copy to your project's `.claude/skills/`.

## Structure

```
anti-oop-claude-skill/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   └── anti-oop-design/
│       └── SKILL.md          # Skill definition
└── README.md
```

## License

MIT
