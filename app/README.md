# DesertLink Companion - Extension Support

## Overview
This Electron app supports browser extensions for enhanced map functionality. The extension support is configured to work with the `extensions/fmg` folder.

## Extension Configuration

### Supported Extensions
- **fmg** - Enhanced mapgenie.io features (already present in `app/extensions/fmg`)

### How It Works
1. Extensions are loaded automatically when the app starts
2. The extension manifest (`manifest.json`) is read to determine extension name and version
3. Extensions use `session.loadExtension()` API for compatibility across Electron versions

## Extension Structure
```
app/extensions/
  └── fmg/              # Your extension folder
      ├── manifest.json # Extension configuration
      ├── background.js # Background service worker
      ├── popup.html    # Extension popup UI
      ├── icon/         # Extension icons (16, 32, 64, 128 px)
      └── content-scripts/ # Content scripts for map pages
```

## Adding New Extensions
1. Create a new folder under `app/extensions/`
2. Add a `manifest.json` with proper configuration
3. Ensure all required files are present
4. Restart the app to load the extension

## Extension Manifest Format
```json
{
  "manifest_version": 3,
  "name": "extension-name",
  "version": "1.0.0",
  "host_permissions": ["*://target.com/*"],
  "web_accessible_resources": [...],
  "permissions": [...]
}
```

## Development Notes
- Extensions are loaded using `session.loadExtension()` API
- Each window gets its own extension instance
- Extension loading is non-blocking for app startup
- Console logs will show extension load status

## Build Configuration
The app uses Electron v32+ for modern webPreferences.extensions support, but also supports older versions via session API.