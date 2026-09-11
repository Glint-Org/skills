# Glint-Capture Reference

## CLI Commands

| Command | Description |
|---------|-------------|
| `glint init` | Create `glint.yaml`, `test/glint_screenshots_test.dart`, `test/flutter_test_config.dart` |
| `glint discover [--write] [--max N]` | Scan `lib/` for `*Screen`/`*Page` widgets, score by marketing value |
| `glint capture [--auto]` | Run `flutter test` on screenshot rules. `--auto` = discover + capture |
| `glint help` | Show help |

## glint.yaml Schema

```yaml
store: play/phone          # play/phone | ios/iphone | ios/ipad | play/tablet-7 | etc.
output: glint_screenshots  # output directory (default: glint_screenshots)

# Single device (soft launch recommended):
devices:
  - name: pixel9
    width: 412
    height: 915
    device_pixel_ratio: 2.625
    platform: android

# Or use a preset:
# devices: play_store   # pixel9 + galaxy_s24
# devices: app_store    # iphone16ProMax + iphone16Pro + iPad
# devices: all          # all 6 curated devices
```

## Device Presets

| Name | Logical Size | DPR | Pixels | Platform | Store |
|------|-------------|-----|--------|----------|-------|
| `pixel9` | 412×915 | 2.625 | 1081×2402 | Android | Play Phone |
| `galaxy_s24` | 360×780 | 3.0 | 1080×2340 | Android | Play Phone |
| `iphone16ProMax` | 430×932 | 3.0 | 1290×2796 | iOS | App Store 6.7" |
| `iphone16Pro` | 393×852 | 3.0 | 1179×2556 | iOS | App Store 6.1" |
| `ipadPro129` | 1024×1366 | 2.0 | 2048×2732 | iOS | App Store iPad |
| `ipadPro11` | 834×1194 | 2.0 | 1668×2388 | iOS | App Store iPad |

## Store Sizes (exported PNGs)

| Store | Dimensions | Device |
|-------|-----------|--------|
| Play Phone | 1080×1920 | pixel9 |
| Play Tablet 7" | 1200×1920 | - |
| Play Tablet 10" | 1600×2560 | - |
| iOS iPhone | 1290×2796 | iphone16ProMax |
| iOS iPad | 2048×2732 | ipadPro129 |

## Test File Structure

```dart
import 'package:flutter/material.dart';
import 'package:glint_capture/glint_capture.dart';

void main() {
  glintScreenshots(
    devices: [GLINTDevice.pixel9],
    rules: [
      GLINTRule.screen(
        name: 'home',
        builder: (context) => const MyHomeScreen(),
      ),
      GLINTRule.screen(
        name: 'profile',
        builder: (context) => const MyProfileScreen(),
        pump: GLINTPump.duration(500), // wait for animations
      ),
    ],
  );
}
```

## Screen Quality

**Prefer:** Home/feed with content, feature screens with rich UI, profile/settings with data, empty states with illustrations.

**Reject:** Login/signup, debug/test, loading/error, permission screens, `Center(child: Text('Hello'))`.

## Output Structure

```
glint_screenshots/
├── android/
│   └── pixel9/
│       ├── home.png
│       └── profile.png
└── session.json
```
