# Session Schema Reference

## Format

```json
{
  "screens": ["android/pixel9/home.png", "android/pixel9/profile.png"],
  "store": "play/phone",
  "version": "1.0",
  "locales": ["en-US"],
  "exportedAt": "2026-09-03T12:00:00.000Z"
}
```

## Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `screens` | string[] | yes | Ordered screenshot paths or data URLs |
| `store` | string | yes | `play/phone`, `ios/iphone`, `ios/ipad`, `play/tablet-7`, etc. |
| `version` | string | yes | Schema version (`"1.0"`) |
| `locales` | string[] | no | BCP-47 tags (default `["en-US"]`) |
| `exportedAt` | string | yes | ISO timestamp |

## Store Values

| Value | Platform | Device |
|-------|----------|--------|
| `play/phone` | Android | Phone (1080×1920) |
| `play/tablet-7` | Android | 7" Tablet (1200×1920) |
| `play/tablet-10` | Android | 10" Tablet (1600×2560) |
| `play/tv` | Android | TV (1920×1080) |
| `play/wear` | Android | Wear OS (450×450) |
| `play/chromebook` | Android | Chromebook (1920×1080) |
| `ios/iphone` | iOS | iPhone (1290×2796) |
| `ios/ipad` | iOS | iPad (2048×2732) |

## Legacy Aliases (auto-normalized)

| Input | Normalized |
|-------|-----------|
| `play` | `play/phone` |
| `android` | `play/phone` |
| `ios` | `ios/iphone` |
| `ios-tablet` | `ios/ipad` |

## Screen Paths

- **From Capture:** Relative paths like `android/pixel9/home.png`
- **From Bridge:** Basenames like `screenshot_0001.png`
- **For View:** Data URLs (`data:image/png;base64,...`) or HTTP URLs
