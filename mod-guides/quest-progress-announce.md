# questProgressAnnounce -- Quests progress events

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `questProgressAnnounce` (`questProgressAnnounce.jar` v1.0.1)  
**Host:** Cybrancee **Stone** (4GB) -- see `dev/host-profile.md`

## Summary

**questProgressAnnounce** is a snaxcraft-local Paper plugin that listens to Quests Classic objective updates and fires a public Bukkit event whenever an **online acting player** gains progress on an **active** quest. It does not show UI itself; consumers (e.g. **TABlistener**) bind to the event.

Hard-depends on **Quests Classic 5.3.2** only. No dependency on TAB or TABlistener.

Source: `dev/quest-progress-announce/`

## Event contract (v1)

**FQCN:** `com.snaxcraft.questprogressannounce.api.QuestProgressAnnounceEvent`

| Getter | Notes |
|--------|--------|
| `getPlayer()` | Acting player (online) |
| `getQuestId()` | Quests storage id |
| `getQuestName()` | Display name; Daily / Shared Daily board prefix stripped for toast |
| `getObjectiveLabel()` | Objective message or type name |
| `getCurrent()` | Progress after tick (>= 0) |
| `getTotal()` | Target (>= 1; no emit if invalid) |

**Emit when:** `BukkitQuesterPostUpdateObjectiveEvent` fires and progress is valid.  
**Do not emit:** for other players on shared progress; offline actors.

Source: `dev/quest-progress-announce/src/main/java/com/snaxcraft/questprogressannounce/api/QuestProgressAnnounceEvent.java`  
Source: `dev/quest-progress-announce/src/main/java/com/snaxcraft/questprogressannounce/QuesterObjectiveListener.java`

## Install

| Item | Value |
|------|--------|
| Jar | `server/plugins/questProgressAnnounce.jar` |
| Build | `powershell -NoProfile -File dev/quest-progress-announce/build-and-copy.ps1` |
| Depends | `Quests-5.3.2.jar` |
| Config | None (v1) |
| Commands | None (v1) |

Requires **full restart** after adding the jar.

## Ops notes

- Works on **any** active quest progress tick (not only compass-tracked).
- **QuestsBar** is untouched; this plugin only announces events.
- If removed, TABlistener quest binding no-ops; Quests behavior unchanged.

## Smoke

1. With Quests + questProgressAnnounce loaded, progress any active quest objective.
2. Another plugin listening on `QuestProgressAnnounceEvent` receives player, name, label, current/total (or use TABlistener boss bar binding).
3. Shared quest: only the **actor** should trigger the event, not party mates standing nearby.
4. Remove jar + restart: no events; Quests progress still works.

## See also

- TAB adapter: [`tab-listener.md`](tab-listener.md)
- QuestsBar (tracked bar): [`questsbar.md`](questsbar.md)
- Quests Classic: [`quests-classic.md`](quests-classic.md)
