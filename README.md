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

## Updating

Supercapture checks for updates automatically. You can also check manually via the app menu: **Supercapture → Check for Updates...**

All browser extensions update automatically with the app. After an app update, reload the extension in your browser's extension manager to pick up the new version.
