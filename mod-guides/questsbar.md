# QuestsBar — objective progress boss bar

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `QuestsBar` (`QuestsBar-3.0.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

QuestsBar shows a **boss bar** for the current Quests Classic **compass-tracked** objective. Players cycle with a COMPASS (`quests.compass`). snaxcraft ships `/kit quest` and `/track` (`/qt`) for discoverability.

Source: https://www.spigotmc.org/resources/questsbar.100634/  
Source: https://pikamug.gitbook.io/quests/casual/bridge-plugins

## Install / restart

1. Jar in `plugins/QuestsBar-3.0.jar` (backup also in `purchasedMods/`).
2. **Full restart** (new jar).
3. Confirm console enables QuestsBar with Quests.

## Players

| Action | Result |
|--------|--------|
| `/kit quest` | Named Quest Compass (60s cooldown) |
| `/track` or `/qt` | Status panel + Get kit |
| Compass right-click | Cycle tracked objective + boss bar |
| Compass left-click | Reset track (SnaxQuestTrack keeps QuestsBar hidden while untracked) |
| `/q` left-click | Sets/clears track via SnaxQuestTrack; clear hides boss bar |

Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions  
Source: https://browsit.gitbook.io/questsgui/quest-journal  
Source: `server/plugins/Essentials/kits.yml`  
Source: `server/plugins/CommandPanels/panels/track.yml`  
Source: [`snax-quest-track.md`](snax-quest-track.md)

## Permissions

- `quests.compass`
- `essentials.kits.quest`

## Related

- [`quests-classic.md`](quests-classic.md)
- [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md)
