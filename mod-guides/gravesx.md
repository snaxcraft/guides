# GravesX — death graves / death chests

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11  
**Applies to:** `GravesX` (`GravesX-2026.4.9.1.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

**GravesX** (fork of Ranull’s Graves) stores a player’s dropped items and most XP in a **grave** at a safe death location instead of scattering loot on the ground. Hangar lists Paper **1.18–26.2**. On snaxcraft the default grave is a **player head** with a hologram, lasting **3 hours** (`10800` seconds).

Source: https://hangar.papermc.io/Legoman99573/GravesX  
Source: https://hangar.papermc.io/Legoman99573/GravesX/versions/2026.4.9.1  
Source: `server/plugins/GravesX/readme.txt`  
Source: `dev/mod-list.md`

This is **plugin** behavior — not vanilla `keepInventory`. Vanilla keep-inventory and some Essentials permissions **prevent graves** (see [Ops](#ops) / [Troubleshooting](#troubleshooting)).

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

## Players

### When you die

1. Items (and stored XP) go into a grave near where you died — not a vanilla item scatter (when graves spawn successfully).
2. A hologram marks the grave (owner, time left, killer/cause).
3. On respawn you may get a **compass** (recovery compass when available) pointing to the grave for a limited time.
4. Right-click / open the grave to reclaim gear. Auto-loot can pull items into your inventory when breaking/opening (default enabled).

Source: `server/plugins/GravesX/config/grave.yml` (`grave`, `block`, `hologram`, `respawn`, `drop.auto-loot`)  
Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation

### Commands

| Command | Purpose |
|---------|---------|
| `/graves` | Open your graves GUI / manage your graves |
| `/graves help` | Plugin info |
| `/graves list [player]` | List graves (other players if permitted) |

From the GUI you can **teleport** to a grave when `teleport.enabled` is true (default on snaxcraft; delay `0` = instant).

Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation  
Source: `server/plugins/GravesX/config/grave.yml` (`teleport`)

### snaxcraft defaults (what to expect)

| Setting | Value | Meaning |
|---------|--------|---------|
| Grave lifetime | `10800` s | **3 hours**, then contents drop (timeout drop on) |
| Max graves per entity | `18` | Cap before placement rules bite |
| Block | `PLAYER_HEAD` | Visible head grave |
| Timed protection | **off** | `protection.enabled: false` — no timed “locked to owner only” window |
| Explode | `false` | Graves resist explosions |
| XP in grave | `store: 0.7` | ~**70%** of calculated XP stored in grave |
| Respawn compass | `true`, `300` s | Compass window after grave creation |
| Storage mode | `EXACT` | Inventory layout preserved; auto-loot can restore armor slots |

Source: `server/plugins/GravesX/config/grave.yml`

Empty inventories do **not** create graves.

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

## Ops

### Install snapshot (live)

| Item | Value |
|------|--------|
| Jar | `server/plugins/GravesX-2026.4.9.1.jar` |
| Config folder | `server/plugins/GravesX/config/` |
| Main grave options | `config/grave.yml` |
| Storage / integrations | `config/config.yml` (H2 DB by default) |
| Permission overrides | `config/permission.yml` (`graves.permission.*`) |
| Data | `server/plugins/GravesX/data/` |

Configs are split across YAML files and merged at load. Prefer editing the documented files; the plugin can auto-update outdated configs and back them up.

Source: `server/plugins/GravesX/readme.txt`  
Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

### Admin commands

| Command | Purpose |
|---------|---------|
| `/graves reload` | Reload configs (**preferred** over `/reload`) |
| `/graves teleport` | TP to a player’s first grave |
| `/graves purge graves` / `holograms` | Purge all graves or leftover holograms |
| `/graves purge player\|offline-player <name>` | Purge one player’s graves |
| `/graves debug <level>` | `0` off, `1` info, `2` failures (why graves don’t spawn) |
| `/graves dump` | Dump diagnostics for support |
| `/graves givetoken <player> <token> <amount>` | Give grave tokens (if tokens used) |

Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation  
Source: https://hangar.papermc.io/Legoman99573/GravesX

### Permissions (documented defaults)

| Permission | Default | Purpose |
|------------|---------|---------|
| `graves.place` | true | Create graves on death |
| `graves.open` | true | Open graves |
| `graves.break` | true | Break graves |
| `graves.teleport` | true | Teleport to own grave (GUI) |
| `graves.experience` | true | Receive XP from graves |
| `graves.autoloot` | true | Auto-loot |
| `graves.gui` | true | Use graves GUI |
| `graves.gui.other` | OP | Other players’ GUI |
| `graves.bypass` | OP | Bypass restrictions |
| `graves.reload` | OP | Reload |
| `graves.keepinventory.bypass` | false | Special keep-inventory interaction (see FAQ / changelog notes) |

Permission **overrides** for grave style/time use nodes like `graves.permission.vip` / `admin` from `permission.yml`.

Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation  
Source: `server/plugins/GravesX/config/permission.yml`  
Source: https://docs.skunity.com/addons/GravesX

### Critical: why ops / admins may not get graves

Graves **will not spawn** when inventory is kept by another system:

1. World gamerule: `/gamerule keepInventory` must be **false** per world.
2. **EssentialsX:** anyone with `essentials.keepinv` — including from `essentials.*`, `*`, or Bukkit **OP** — keeps inventory and **skips graves**.

**snaxcraft fix (LuckPerms):** keep your admin `essentials.*` grant; add an explicit deny. Full command list: [`essentialsx.md` — GravesX + keepinv](essentialsx.md#gravesx--essentialskeepinv-admins).

```text
/lp listgroups
/lp group <adminGroup> permission set essentials.keepinv false
/lp group <adminGroup> permission set essentials.keepxp false
/lp user <AdminName> permission check essentials.keepinv
```

Or per user: `/lp user <AdminName> permission set essentials.keepinv false` (and `essentials.keepxp false`).

Then die with items — expect a grave. If not: `/graves debug 2` and check console.

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ  
Source: https://github.com/EssentialsX/Essentials/issues/2920  
Source: [`mod-guides/essentialsx.md`](essentialsx.md)  
Source: `server/plugins/Essentials/config.yml` (keepinv-related settings exist; the gate is the permission)
### Tunables worth knowing (Stone / co-op)

| Goal | Where |
|------|--------|
| Longer/shorter graves | `grave.yml` → `grave.time` (`-1` = forever) |
| Owner-only lock window | `protection.enabled: true` + `protection.time` |
| Less XP loss | `experience.store` (keep ≤ `1.0`) |
| Disable compass | `respawn.compass: false` |
| Storage backend | `config.yml` → `settings.storage.type` (default **H2**; fine for 6 players) |

Source: `server/plugins/GravesX/config/grave.yml`  
Source: `server/plugins/GravesX/config/config.yml`

Integrations for plugins we **do not** run (ItemsAdder, Nexo, CoreProtect, etc.) may be enabled in `config.yml` but are inert until those jars exist. Disable noisy integrations there if console spam appears.

Source: `server/plugins/GravesX/config/config.yml` (`settings.integration`)  
Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

### Support dump

Author expects a **`/graves dump`** plus a clear repro when reporting bugs. Discord linked from plugin readme: https://discord.ranull.com/

Source: `server/plugins/GravesX/readme.txt`

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| No grave on death | Inventory not empty? `keepInventory` false? Deny `essentials.keepinv`? Run `/graves debug 2` and die again — watch console |
| Stuck hologram after loot | `/graves purge holograms`, or kill armor stands tagged `graveHologram` (see FAQ). Paper `armor-stands-tick` notes in FAQ |
| Can’t open friend’s grave | With protection off, check permissions / killer-owner rules if you later enable protection |
| Config broke after edit | Validate YAML; restore from plugin backup / regenerate per FAQ |

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

## See also

- Player guide: [`guide/death-graves.md`](../guide/death-graves.md)  
- [`gsit.md`](gsit.md) — sit/lay/crawl QoL  
- [`essentialsx.md`](essentialsx.md) — `/back`, homes; **keepinv** conflicts with graves  
- `dev/mod-list.md`
