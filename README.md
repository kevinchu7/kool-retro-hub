<p align="right">
  <a href="README.md">English</a> | <a href="README.zh-CN.md">中文</a>
</p>

# KoolRetroHub

A browser-based retro game emulator powered by EmulatorJS.

## How to Add a Game

### 1. Place the ROM file

Copy your game ROM into `data/roms/`:

```
data/roms/
├── my_game.nes       ← NES ROM
├── pokemon.gba       ← GBA ROM
└── zelda.n64         ← N64 ROM
```

### 2. Configure in games.json

Edit `config/games.json` and add an entry:

```json
{
    "id": "my_game",
    "title": "My Game",
    "file": "data/roms/my_game.nes",
    "core": "nes",
    "cover": "data/covers/my_game.png",
    "description": "A brief description."
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `id` | ✅ | Unique identifier, used in URL (`play.html?game=xxx`) |
| `title` | ✅ | Display name shown in game library |
| `file` | ✅ | Path to the ROM file |
| `core` | ✅ | Emulator core — `nes`, `gba`, `n64`, `snes`, `psx`, `psp`, etc. |
| `cover` | ❌ | Path to cover image (leave `""` to show placeholder) |
| `description` | ❌ | Short description shown on the game card |

### 3. (Optional) Add a cover image

Place a 300×400 px PNG/JPG in `data/covers/` and set the `cover` field in `games.json`.

### 4. Start the server

```bash
cd /path/to/game-hub
python -m http.server 8080
# or
npx http-server -p 8080
```

Open `http://localhost:8080` in your browser.

> **Note**: The emulator needs an HTTP server — `file://` protocol will not work due to browser CORS restrictions.

## Supported Cores

| Core | Systems | File Extensions |
|------|---------|-----------------|
| `nes` | NES/Famicom | `.nes` |
| `snes` | SNES/Super Famicom | `.smc`, `.sfc` |
| `gba` | Game Boy Advance | `.gba` |
| `gb` | Game Boy / Game Boy Color | `.gb`, `.gbc` |
| `n64` | Nintendo 64 | `.n64`, `.z64` |
| `psx` | PlayStation | `.bin`, `.cue`, `.chd` |
| `psp` | PlayStation Portable | `.iso`, `.cso` |
| `segaMD` | Sega Mega Drive / Genesis | `.md`, `.bin` |
| `atari2600` | Atari 2600 | `.a26` |
| ... | See EmulatorJS docs | |

## File Naming

Avoid spaces in ROM filenames. Use underscores instead:

```
✅ pokemon_red.gba
❌ pokemon red.gba
```

## Save States

- **Save**: Click the save button → downloads a `.state` file
- **Load**: Click the load button → select a `.state` file
- Files are named `{game_id}_{timestamp}.state`

## Tech Stack

- [EmulatorJS](https://github.com/EmulatorJS/EmulatorJS) v4.0.12
- Pure HTML/CSS/JS (no backend required)

---

Updated occasionally. If you like it, please drop a ⭐ Star~
