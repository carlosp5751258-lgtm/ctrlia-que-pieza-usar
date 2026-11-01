# Claude Code: skills vs hooks, MCP, subagents and plugins

[Leer en español](README.md)

A minimal, real example of each piece Claude Code is extended with, placed where it goes, ready to copy into your project. The short rule: **CLAUDE.md** for what Claude must always know, **skill** for procedures, **subagent** to isolate work, **hook** for what must always happen, **MCP** to connect services and **plugin** to package and share.

The full reference (when to use each one, how much context it uses, who wins when they repeat) is at:

- English: https://ctrlia.dev/en/recetas/que-pieza-usar.html
- Español: https://ctrlia.dev/recetas/que-pieza-usar.html

## What's included

| File | Piece | What for |
| --- | --- | --- |
| `ejemplo/CLAUDE.md` | CLAUDE.md | Context loaded in every session ("use pnpm, not npm", in Spanish) |
| `ejemplo/.claude/skills/release/SKILL.md` | Skill | `/release`: release notes since the last tag (in Spanish); only you invoke it (`disable-model-invocation: true`) |
| `ejemplo/.claude/agents/code-reviewer.md` | Subagent | Read-only reviewer (`tools: Read, Glob, Grep`), official example |
| `ejemplo/.claude/settings.json` | Hook | `PostToolUse` that formats with Prettier after every edit, official example; **requires `jq` and `npx`** |

## How to use it

Copy only the piece you need to the same path in your project, for example the skill:

```bash
git clone https://github.com/carlosp5751258-lgtm/ctrlia-que-pieza-usar.git
mkdir -p .claude/skills
cp -r ctrlia-que-pieza-usar/ejemplo/.claude/skills/release .claude/skills/
```

If you already have `.claude/settings.json`, don't replace it: add only the `hooks` block.

MCP servers and plugins are created with commands (official examples):

```bash
# MCP: connect an external service over HTTP; inside the session, /mcp for status
claude mcp add --transport http notion https://mcp.notion.com/mcp

# Plugin: package your setup (since 2.1.157)
claude plugin init mi-kit
claude plugin details mi-kit@skills-dir
claude plugin disable mi-kit@skills-dir
```

## What was tested

With Claude Code **2.1.316** on Linux: `claude plugin --help` and `claude plugin init mi-kit`, which created `~/.claude/skills/mi-kit/` with `SKILL.md` and `.claude-plugin/plugin.json`. The files in this repo were checked for valid JSON and frontmatter with `name` and `description`. The subagent, hook and MCP examples are verbatim from the official docs; the Prettier hook wasn't run (`jq` is missing on the test PC).

## License

MIT. See [LICENSE](LICENSE).

---
Part of **[Ctrl+IA](https://ctrlia.dev/)**: code with Claude Code like a pro, in Spanish. Made by Carlos P.
