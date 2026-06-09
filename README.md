# Miku - Discord Auto Quest

![JavaScript](https://img.shields.io/badge/JavaScript-Standalone-f7df1e?style=for-the-badge&logo=javascript&logoColor=111)
![Discord](https://img.shields.io/badge/Discord-Quest%20Helper-5865f2?style=for-the-badge&logo=discord&logoColor=white)
![Licence](https://img.shields.io/badge/Licence-MIT-38d9d0?style=for-the-badge)

Miku is a sleek Discord Quest automation script with a full in-client dashboard. Drop it into Discord, pick the quests you want, and watch Miku track progress, handle supported quest types, and keep the UI tidy while it works.

It is built as a single self-contained JavaScript file: no build step, no dependencies, no setup ceremony.

> Use at your own risk. This script interacts with Discord's private client internals. Automating client behaviour may violate Discord's Terms of Service and can put your account at risk.

## What Makes It Nice

- Clean draggable dashboard that lives inside Discord
- Quest picker before anything starts, so you stay in control
- Reward filters for in-game items, avatar decorations, orbs, and other rewards
- Live task cards with progress bars, statuses, logs, and claim buttons
- Video, game, stream, activity, and achievement quest handling
- Optional auto-enrol before each quest
- Optional auto-claim after completion, with fallback when Discord asks for captcha/manual action
- Rate-limit-aware request queue with jittered retries and backoff
- Cleanup hooks for patched stores, listeners, stream metadata, and fake activity state
- Saved dashboard position through `localStorage`

## Preview In Words

When Miku starts, it opens a compact control panel in Discord. You choose the quests, filter by reward type, toggle auto-enrol or auto-claim, then press `START`. Miku queues the work, shows each quest as a card, updates progress as it goes, and leaves a manual claim button when a reward cannot be claimed automatically.

## Project Structure

```text
.
|-- script.js   # Main Miku quest automation script
|-- LICENSE     # MIT licence
`-- README.md   # Project documentation
```

## Requirements

- Discord desktop or browser client
- Active, incomplete Discord Quests
- DevTools console access

No package manager is required. If you can open Discord and paste JavaScript into the console, you have everything needed to run the script.

## Quick Start

1. Open Discord.
2. Open DevTools.
3. Go to the Console tab.
4. Paste the contents of `script.js`.
5. Press Enter.
6. Select your quests in the Miku picker.
7. Click `START`.

## Controls

| Control | What It Does |
| --- | --- |
| `START` | Runs the selected quests. |
| `SELECT ALL` / `DESELECT ALL` | Toggles visible quests in the picker. |
| Reward filters | Shows or hides quests by reward type. |
| `Auto-enrol in quests` | Enrols each quest just before running it. |
| `Auto-claim rewards` | Tries to claim completed rewards automatically. |
| `CLAIM REWARD` | Manually claims a completed quest reward. |
| `GO TO QUESTS` | Opens the quest area when an achievement needs user action. |
| `STOP` | Stops Miku and runs cleanup. |
| `HIDE` | Hides the dashboard. |
| `Shift + .` | Toggles dashboard visibility. |

## Supported Quest Types

| Quest Type | How Miku Handles It |
| --- | --- |
| Video | Sends timed video progress updates until the target duration is reached. |
| Game | Temporarily patches Discord's running game store to simulate a game session. |
| Stream | Temporarily patches stream metadata to simulate a stream session. |
| Activity | Sends heartbeat updates through an available voice/private channel context. |
| Achievement | Attempts heartbeat completion first, then falls back to action-required tracking. |

## Configuration

Safe user-editable settings live near the top of `script.js`:

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

Useful tweaks:

- Change `THEME`, `SUCCESS`, `WARN`, or `ERR` to customise dashboard colours.
- Set `HIDE_ACTIVITY` to `true` if you want to suppress fake activity RPC status where supported.
- Increase `MAX_LOG_ITEMS` if you want a longer dashboard log history.

## Troubleshooting

| Problem | Likely Fix |
| --- | --- |
| `Webpack chunk not found` | Run the script inside Discord, not another page. |
| `Core modules not found` | Reload Discord and try again. Discord internals may have changed. |
| No quests appear | There may be no active, incomplete, non-expired quests available. |
| Activity quest fails | Miku needs an available private or guild voice channel context. |
| Auto-claim fails | Discord may require captcha or manual confirmation. Use `CLAIM REWARD`. |
| Dashboard is hidden | Press `Shift + .` or rerun after stopping/reloading Discord. |
| A quest gets skipped | It may be expired, region-restricted, removed, or returning a client error. |

## Notes For Users

- Miku does not need your token pasted anywhere.
- Miku runs in the current Discord session through client internals.
- Discord updates can break module lookup or quest behaviour without warning.
- Some quests still require real user action, especially achievement-style activity quests.
- Captcha-protected rewards cannot be bypassed by this script.

## Safety

This project is provided for educational and experimental use. It modifies client-side Discord state and calls Discord quest endpoints from inside the logged-in client session.

- Do not use it on accounts you cannot afford to lose.
- Do not assume it will survive Discord updates.
- Do not expect support for every quest type or reward flow.
- Use the `STOP` button before rerunning when possible.

## Licence

MIT License. See `LICENSE` for details.

Copyright (c) 2026 Ntureyc.
