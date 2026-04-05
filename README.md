# Supercapture

A screenshot annotation tool for macOS.

## Install Supercapture

1. Download **SuperCapture-osx-Setup.pkg** from the [latest release](https://github.com/supercapture/releases/releases/latest)
2. Open the `.pkg` and follow the installer
3. Launch **Supercapture** from your Applications folder
4. Grant **Screen Recording** permission when prompted

## Browser Extensions

The browser extensions enable full-page screenshots, area selection, and multi-page slideshow capture (DocSend, Google Slides, Canva, and more).

> The extensions communicate with the desktop app over localhost. Supercapture must be running for the extensions to work.

### Safari Extension

The Safari extension is included with Supercapture — no separate download needed.

1. Open **Safari → Settings → Extensions** (or Safari → Preferences → Extensions)
2. Check the box next to **Supercapture**
3. When prompted, choose which websites the extension can access (or select **All Websites**)

The Supercapture icon will appear in your Safari toolbar. You can also right-click any page for capture options.

### Chrome / Edge / Brave Extension

The same extension works in all Chromium-based browsers. The extension is bundled inside the app — no separate download needed.

1. Open your browser's extensions page: Chrome (`chrome://extensions`), Edge (`edge://extensions`), or Brave (`brave://extensions`)
2. Enable **Developer mode** (toggle in the top-right corner)
3. Click **Load unpacked** and select:
   ```
   /Applications/Supercapture.app/Contents/Resources/Extensions/chrome
   ```
4. The Supercapture icon will appear in your browser toolbar

> **Tip:** You can paste the path above into the folder selection dialog's **Go to Folder** field (Cmd+Shift+G in Finder).

### Firefox Extension

The extension is bundled inside the app — no separate download needed.

1. Open Firefox and go to `about:debugging#/runtime/this-firefox`
2. Click **Load Temporary Add-on** and select:
   ```
   /Applications/Supercapture.app/Contents/Resources/Extensions/firefox/manifest.json
   ```
3. The Supercapture icon will appear in your Firefox toolbar

> Temporary add-ons are removed when Firefox restarts. For permanent installation, the extension needs to be signed via [addons.mozilla.org](https://addons.mozilla.org).

## Command-Line Interface

Supercapture includes a CLI tool for scripting captures, managing gallery items, and controlling the app from the terminal.

```bash
# Add to your PATH (one-time setup)
ln -s /Applications/Supercapture.app/Contents/MacOS/supercapture-cli /usr/local/bin/supercapture

# Check if the app is running
supercapture status

# List available tools
supercapture tools

# Search for capture-related tools
supercapture tools capture

# Call a tool
supercapture call app_get_state
supercapture call capture_self -o screenshot.png
supercapture call gallery_list limit=5
```

Run `supercapture help` for full usage. Requires the Supercapture desktop app to be running.

## Headless Browser Automation

Supercapture can launch a headless browser for fully automated CLI capture workflows — no visible window, no user interaction needed. This is useful for scripting screenshot capture of web pages, presentations, and local HTML files.

```bash
supercapture call browser_launch url=https://news.yahoo.com width=1800 height=1200
supercapture call capture_visible_page tab_url=news.yahoo.com
supercapture call browser_close
```

### Requirements

Headless mode requires **Chromium** (Google Chrome does not support loading unpacked extensions programmatically).

```bash
brew install chromium
```

On first run, macOS Gatekeeper may block Chromium. Remove the quarantine attribute:

```bash
xattr -cr /opt/homebrew/Caskroom/chromium/*/chrome-mac/Chromium.app
```

### Available Tools

| Tool | Description |
|------|-------------|
| `browser_launch` | Launch headless Chromium with the extension. Optional: `url`, `width`, `height` (default 1800x1200) |
| `browser_close` | Close the headless browser and clean up |
| `extension_open_tab` | Open a URL in the headless browser (`file:///` supported) |
| `capture_visible_page` | Capture the visible viewport (use `tab_url` to target a specific tab) |
| `capture_full_page` | Capture a full scrolling page |
| `capture_presentation` | Auto-detect and capture all slides from a presentation |

All capture and automation tools accept `tab_url` for URL-based tab matching, in addition to the existing `tab_title`.

## MCP Server

Supercapture exposes an [MCP](https://modelcontextprotocol.io) server with 150+ tools for capturing screenshots, annotating images, managing gallery items, recording video, and more. Any MCP-compatible client running on the same machine can connect — no authentication required for local connections.

### Configuration

Add the following to your MCP client's config file:

```json
{
  "mcpServers": {
    "supercapture": {
      "url": "http://localhost:21516/mcp"
    }
  }
}
```

**Config file locations by client:**

| Client | Config File |
|--------|------------|
| Claude Code | `~/.claude/settings.json` |
| Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Cursor | Cursor Settings → MCP |
| Windsurf | `~/.codeium/windsurf/mcp_config.json` |
| VS Code (Copilot) | `.vscode/mcp.json` in workspace |

For other MCP clients, point them at `http://localhost:21516/mcp` (JSON-RPC 2.0 over Streamable HTTP).

Run `supercapture tools` (CLI) or send a `tools/list` request to see all available tools.

## Updating

Supercapture checks for updates automatically. You can also check manually via the app menu: **Supercapture → Check for Updates...**

All browser extensions update automatically with the app. After an app update, reload the extension in your browser's extension manager to pick up the new version.
