# Stremio Discord Rich Presence

A Windows background application that adds Discord Rich Presence integration for Stremio, automatically showing what you're watching on Discord.

## Features

✅ **Automatic Detection** - Monitors Stremio window and detects what you're watching  
✅ **Rich Metadata** - Fetches movie/show posters and runtime from TMDB  
✅ **Progress Bar** - Shows watch progress with start/end timestamps  
✅ **Episode Support** - Displays season and episode numbers for TV shows  
✅ **System Tray** - Runs silently in background with tray icon  
✅ **Easy Controls** - Toggle Rich Presence and auto-start from tray menu  
✅ **Persistent Settings** - Saves preferences in config.json  
✅ **Auto-reconnect** - Works even if Discord restarts  
✅ **Auto-start** - Can launch automatically with Stremio

## Prerequisites

Before building, you need:

1. **Node.js 18+** - Download from [nodejs.org](https://nodejs.org/)
2. **Discord Application** - Create one at [discord.com/developers](https://discord.com/developers/applications)
3. **TMDB API Key** - Get one free at [themoviedb.org/settings/api](https://www.themoviedb.org/settings/api)

## Setup Instructions

### Step 1: Create Discord Application

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Name it "Stremio" (or whatever you prefer)
4. Go to "Rich Presence" → "Art Assets"
5. Upload a Stremio logo as `stremio_logo`
6. Copy your **Application ID** (Client ID)

### Step 2: Get TMDB API Key

1. Go to [TMDB](https://www.themoviedb.org/)
2. Create a free account
3. Go to Settings → API
4. Request an API key (choose "Developer")
5. Copy your **API Key (v3 auth)**

### Step 3: Configure the Application

1. Open `index.js`
2. Replace these values:
   ```javascript
   const DISCORD_CLIENT_ID = 'YOUR_DISCORD_CLIENT_ID_HERE';
   const TMDB_API_KEY = 'YOUR_TMDB_API_KEY_HERE';
   ```

### Step 4: Install Dependencies

```bash
npm install
```

## Running the Application

### Development Mode

```bash
npm start
```

This runs the app in development mode using Electron.

## Building the Application

### Method 1: Electron Builder (Recommended)

Creates a proper Windows installer:

```bash
npm run build
```

This creates:
- `dist/Stremio Discord RPC Setup.exe` - Installer
- Installed to `C:\Users\YourName\AppData\Local\Programs\stremio-discord-rpc\`

For a portable version:

```bash
npm run build:portable
```

This creates:
- `dist/Stremio Discord RPC.exe` - Portable executable

### Method 2: PKG (Alternative)

Creates a single executable file:

```bash
npm run package
```

This creates:
- `dist/stremio-rpc.exe` - Standalone executable

**Note:** The PKG method may have issues with Electron's IPC. Use Electron Builder for best results.

## Installation

### Using the Installer

1. Run `Stremio Discord RPC Setup.exe`
2. Follow installation wizard
3. Launch from Start Menu or Desktop shortcut
4. App will appear in system tray

### Using Portable Version

1. Run `Stremio Discord RPC.exe` from anywhere
2. App will appear in system tray
3. No installation required

## Usage

### System Tray Menu

Right-click the tray icon to access:

- **✓ Rich Presence Enabled** - Toggle Discord Rich Presence on/off
- **✓ Auto-start with Stremio** - Toggle automatic startup
- **Exit** - Close the application

### How It Works

1. The app monitors for Stremio running every 5 seconds
2. When Stremio is detected, it reads the window title
3. Parses movie/show information from the title
4. Fetches metadata from TMDB (poster, runtime)
5. Updates Discord Rich Presence with:
   - Movie/Show title
   - Episode info (if TV show)
   - Poster image
   - Progress bar (based on runtime)
   - "Watch on Stremio" button

### Title Format Examples

The app recognizes these Stremio window title formats:

- `Stremio — The Matrix` → Movie
- `Stremio — Breaking Bad S05E14` → TV Show with episode
- `Stremio` → Idle (clears presence)

## Configuration

Settings are saved in `config.json`:

```json
{
  "enabled": true,
  "autoStart": false
}
```

Location: `%APPDATA%/stremio-discord-rpc/config.json`

## Troubleshooting

### Discord not showing presence

1. Make sure Discord is running
2. Check that "Display current activity as status message" is enabled in Discord Settings → Activity Privacy
3. Restart both Discord and the app
4. Verify your Discord Client ID is correct

### Can't detect Stremio

1. Make sure Stremio is running
2. Make sure you're actually playing something (not just browsing)
3. Check that the window title contains "Stremio —"

### TMDB metadata not loading

1. Verify your TMDB API key is valid
2. Check your internet connection
3. The app will still work without TMDB, just without posters/runtime

### Auto-start not working

1. Check Windows Task Manager → Startup tab
2. Enable "Stremio Discord RPC" if disabled
3. Or toggle auto-start off and on again in tray menu

## File Structure

```
stremio-discord-rpc/
├── index.js           # Main application code
├── package.json       # Dependencies and build config
├── icon.ico          # Application icon (create or download)
├── config.json       # User settings (auto-generated)
└── dist/             # Built executables (after build)
```

## Creating an Icon

You can use any icon converter to create `icon.ico`:

1. Download a Stremio logo PNG
2. Use [converticon.com](https://converticon.com/) or similar
3. Convert to 256x256 ICO format
4. Save as `icon.ico` in project root

Or use the default Electron icon (app will still work).

## Requirements

- **Windows 10/11** (64-bit)
- **Discord** desktop app running
- **Stremio** installed and running
- **Internet connection** for TMDB API

## Known Limitations

- Only works on Windows
- Requires Stremio window title to be in standard format
- Cannot detect playback progress (only shows estimated progress based on runtime)
- Works best with Stremio's internal player

## License

MIT License - Feel free to modify and distribute

## Credits

- [Discord RPC](https://github.com/discordjs/RPC) - Discord Rich Presence client
- [TMDB](https://www.themoviedb.org/) - Movie/TV metadata
- [Electron](https://www.electronjs.org/) - Cross-platform desktop app framework

## Support

If you encounter issues:

1. Check the troubleshooting section
2. Verify all configuration values
3. Check console output in development mode
4. Make sure all prerequisites are installed

---

**Enjoy showing off what you're watching on Stremio! 🎬**