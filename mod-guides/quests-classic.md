# Quests Classic — challenge / quest plugin

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11  
**Applies to:** `Quests` (`Quests-5.3.2.jar` — PikaMug **Quests Classic**)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

**Quests Classic** (Modrinth slug `quests.classic`) lets players take optional goals with stages, rewards, and Quest Points. On snaxcraft it is **side content** — you can ignore it and still play survival. Vanilla advancements stay on the normal **`L`** tab; they are not replaced by this plugin.

This is **not** LMBishop’s Hangar plugin also named “Quests.” Use the PikaMug jar only.

Source: https://modrinth.com/plugin/quests.classic  
Source: https://pikamug.gitbook.io/quests/  
Source: `dev/mod-list.md`

**Our challenge list:** [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md) — branched progression (starter unlock, locked tips hidden, 2 global paths).

**GUI:** [`QuestsGUI`](https://browsit.gitbook.io/questsgui/) **2.2.1** — journal `/q` chest; list GUI off. **SnaxQuestList** owns `/ql` (personal then Together).

**Player flow:** Take **Gotta Start Somewhere** (break 1 short grass) → personal roots + **Together - …** global roots given (starter rewards + `give-at-login` on the two path roots). Next steps via reward `questadmin give`. No JoinCommands.

Source: https://browsit.gitbook.io/questsgui/  
Source: https://pikamug.gitbook.io/quests/beginner/options.md  
Source: `dev/mod-list.md`  
Source: `server/plugins/Quests/config.yml`  
Source: `server/plugins/QuestsGUI/config.yml`

## Players

Default player commands (aliases **`/qs`** / **`/q`** also work):

| Command | Purpose |
|---------|---------|
| `/quests` | Plugin help |
| `/quests list [page]` | List available quests — **SnaxQuestList** chest (`/ql`); personal tips then Together |
| `/quests take <quest>` | Accept a quest |
| `/quests quit <quest>` | Abandon a quest |
| `/quest` | Current objectives |
| `/quest <quest>` | Info about a quest |
| `/quests stats` | Your quest stats |
| `/quests top [n]` | Leaderboard |
| `/quests journal` | Toggle Quest Journal (QuestsGUI chest menu) |
| `/q` | snaxcraft alias → `/quests journal` (`server/commands.yml`; needs restart) |
| `/ql` | snaxcraft alias → `/quests list` |
| `/qs` | snaxcraft alias → `/quests stats` |

Permissions for these start with `quests.` (e.g. `quests.take`). Ops usually have everything; others need LuckPerms nodes.

Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions.md  
Source: `server/commands.yml`

### How it feels on snaxcraft

1. Take **Gotta Start Somewhere**, break 1 short grass — personal branch tips **and** global Kill/Mine roots are given (shared globals; roots also use `give-at-login` after unlock).  
2. Locked personal quests stay hidden until unlocked; finishing auto-gives the next tip.  
3. Track with `/quest`. Vanilla `L` advancements stay separate.  
4. Full per-quest walkthrough: [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md).

Source: `server/plugins/Quests/storage/quests.yml`  
Source: [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md)

### Quest Points

Quest Points are a plugin currency. On snaxcraft they power the **`/qp` shop** (eggs, spawners, structure blocks, gear tiers) and are earned from **dailies** (`/daily` / `/qd`) plus a drip from the ladder. Check totals with `/quests stats`.

Player guide: [`guide/snaxcraft-dailies.md`](../guide/snaxcraft-dailies.md)  
Ops panels: [`mod-guides/commandpanels.md`](commandpanels.md)

Source: https://pikamug.gitbook.io/quests/beginner/rewards.md  
Source: `server/plugins/CommandPanels/panels/qp-shop.yml`

## Ops

### Install / version

| Item | snaxcraft |
|------|-----------|
| Jar | `Quests-5.3.2.jar` |
| Folder | `plugins/Quests/` |
| Modrinth | Lists **26.2** + Paper for 5.3.2 |
| Reload | `/questadmin reload` (alias `/qa reload`) — **not** server `/reload` |

After jar or YAML changes, prefer `/questadmin reload` or a full restart. Never use Bukkit `/reload`.

Source: https://modrinth.com/plugin/quests.classic/version/5.3.2  
Source: https://pikamug.gitbook.io/quests/setup/quests-editor.md  
Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions.md

### Important files

| Path | Role |
|------|------|
| `plugins/Quests/config.yml` | Plugin options (timeouts, max quests, journal, etc.) |
| `plugins/Quests/storage/quests.yml` | Saved quests (snaxcraft ladder) |
| `plugins/Quests/storage/actions.yml` | Actions (e.g. GiveRod) |
| `plugins/Quests/storage/conditions.yml` | Conditions |
| `plugins/Quests/lang/` | Strings / translations |

Author docs: prefer the **in-game editors** for new/changed quests; hand-editing `quests.yml` is unsupported if it breaks.

Source: https://pikamug.gitbook.io/quests/setup/configuration.md  
Source: `server/plugins/Quests/`

### snaxcraft config highlights

From live `config.yml` after sync:

| Key | Value | Notes |
|-----|-------|-------|
| `allow-command-questing` | `true` | `/quests take` works |
| `confirm-accept` | `false` | No extra confirm prompt on accept |
| `ignore-locked-quests` | `true` | Locked quests stay out of the list |
| `max-quests` | `50` | Cap on quests held at once |
| `give-journal-item` | `false` | No journal item forced into inventory |
| `show-titles` | `true` | Titles on accept/complete |
| `storage-method.player-data` | `yaml` | Flat files, not MySQL |

Source: `server/plugins/Quests/config.yml`  
Source: https://pikamug.gitbook.io/quests/setup/configuration.md

### Regenerating ladder and daily content

1. After YAML edits prefer regenerating with `dev/scripts/gen-quests-progression.ps1` then `gen-daily-quests.ps1` (backs up `quests.yml`). Progression rebuilds ladder + Together and drops generated dailies, so the daily generator must run second to merge all 108 back.
2. `/questadmin reload` or full restart. ItemStacks need `v: 4903`. Place stages need `place-block-durability` beside `place-block-names`, or Quests rejects the whole quest.
3. Do **not** install JoinCommands (Paper 26.2 unsupported). Globals unlock from the starter.
4. Branch order source of truth: `dev/quests-branch-map.json`. Global chains: `dev/quests-global-chains.json`. Reward tables: `dev/quest-item-rewards.json`. `/qc` panels: `dev/scripts/gen-qc-panels.ps1`.
5. `/qc` done icons use `pa data overwrite <player> snax_qc_<id> 1` on complete (CommandPanels 4.2.1; not PAPI `has_completed`). Past completes: `dev/scripts/backfill-qc-cp-data.ps1` then paste console output. Keep the PAPI Quests expansion updated (`/papi ecloud download Quests`) for Tab/compass placeholders.

Source: `dev/scripts/gen-quests-progression.ps1`  
Source: `dev/scripts/gen-daily-quests.ps1`  
Source: https://pikamug.gitbook.io/quests/setup/configuration.md

### Admin commands (short)

| Command | Purpose |
|---------|---------|
| `/questadmin` / `/qa` | Admin help |
| `/questadmin reload` | Reload plugin data |
| `/questadmin give <player> <quest>` | Force-take |
| `/questadmin finish <player> <quest>` | Force-complete |
| `/questadmin reset <player>` | Wipe that player’s Quests data |
| `/quests editor` | Create/edit quests (ops / `quests.editor.*`) |

Full list: https://pikamug.gitbook.io/quests/setup/commands-and-permissions.md

### Editing content

1. Prefer **`/quests editor`** in-game (chat prompts).
2. Sync with `scripts/sftp-pull.ps1` so `server/plugins/Quests/` matches the host.
3. Update [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md) when the ladder changes.
4. Push YAML only when you know the format; then `/questadmin reload` and watch console.

Source: https://pikamug.gitbook.io/quests/setup/quests-editor.md

### Stone / performance

One quest plugin is fine on **4GB Stone**. Avoid stacking Citizens NPCs, heavy bridge plugins, or large global quest spam without testing TPS. Quests Classic jar is ~5MB. YAML delay-load can still trip the watchdog -- wait for `Loaded N Quest(s)`.

Source: `dev/host-profile.md`

### Not installed (on purpose)

| Thing | Why |
|-------|-----|
| Citizens / ZNPCsPlus | NPC quest givers — not required for command quests |
| Economy money rewards | No economy plugin; ladder uses items/XP/QP only |

~~QuestsGUI~~ — **installed** (`QuestsGUI-2.2.1.jar`).

Source: `dev/mod-list.md`  
Source: https://pikamug.gitbook.io/quests/beginner/dependencies.md  
Source: https://browsit.gitbook.io/questsgui/

## Troubleshooting

| Symptom | Check |
|---------|--------|
| Unknown command | Jar in `plugins/`, restart, console enable errors |
| Can’t take quest | Requirements / LuckPerms `quests.take` |
| Progress stuck | Wrong block (e.g. deepslate vs `IRON_ORE`); `/quest` objectives |
| Reload broken | Console YAML error; restore prior `quests.yml` via SFTP |
| Confused with “other Quests” | Confirm jar is **PikaMug** `Quests-5.3.2`, not LMBishop |

Source: https://pikamug.gitbook.io/quests/setup/configuration.md  
Source: `server/plugins/Quests/storage/quests.yml`

## See also

- [`guide/snaxcraft-quests.md`](../guide/snaxcraft-quests.md) — our challenge ladder  
- [`questsbar.md`](questsbar.md) — boss-bar progress; `/track` `/qt`; `/kit quest`  
- [`mod-guides/essentialsx.md`](essentialsx.md) — homes / kits (includes `/kit quest`)  
- [`dev/mod-list.md`](../dev/mod-list.md) — installed plugins  
- Author docs: https://pikamug.gitbook.io/quests/  
- Modrinth: https://modrinth.com/plugin/quests.classic  
