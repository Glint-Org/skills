# Glint-Bridge Reference

## Commands

| Command | Description |
|---------|-------------|
| `python glint.py check` | Verify ADB + AI status |
| `python glint.py devices` | List connected USB/WiFi devices |
| `python glint.py capture` | Single screenshot → `output/` |
| `python glint.py batch --count N` | N screenshots with 1s delay |
| `python glint.py crawl --package com.app` | Auto-navigate + capture (heuristic) |
| `python glint.py crawl --package com.app --ai` | AI-guided navigation + capture |
| `python glint.py crawl-web --url https://example.com` | Web page crawl |
| `python glint.py start` | WebSocket server for Glint-Web |

## Prerequisites

- **ADB:** `apt install android-tools-adb` / `brew install android-platform-tools`
- **Python 3.10+:** with `websockets>=12.0` installed
- **Device:** USB connected with USB debugging enabled
- **For AI crawl:** `GLINT_AI_API_KEY` or `OPENAI_API_KEY` or `ANTHROPIC_API_KEY` env var
- **For Appium crawl:** `pip install Appium-Python-Client` + running Appium server

## Crawl Modes

### Heuristic (no AI key)
- Scrolls and taps through the app
- Keeps every 3rd unique screen
- Dedup by file size fingerprint
- Good enough for simple apps

### AI (with API key)
- Vision model scores each screen for store marketing value
- Smart navigation: taps feature-rich areas, scrolls to content
- Rejects: login, loading, error, permission dialogs
- Keeps 5-8 best unique screens

## Output

```
Glint-Bridge/output/
├── screenshot_0001.png
├── screenshot_0002.png
├── ...
└── session.json
```

## WebSocket Protocol

Server: `ws://127.0.0.1:7700`

1. Client connects
2. Client sends: `{"action":"pair","token":"<token>"}`
3. Server accepts or rejects
4. Client sends actions: `capture_single`, `capture_batch`, `crawl`, `devices`, `wifi`, `ping`

## Security

- Binds to `localhost` only (never `0.0.0.0`)
- Pairing token required before any action
- API keys read from env only
