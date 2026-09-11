# Glint agent skills

Agent skill for [Glint](https://github.com/Glint-Org) - create Play Store and App Store screenshots from real app UI.

**Docs:** https://glint-org.github.io/Glint-Docs/

## Install

```bash
npx skills add Glint-Org/skills
# or just the glint skill:
npx skills add Glint-Org/skills --skill glint
```

Then ask your agent something like: *create store screenshots for this app*.

## Layout

```
glint/
  SKILL.md           # when / how to run Capture, Bridge, Web, MCP
  references/        # deeper CLI and schema notes (loaded on demand)
```

Keep the skill in its own folder (`glint/`). Do not flatten `SKILL.md` to the repo root unless this repo becomes a single-skill-only package renamed to match the skill.

## What it teaches the agent

1. Pick Capture (Flutter) or Bridge (Android device)
2. Capture real screens → `session.json` + PNGs
3. Import / export via Glint Web (or MCP / headless)
4. Iterate without inventing fake store art

## Related repos

| Repo | Role |
|------|------|
| [Glint-Capture](https://github.com/Glint-Org/Glint-Capture) | Flutter capture |
| [Glint-Bridge](https://github.com/Glint-Org/Glint-Bridge) | Device / ADB capture |
| [Glint-Web](https://github.com/Glint-Org/Glint-Web) | Frames editor + ZIP |
| [Glint-MCP](https://github.com/Glint-Org/Glint-MCP) | Agent tools |
| [Glint-Docs](https://github.com/Glint-Org/Glint-Docs) | Public documentation |

## License

MIT - see [LICENSE](LICENSE).
