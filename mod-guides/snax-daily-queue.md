# SnaxDailyQueue — daily quest auto-give

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `SnaxDailyQueue` (`SnaxDailyQueue.jar` v1.0.2)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

**SnaxDailyQueue** is a snaxcraft-local Paper plugin that reads `usercache.json`, filters an ignore list, and auto-gives **today’s 12 dailies** (8 personal + 4 shared) to known players. Online players get immediate `questadmin give`; offline players are queued via **ScheduleCommands** (`schedule add …`) for delivery on next join.

Quests **`give-at-login` is off** on dailies and Together roots (craft/smelt share leak fix). This plugin replaces login auto-give. **`/qd`** remains the backup — especially for brand-new players before they appear in usercache.

Source: `dev/mod-list.md`

## Players

- After your **first join**, your name lands in `usercache.json`. SnaxDailyQueue assigns today’s board on the **7:00 PM Pacific** flip and on periodic catch-up ticks. Unfinished dailies from the previous board are **quit** at that flip (and on join / plugin enable if you were already holding them).
- If dailies are missing (first visit, rename edge case, or before a catch-up tick), open **`/qd`** and take them manually — same board as auto-give.
- Shared dailies still show as shared on the board; cross-player personal progress no longer leaks via login give.

Source: `guide/snaxcraft-dailies.md`

## Ops

### Install (local build)

| Item | Value |
|------|--------|
| Jar | `server/plugins/SnaxDailyQueue.jar` (build: `mvn -f dev/snax-daily-queue/pom.xml package`; copy from `dev/snax-daily-queue/target/SnaxDailyQueue.jar`) |
| Config | `server/plugins/SnaxDailyQueue/config.yml` |
| Board catalog | `server/plugins/SnaxDailyQueue/boards.json` (generated — do not hand-edit) |
| Source | `dev/snax-daily-queue/` |

Source: `dev/snax-daily-queue/pom.xml`

### Depends on ScheduleCommands

Offline delivery requires **ScheduleCommands** (`ScheduleCommands.jar`). SnaxDailyQueue dispatches:

```text
schedule add <player> questadmin give {player} <quest display name>
```

Online path uses `questadmin give <player> <quest display name>` directly. Quest names must match Quests `name:` fields (same strings as `/qd` panels).

Source: `dev/snax-daily-queue/src/main/java/com/snaxcraft/dailyqueue/DailyAssigner.java`  
Source: https://modrinth.com/plugin/schedulecommand  
Source: https://hangar.papermc.io/elektroeule/ScheduleCommands

### Commands

| Command | Alias | Purpose |
|---------|-------|---------|
| `/snaxdailyqueue run` | `/sdq run` | Force one assignment tick now |
| `/snaxdailyqueue reload` | `/sdq reload` | Reload `config.yml` + `boards.json` |

Permission: `snaxdailyqueue.admin` (default op).

Source: `dev/snax-daily-queue/src/main/resources/plugin.yml`

### Config (`config.yml`)

| Key | Default | Meaning |
|-----|---------|---------|
| `usercache-path` | `usercache.json` | Relative to server root |
| `boards-file` | `boards.json` | Relative to plugin data folder (or server root); generated display names |
| `catch-up-interval-minutes` | `180` | Re-run assignment every 3 hours |
| `timezone` | `America/Los_Angeles` | Board flip timezone |
| `board-flip-local-time` | `"19:00"` | Daily reset instant (matches Quests planner) |
| `ignore` | `[]` | Case-insensitive names to skip (alt accounts, bots) |
| `clear-daily-done-on-flip` | `true` | On board index change, strip `snax_done_*` from CommandPanels `data.yml` (keep `snax_qc_*` for `/qc`) |
| `commandpanels-data-file` | `plugins/CommandPanels/data.yml` | Path to CP player data (server-root relative) |

Source: `server/plugins/SnaxDailyQueue/config.yml`  
Source: `dev/snax-daily-queue/src/main/resources/config.yml`

### Regenerate `boards.json`

After changing `dev/daily-boards.json` or re-running daily quest generators:

```powershell
powershell -NoProfile -File dev/scripts/gen-snax-daily-queue-boards.ps1
```

`gen-daily-quests.ps1` calls this at the end so board swaps stay in sync with Quests YAML and CommandPanels `/qd` panels.

Source: `dev/scripts/gen-snax-daily-queue-boards.ps1`  
Source: `dev/scripts/gen-daily-quests.ps1`

### Deploy checklist (with Quests changes)

When pushing dailies + auto-give together:

1. `SnaxDailyQueue.jar` + `plugins/SnaxDailyQueue/**`
2. Regenerated `Quests/storage/quests.yml` (`give-at-login: false` on dailies / Together roots)
3. Full restart (new jar) or `/snaxdailyqueue reload` + `/questadmin reload` as appropriate
4. Smoke: `/snaxdailyqueue run` — log shows board index + player count; verify no personal craft leak between two accounts

## Troubleshooting

| Symptom | Check |
|---------|--------|
| No auto-give at all | Plugin loaded? `boards.json` present? `/snaxdailyqueue run` console log |
| Offline player never gets dailies | ScheduleCommands loaded? Confirm live jar syntax is `schedule add <player> <command..>` |
| Wrong board leftover in `/q` | v1.0.2+ quits `dailyP*`/`dailyS*` not on today's board. `/sdq run` while online, or relog. Planner does **not** auto-quit. |
| Wrong board quests given | Regenerate `boards.json`; epoch must match `dev/daily-boards.json` |
| Alt still gets dailies | Add name to `ignore` in config; `/snaxdailyqueue reload` |
| New player has no dailies | Expected until first join + usercache entry — use `/qd` |
| Personal progress still shared | Confirm `give-at-login: false` in live `quests.yml`; restart if stale |

## See also

- Player dailies: [`guide/snaxcraft-dailies.md`](../guide/snaxcraft-dailies.md)
- `/qd` panels: [`commandpanels.md`](commandpanels.md)
- Quests Classic: [`quests-classic.md`](quests-classic.md)
- ScheduleCommands: https://modrinth.com/plugin/schedulecommand
- `dev/mod-list.md`
