# SnaxQuestTrack — `/q` click to toggle compass track

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `SnaxQuestTrack` (`SnaxQuestTrack.jar` v1.0.3)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

Left-click a quest icon in the QuestsGUI journal (`/q`) to **set** Quests Classic compass track; click the **same** tracked quest again to **clear**. Journal stays open; short chat confirm. Requires `quests.compass`. Clearing track also **hides the QuestsBar** objective bar (QuestsBar otherwise falls back to a random active quest).

Source: `dev/snax-quest-track/`  
Source: https://browsit.gitbook.io/questsgui/quest-journal  
Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions

## Depends

Hard-depend: **Quests** 5.3.2 + **QuestsGUI** 2.2.1. Soft-depend: **QuestsBar** 3.0 (boss-bar hide on clear).

## Players

| Action | Result |
|--------|--------|
| `/q` → left-click quest | Track that quest (TAB / QuestsBar / compass) |
| `/q` → left-click same tracked quest | Clear track **and hide objective boss bar** |
| Compass / `/track` | Still work as backups (compass left-click clear → bar hides within ~1s) |

## Ops

1. Build: `powershell -NoProfile -File dev/snax-quest-track/build-and-copy.ps1`
2. Push one path: `powershell -NoProfile -File scripts/sftp-push.ps1 -Paths 'plugins/SnaxQuestTrack.jar'`
3. Full restart (new jar + depends).
4. Config: `plugins/SnaxQuestTrack/config.yml` — `journal-title` must match Quests `journalTitle` (en-US: `Quest Journal`).

## Notes

Kill/tame stages count as locatable in Quests Classic even with no coords. v1.0.2 always `setCompassTarget` before `updateCompass` so QuestsBar moves when no nearby mob (e.g. We Need to Go Deeper).

Quests Classic `takeQuest` always retargets the compass (chain reward `questadmin give`, `/qd`, `/ql` take). v1.0.3 snapshots the previous track on PreStart and restores it when that quest is still active. Completing the *tracked* quest still lets the next chain step become tracked.

Source: Quests 5.3.2 `BukkitQuester.takeQuest` (`setCompassTarget` before `BukkitQuesterPostStartQuestEvent`)

## Smoke

1. Have 2+ active quests; `/q`; left-click A → chat + boss bar/TAB.
2. Left-click A again → cleared; **boss bar gone** (not swapped to another quest).
3. Left-click B → switches.
4. Track a kill-only quest with no nearby mobs (e.g. We Need to Go Deeper) → boss bar title switches immediately.
5. `/ql` click-to-take unchanged.
6. Track quest A; complete a *different* chain quest (e.g. Monster Hunter while tracking something else) -> TAB/QuestsBar stay on A (Take Aim starts, but does not steal track).
7. Track Monster Hunter; complete it -> Take Aim may become tracked (previous compass was cleared).

## Related

- [`questsbar.md`](questsbar.md)
- [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md)
