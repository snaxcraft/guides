# TABlistener -- event-to-TAB adapter

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-12  
**Applies to:** `TABlistener` (`TABlistener.jar` v1.0.1)  
**Host:** Cybrancee **Stone** (4GB) -- see `dev/host-profile.md`

## Summary

**TABlistener** loads YAML **bindings** that map any Bukkit event (by FQCN) to TAB display surfaces via reflection. No compile-time link to Quests or **questProgressAnnounce**; wiring is config-only.

Hard-depends on **TAB 6.1.2** only. v1 implements the **`bossbar`** feature handler (P0 spike passed); other `feature:` types are config-valid but not implemented until spiked.

Source: `dev/tab-listener/`

## Default binding (shipped in jar)

Config path inside jar: `config.yml` (extracted to plugin data folder on first run).

```yaml
bindings:
  - id: quest-progress-bossbar
    event: com.snaxcraft.questprogressannounce.api.QuestProgressAnnounceEvent
    player: getPlayer
    fields:
      questName: getQuestName
      objectiveLabel: getObjectiveLabel
      current: getCurrent
      total: getTotal
    apply:
      - feature: bossbar
        title: "{questName} - {current}/{total}"
        progress: "{current}/{total}*100"
        color: YELLOW
        style: PROGRESS
        duration-ms: 2000
```

If **questProgressAnnounce** is absent, this binding is skipped (logged once).

Source: `dev/tab-listener/src/main/resources/config.yml`

## Duration rules (`duration-ms`)

| Value | Behavior |
|-------|----------|
| **> 0** | Show/update, remove after N ms |
| **0** | Forever until replaced (same binding id + player), quit, or restart |
| **omit** | Feature default (**2000** ms for bossbar) |

New apply for same binding id + player **replaces** prior timed or forever instance (no stacking).

Source: `dev/tab-listener/src/main/java/com/snaxcraft/tablistener/DurationPolicy.java`

## TAB feature matrix (spike gate)

| `feature:` | v1 status | Notes |
|------------|-----------|-------|
| `bossbar` | **Implemented** | TAB `BossBarManager`; multi-bar OK with QuestsBar |
| `placeholder` | Not implemented | Spike required |
| `scoreboard` | Not implemented | Must restore after timed apply |
| `header_footer` | Not implemented | Spike required |
| `tablist_format` | Not implemented | Spike required |
| `layout` | Not implemented | Heavy; rare events only |
| `playerlist_objective` | **Unsupported** | Layout enabled on snaxcraft |
| `nametag` | Not implemented | Lowest priority; team restore risk |

Source: https://github.com/NEZNAMY/TAB/wiki/Developer-API

## Prerequisites

TAB **`bossbar.enabled: true`** in `server/plugins/TAB/config.yml`. Permanent config bars may stay **empty** (`bars: {}`) so only event-driven bars show.

Source: `server/plugins/TAB/config.yml`  
Source: https://github.com/NEZNAMY/TAB/wiki/Feature-guide:-Bossbar

## Install

| Item | Value |
|------|--------|
| Jar | `server/plugins/TABlistener.jar` |
| Build | `powershell -NoProfile -File dev/tab-listener/build-and-copy.ps1` |
| Depends | `TAB v6.1.2.jar` |
| Config | `plugins/TABlistener/config.yml` (default from jar) |
| Commands | None (v1) |

Requires **full restart** after adding the jar.

## Smoke (with questProgressAnnounce)

1. Progress any active quest -> actor sees a **second** boss bar (`Slay 5 Skeletons - 1/5`, no `KILL_MOB`).
2. Default `duration-ms: 2000` -> bar gone ~2s; progress again within window -> **replaces**, does not stack.
3. Set `duration-ms: 0` -> bar stays until next progress on that binding.
4. QuestsBar tracked bar still shows when a quest is compass-tracked.
5. Remove TABlistener -> no TAB flash; questProgressAnnounce events still fire (no player-visible effect).
6. Remove questProgressAnnounce -> quest binding no-ops.

## See also

- Event source: [`quest-progress-announce.md`](quest-progress-announce.md)
- QuestsBar: [`questsbar.md`](questsbar.md)
- TAB footer/sidebar: `server/plugins/TAB/config.yml`
