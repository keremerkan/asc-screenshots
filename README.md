# asc-screenshots

AI agent skill that generates production-ready App Store screenshots for iPhone and iPad. Designs ad-style marketing layouts, frames them in official Apple device bezels, and exports in a format ready for upload via [asc-client](https://github.com/keremerkan/asc-client).

## What it does

- Asks about your app's brand, features, and style preferences
- Scaffolds a Next.js project (or works within an existing one)
- Frames screenshots into official Apple device bezels using [FrameMe](https://github.com/joshluongo/frameme) (pixel-perfect Dynamic Island, rounded corners)
- Designs each screenshot as an **advertisement** — not a UI showcase
- Writes compelling copy using proven App Store copywriting patterns
- Supports multiple languages with a `copy.json` file and language switcher
- Exports PNGs at the largest Apple-required size per device (auto-scales to smaller displays)
- Zip export compatible with [asc-client](https://github.com/keremerkan/asc-client) for direct App Store Connect upload

## Install

### Using npx skills (recommended)

```bash
npx skills add keremerkan/asc-screenshots
```

Works with Claude Code, Cursor, Windsurf, OpenCode, Codex, and [40+ other agents](https://github.com/vercel-labs/skills#available-agents).

Install globally (available across all projects):

```bash
npx skills add keremerkan/asc-screenshots -g
```

Install for a specific agent:

```bash
npx skills add keremerkan/asc-screenshots -a claude-code
```

### Manual (git clone)

```bash
git clone https://github.com/keremerkan/asc-screenshots ~/.claude/skills/asc-screenshots
```

### Install FrameMe (required, macOS only)

```bash
git clone https://github.com/joshluongo/frameme.git /tmp/frameme
cd /tmp/frameme && swift build -c release
strip .build/release/frameme
cp .build/release/frameme /usr/local/bin/frameme
```

## Usage

Once installed, the skill triggers automatically when you ask your AI agent to:

- Build App Store screenshots
- Generate marketing screenshots for an iOS/iPad app
- Create exportable screenshot assets

```
> Build App Store screenshots for my app
```

The agent will ask about your screenshots, brand colors, font, features, style direction, target devices, localization, and number of slides before building anything.

## What gets scaffolded

```
project/
├── public/
│   ├── app-icon.png            # Your app icon
│   ├── framed/                 # Device-framed screenshots (via FrameMe)
│   │   ├── iphone/{locale}/
│   │   └── ipad/{locale}/
│   └── screenshots/            # Raw app screenshots
│       ├── iphone/{locale}/
│       └── ipad/{locale}/
├── src/app/
│   ├── copy.json               # Localized copy (editable without touching code)
│   ├── layout.tsx              # Font setup
│   └── page.tsx                # Screenshot generator (single file)
├── package.json
└── ...
```

Run the dev server, preview in the browser, export individual PNGs or download all as a zip.

```bash
cd path/to/generator && bun next dev --port 3847
# Open http://localhost:3847
```

## Included bezels

| Device | Bezel file | Resolution |
|--------|-----------|-----------|
| iPhone 17 Pro | `iphone-17-pro.png` | 1350×2760 |
| iPhone 17 Pro Max | `iphone-17-pro-max.png` | 1470×3000 |
| iPad Pro 11" M4 | `ipad-pro-11.png` | 1880×2640 |
| iPad Pro 13" M4 | `ipad-pro-13.png` | 2300×3000 |

Capture screenshots on a simulator that matches one of these devices.

## Export sizes

| Device | Display | Resolution |
|--------|---------|-----------|
| iPhone | 6.9" | 1320×2868 |
| iPad | 13" | 2064×2752 |

Only the largest size per device is generated — App Store Connect automatically scales to smaller displays.

## Export format (asc-client compatible)

The zip follows the [asc-client](https://github.com/keremerkan/asc-client) directory structure:

```
en-US/APP_IPHONE_67/01_hero.png
en-US/APP_IPAD_PRO_3GEN_129/01_hero.png
de-DE/APP_IPHONE_67/01_hero.png
```

Upload directly: `asc-client apps upload-media <bundle-id> --folder <unzipped-folder>`

## Requirements

- macOS
- Node.js 18+
- [FrameMe](https://github.com/joshluongo/frameme) (build from source, see install instructions above)
- One of: bun, pnpm, yarn, or npm (detected automatically, bun preferred)

## Credits

Originally based on [ParthJadhav/app-store-screenshots](https://github.com/ParthJadhav/app-store-screenshots). This project has since been significantly rewritten with FrameMe integration, iPad support, localization, and asc-client compatible export.

## License

MIT
