# CommandPanels — ops

**Last verified:** 2026-08-16  
**Host:** Cybrancee **Stone** (4GB) -- see `dev/host-profile.md`  
**Jar:** Hangar **CommandPanels** build for Paper **26.1–26.2** (snaxcraft uses this — not DeluxeMenus)  
**Folder:** `server/plugins/CommandPanels/`

Source: https://hangar.papermc.io/RockyHawk/CommandPanels

## Player-facing titles

Chest `title:` strings stay short (`Dailies`, `Track`, `Tab settings`, `Quest Point Shop`, `Completed`). No board numbers or slash-commands in the GUI chrome. Ops notes belong in YAML `#` comments / this guide.

Source: `dev/scripts/gen-daily-panels.ps1`

## snaxcraft panels

| Panel / command | Role |
|-----------------|------|
| `daily` (`/daily`, `/qd`) | Today’s daily board (8 conditioned `daily-board-N.yml` files) |
| `qp` (`/qp`) | QP shop root → `qp-blocks`, `qp-eggs`, `qp-spawners`, `qp-gear` |
| `tabsettings` (`/tabsettings`, alias `/ts`) | Tab footer + player-list display toggles (see **Tab settings** below) |

Aliases in `server/commands.yml` need a **full server restart**.

## Reload

- Panels: `/pa reload` (confirm with `/pa help` on your build)
- Quests after YAML push: `/questadmin reload` — **not** Bukkit `/reload`

## Permissions

Players need CommandPanels open permission (e.g. `commandpanels.command` / `commandpanels.command.open` on `default` via LuckPerms). Do not grant reload to everyone.

## PlaceholderAPI

`/qd` board routing uses **Server** + **Math** (not Javascript — no eCloud download / broken on Java 25).

```
/papi ecloud download Server
/papi ecloud download Math
/papi reload
```

Board index (0–7), same clock as Quests planner / `dev/daily-boards.json` epoch (no colons in nested Server placeholder — Math breaks on `:`):

`%math_0_FLOOR({server_countup_raw_yyyyMMddHHmmss_20260810190000}/86400)[prc]8%`

`/qd` currently serves a copied board panel (`set-daily-active-panel.ps1`); live `[open]` router is optional after parse smoke. Requires Server expansion `time.zone: America/Los_Angeles`.

Source: https://wiki.placeholderapi.com/users/commands/  
Source: https://andre601.ch/expansions/math/  
Source: https://github.com/PlaceholderAPI/Server-Expansion  
Source: https://wiki.placeholderapi.com/placeholders/ (Javascript = NO DOWNLOAD COMMAND)

## Data keys

CommandPanels **4.2.1** console syntax (from `lang.yml`):

`/pa data <action> <player> [key] [value]`

Quest rewards use `pa data overwrite <player> snax_done_<id> 1` (dailies — `/qd` glow only) and `pa data overwrite <player> snax_qc_<id> 1` (ladder/Together for `/qc`). Dailies never write `snax_qc_*` and never appear in `/qc` panels. On daily board flip, SnaxDailyQueue strips `snax_done_*` (keeps `snax_qc_*`). The old `commandpanels data set …` string is **not** a valid command on this build — flags never wrote.

`/qc` history past completes: pull `Quests/data`, run `dev/scripts/backfill-qc-cp-data.ps1` or `write-qc-cp-data-from-quests.ps1` (ladder/Together IDs only), paste `dev/generated/qc-cp-backfill-commands.txt` in console.

Source: `server/plugins/CommandPanels/lang.yml` (`data_usage`)

## Click requirements vs item conditions

These are two different parsers on **4.2.1**. Mixing them silently breaks a panel.

| Key | Where | Syntax |
|-----|-------|--------|
| `conditions:` | item level (show/hide an item) | bare condition — `'%commandpanels_data_x% $EQUALS 1'` |
| `requirements:` | inside `left-click:` / `right-click:` | **tag first**, then the argument — `'[conditions] %quests_player_quest_points% $ATLEAST 20'` |

Every `requirements:` entry must begin with one of `[conditions]`, `[xp]`,
`[item]`, `[data]`, `[vault]`. The runner reads the first whitespace-delimited
token as the tag; anything else prints **"Unknown requirement tag"** in chat and
the click aborts — the `fail:` commands do not run either, so it looks like a
dead button.

Condition operators (valid only inside a condition string): `$EQUALS`,
`$ATLEAST`, `$HASPERM`, combined with `$AND`, `$OR`, `$NOT` and parentheses.

QP shop buy pattern:

```yaml
left-click:
  requirements:
  - '[conditions] %quests_player_quest_points% $ATLEAST 20'
  fail:
    commands:
    - '[msg] &cNot enough Quest Points (need 20).'
  commands:
  - '[console] questadmin takepoints %player_name% 20'
  - '[console] minecraft:give %player_name% grass_block 64'
```

Source: `server/plugins/CommandPanels/panels/qp-blocks-building.yml`  
Source: `server/plugins/CommandPanels/lang.yml` (`requirement_unknown_tag`)

## Tab settings

Panel: `server/plugins/CommandPanels/panels/tabsettings.yml` — title **Tab settings** (no slash in GUI title).

| Command | Notes |
|---------|-------|
| `/tabsettings` | Primary — opens the settings chest |
| `/ts` | Short alias (EssentialsX owns `/t` as tell — do not use `/t`) |

Six per-player CP data keys (missing or `1` = shown, `0` = hidden): `snax_tab_tracked`, `snax_tab_daily`, `snax_tab_shared_daily`, `snax_tab_quests`, `snax_tab_shared`, `snax_tab_players`. TAB footer reads these via PlaceholderAPI `%commandpanels_data_*%`. Panel clicks must use `[console] pa data overwrite %player_name% …` (same pattern as `/qd` quest give) — bare `pa data` runs as the player and fails without admin permission. After a data write that changes item `conditions`, use `[refresh]` (not `[open] tabsettings`) so the open panel re-parses on/off items — Source: CommandPanels `RefreshPanelTag` + https://docs.commandpanels.net/TagsPlaceholders/CommandTags

Icons (same item on/off; Shown/Hidden in lore): compass, clock, bell, book, diamond sword, player head.

**Other players + hearts:** TAB Layout (needed to hide others) is incompatible with Tablist HP hearts. `playerlist-objective` stays off while layout is on. In-world belowname hearts are unchanged.

After SFTP push: `/pa reload` on the host. For TAB: `/tab reload`.

Source: `server/plugins/CommandPanels/panels/tabsettings.yml`  
Source: `server/plugins/Essentials/config.yml` (`socialspy-commands` lists `t` for tell)
