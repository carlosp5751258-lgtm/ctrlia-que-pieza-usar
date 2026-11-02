# Claude Code: skills vs hooks, MCP, subagentes y plugins

[Read in English](README.en.md)

English version: [README.en.md](README.en.md) (archivos en `en/`).

Un ejemplo mínimo y real de cada pieza con la que se extiende Claude Code, colocado donde va, para copiar a tu proyecto. La regla corta: **CLAUDE.md** para lo que Claude debe saber siempre, **skill** para procedimientos, **subagente** para aislar trabajo, **hook** para lo que debe pasar siempre, **MCP** para conectar servicios y **plugin** para empaquetar y compartir.

La referencia completa (cuándo usar cada una, cuánto contexto gasta, quién gana si se repiten) está en:

- Español: https://ctrlia.dev/recetas/que-pieza-usar.html
- English: https://ctrlia.dev/en/recetas/que-pieza-usar.html

## Qué incluye

| Archivo | Pieza | Para qué |
| --- | --- | --- |
| `ejemplo/CLAUDE.md` | CLAUDE.md | Contexto que se carga en cada sesión («usa pnpm, no npm») |
| `ejemplo/.claude/skills/release/SKILL.md` | Skill | `/release`: notas de versión desde el último tag; solo la invocas tú (`disable-model-invocation: true`) |
| `ejemplo/.claude/agents/code-reviewer.md` | Subagente | Revisor de solo lectura (`tools: Read, Glob, Grep`), ejemplo oficial |
| `ejemplo/.claude/settings.json` | Hook | `PostToolUse` que formatea con Prettier tras cada edición, ejemplo oficial; **requiere `jq` y `npx`** |

## Cómo usarlo

Copia solo la pieza que necesites a la misma ruta de tu proyecto, por ejemplo la skill:

```bash
git clone https://github.com/carlosp5751258-lgtm/ctrlia-que-pieza-usar.git
mkdir -p .claude/skills
cp -r ctrlia-que-pieza-usar/ejemplo/.claude/skills/release .claude/skills/
```

Si ya tienes `.claude/settings.json`, no lo sustituyas: añade solo el bloque `hooks`.

MCP y plugins se crean con comandos (ejemplos oficiales):

```bash
# MCP: conectar un servicio externo por HTTP; dentro de la sesión, /mcp para el estado
claude mcp add --transport http notion https://mcp.notion.com/mcp

# Plugin: empaquetar tu configuración (desde la 2.1.157)
claude plugin init mi-kit
claude plugin details mi-kit@skills-dir
claude plugin disable mi-kit@skills-dir
```

## Qué se probó

Con Claude Code **2.1.316** en Linux: `claude plugin --help` y `claude plugin init mi-kit`, que creó `~/.claude/skills/mi-kit/` con `SKILL.md` y `.claude-plugin/plugin.json`. Los archivos de este repo se comprobaron como JSON válido y frontmatter con `name` y `description`. Los ejemplos de subagente, hook y MCP son literales de la doc oficial; el hook de Prettier no se ejecutó (falta `jq` en el PC de pruebas).

## Licencia

MIT. Ver [LICENSE](LICENSE).

---
Parte de **[Ctrl+IA](https://ctrlia.dev/)**: programa con Claude Code como un pro, en español. Hecho por Carlos P.
