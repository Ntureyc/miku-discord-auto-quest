# Miku - Discord Auto Quest

Miku is a polished in-client helper script for Discord Quests. It injects a draggable dashboard into Discord, lets you choose which quests to run, tracks progress live, and handles supported quest types with built-in retry and cleanup logic.

> Use at your own risk. Automating Discord client behaviour may violate Discord's Terms of Service and could put your account at risk.

## Highlights

- Quest picker with selectable quests before execution
- Reward filters for in-game items, avatar decorations, orbs, and other rewards
- Support for video, game, stream, activity, and achievement-style quests
- Optional auto-enrollment for available quests
- Optional auto-claim attempt after completion
- Draggable dashboard with live progress cards and logs
- Stop and cleanup controls for patched Discord stores/listeners
- Rate-limit-aware request queue with retry/backoff behaviour
- Local UI position persistence through `localStorage`

## Repository

```text
.
|-- script.js   # Main Miku quest automation script
|-- LICENSE     # MIT licence
`-- README.md   # Project documentation
```

## Requirements

- Discord desktop or web client
- A Discord account with available Quests
- Browser/client DevTools access

No package install is required. This repository is a standalone JavaScript script.

## Usage

1. Open Discord in the desktop client or browser.
2. Open DevTools and switch to the Console tab.
3. Paste the contents of `script.js` into the console.
4. Press Enter to run it.
5. Use the Miku quest picker to select quests and options.
6. Click `START` and watch progress in the dashboard.

## Dashboard Controls

- `START` begins the selected quests.
- `DESELECT ALL` / `SELECT ALL` toggles visible quests in the picker.
- Reward filter chips show or hide quest groups by reward type.
- `Auto-enroll in quests` enrolls quests immediately before execution.
- `Auto-claim rewards` tries to claim completed rewards automatically.
- `CLAIM REWARD` appears when a quest is complete and needs manual claiming.
- `GO TO QUESTS` appears when an achievement-style quest needs user action.
- `STOP` shuts down the script and runs cleanup hooks.
- `HIDE` hides the dashboard.
- `Shift + .` toggles dashboard visibility.

## Supported Quest Types

| Quest Type | Behaviour |
| --- | --- |
| Video | Sends timed video progress updates until the target duration is reached. |
| Game | Temporarily patches Discord's running game store to simulate a game session. |
| Stream | Temporarily patches stream metadata to simulate a stream session. |
| Activity | Sends heartbeat updates through an available voice/private channel context. |
| Achievement | Attempts heartbeat completion first, then falls back to manual/action-required tracking. |

## Configuration

User-editable settings live near the top of `script.js`:

```js
const CONFIG = {
    NAME: "Miku",
    VERSION: "v4.5.2 (Enterprise)",
    THEME: "#38D9D0",
    SUCCESS: "#6EE7A8",
    WARN: "#F7C66B",
    ERR: "#FF7A8A",
    TRY_TO_CLAIM_REWARD: false,
    HIDE_ACTIVITY: false,
    MAX_LOG_ITEMS: 60
};
```

Common tweaks:

- Change `THEME`, `SUCCESS`, `WARN`, or `ERR` to customise dashboard colours.
- Set `HIDE_ACTIVITY` to `true` to suppress fake activity RPC status where supported.
- Adjust `MAX_LOG_ITEMS` to keep more or fewer dashboard log entries.

## Troubleshooting

| Problem | What to Check |
| --- | --- |
| `Webpack chunk not found` | Make sure the script is running inside Discord, not on another page. |
| `Core modules not found` | Discord internals may have changed. Reload Discord and try again. |
| No quests appear | You may have no active, incomplete, non-expired quests. |
| Activity quest fails | The script needs an available private or guild voice channel context. |
| Auto-claim fails | Discord may require captcha or manual claim confirmation. Use `CLAIM REWARD`. |
| Dashboard disappeared | Press `Shift + .` or rerun the script after stopping/reloading. |

## Safety Notes

- This script interacts with Discord's private client internals and APIs.
- Discord updates can break the script without warning.
- Automated quest completion may violate platform rules.
- Do not use this on accounts you cannot afford to lose.
- The script is provided as-is with no guarantee of reliability or account safety.

## Licence

MIT License. See `LICENSE` for details.

Copyright (c) 2026 Ntureyc.
