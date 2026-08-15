# SnaxQuestList — grouped `/ql`

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `SnaxQuestList` (`SnaxQuestList.jar` v1.0.0)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

QuestsGUI’s stock list uses a hash set, so personal tips and **Together** (shared) quests appear mixed. **SnaxQuestList** replaces `/ql` and `/quests list` with a chest that shows **personal first**, then a **Together** separator, then shared goals. Click still offers the quest (same as QuestsGUI take).

Source: `dev/snax-quest-list/`  
Source: `server/plugins/QuestsGUI/config.yml` (`command.list.enable: false`)

## Players

- `/ql` or `/quests list` — takeable quests only (locked tips stay hidden when Quests `ignore-locked-quests` is on).
- Personal story tips first; shared **Together** (and Shared Dailies if they ever appear) after the gray **Together** pane.

## Ops

| Item | Value |
|------|--------|
| Jar | `server/plugins/SnaxQuestList.jar` (build: `mvn -f dev/snax-quest-list/pom.xml package`) |
| Config | `plugins/SnaxQuestList/config.yml` — `shared-at-end`, `show-separator`, `click-lore` |
| QuestsGUI | Keep `command.list.enable: false` so the hash-ordered GUI does not reopen |

Needs a **full restart** to load the new jar (or plugman if you use it). Then smoke `/ql`.

Source: `dev/snax-quest-list/src/main/resources/config.yml`
