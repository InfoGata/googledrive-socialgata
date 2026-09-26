# Google Drive Plugin for SocialGata

A SocialGata sync plugin that enables cloud synchronization of your favorites using Google Drive.

## Features

- Sync your SocialGata favorites to Google Drive
- Stored in the hidden app data folder, so it doesn't clutter your Drive
- OAuth2 authentication with automatic token refresh
- Cross-device synchronization
- Optionally use your own Google OAuth client

## Installation

### From URL (Recommended)

Install the plugin in SocialGata by providing the manifest URL:
```
https://cdn.jsdelivr.net/gh/InfoGata/googledrive-socialgata@latest/manifest.json
```

### Manual Installation

1. Clone this repository
2. Install dependencies: `npm install`
3. Build: `npm run build`
4. In SocialGata, add the plugin from the `dist/` folder

## Configuration

No setup is needed: go to SocialGata Settings → Cloud Sync, select this plugin
and connect your Google account.

The default client exchanges and refreshes tokens through the InfoGata token
service, which holds its client secret. Its authorized redirect URIs must include
`<socialgata origin>/login_popup.html` for every origin SocialGata is served from
(e.g. `http://localhost:3005/login_popup.html`).

### Using your own OAuth client

1. Go to the [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
2. Enable the Google Drive API
3. On the OAuth consent screen, add the `https://www.googleapis.com/auth/drive.appdata` scope
4. Create an OAuth client ID of type "Web application"
5. Add `<socialgata origin>/login_popup.html` as an authorized redirect URI (the plugin options page shows the exact value)
6. Enter the Client ID and Client Secret in the plugin options and click Save
7. Connect from SocialGata Settings → Cloud Sync

With your own client, tokens are requested directly from Google instead of the token service.

## Development

### Prerequisites

- Node.js 18+
- npm

### Setup

```bash
npm install
```

### Build

```bash
npm run build
```

This runs two builds:
- `npm run build:options` - Builds the options UI page
- `npm run build:plugin` - Builds the main plugin script

### Output

- `dist/index.js` - Main plugin script
- `dist/options.html` - Options/settings page

## Plugin API Methods

| Method | Description |
|--------|-------------|
| `onSyncUpload` | Upload document data to Google Drive |
| `onSyncDownload` | Download document data from Google Drive |
| `onLogin` | OAuth2 login flow |
| `onLoginCallback` | Exchange the authorization code for tokens |
| `onLogout` | Revoke and clear authentication |
| `onIsLoggedIn` | Check login status |

## License

MIT
