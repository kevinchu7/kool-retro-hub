<p align="right">
  <a href="README.md">English</a> | <a href="README.zh-CN.md">中文</a>
</p>

# KoolRetroHub

基于 EmulatorJS 的浏览器端怀旧游戏模拟器。

## 如何添加游戏

### 1. 放入 ROM 文件

将游戏 ROM 复制到 `data/roms/` 目录：

```
data/roms/
├── my_game.nes       ← NES 游戏
├── pokemon.gba       ← GBA 游戏
└── zelda.n64         ← N64 游戏
```

### 2. 配置 games.json

编辑 `config/games.json`，添加一个条目：

```json
{
    "id": "my_game",
    "title": "My Game",
    "file": "data/roms/my_game.nes",
    "core": "nes",
    "cover": "data/covers/my_game.png",
    "description": "一段简短的描述。"
}
```

| 字段 | 必填 | 说明 |
|------|------|------|
| `id` | ✅ | 唯一标识，用于 URL（`play.html?game=xxx`） |
| `title` | ✅ | 游戏名称，显示在游戏库中 |
| `file` | ✅ | ROM 文件路径 |
| `core` | ✅ | 模拟核心 — `nes`、`gba`、`n64`、`snes`、`psx`、`psp` 等 |
| `cover` | ❌ | 封面图片路径（留空 `""` 显示占位图） |
| `description` | ❌ | 游戏描述，显示在卡片上 |

### 3. （可选）添加封面图片

将 300×400 像素的 PNG/JPG 放入 `data/covers/`，然后在 `games.json` 中设置 `cover` 字段。

### 4. 启动服务器

```bash
cd /path/to/game-hub
python -m http.server 8080
# 或
npx http-server -p 8080
```

浏览器打开 `http://localhost:8080`。

> **注意**：模拟器需要 HTTP 服务器运行，不能直接用 `file://` 打开，浏览器 CORS 策略会阻止加载。

## 支持的核心

| 核心 | 对应平台 | 文件后缀 |
|------|---------|---------|
| `nes` | 红白机 / FC | `.nes` |
| `snes` | 超任 / SFC | `.smc`、`.sfc` |
| `gba` | Game Boy Advance | `.gba` |
| `gb` | Game Boy / Color | `.gb`、`.gbc` |
| `n64` | Nintendo 64 | `.n64`、`.z64` |
| `psx` | PlayStation | `.bin`、`.cue`、`.chd` |
| `psp` | PlayStation Portable | `.iso`、`.cso` |
| `segaMD` | Sega Mega Drive | `.md`、`.bin` |
| `atari2600` | Atari 2600 | `.a26` |
| ... | 更多请查看 EmulatorJS 文档 | |

## 文件命名建议

文件名中不要包含空格，建议使用下划线：

```
✅ pokemon_red.gba
❌ pokemon red.gba
```

## 存档管理

- **保存进度**：点击「存档」按钮 → 下载 `.state` 文件到本地
- **读取存档**：点击「读档」按钮 → 选择本地的 `.state` 文件
- 文件名格式：`{游戏ID}_{时间戳}.state`

## 技术栈

- [EmulatorJS](https://github.com/EmulatorJS/EmulatorJS) v4.0.12
- 纯 HTML/CSS/JS（无需后端）

---

不定期更新，喜欢的话请点个 ⭐ Star~
