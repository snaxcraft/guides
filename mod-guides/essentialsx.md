# EssentialsX — co-op homes, warps, and QoL

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11 (`/kit quest` for QuestsBar)  
**Applies to:** `Essentials` (`EssentialsX-2.22.0.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

EssentialsX adds everyday co-op commands: **homes**, **TPA**, **warps**, **kits**, MOTD, AFK, and admin QoL. snaxcraft runs the **core** jar only (no Chat / Spawn / Protect / Discord modules in `server/plugins/` as of last sync).

Hangar lists **2.22.0** against Paper through **26.1.2**. On **26.2** it may log an unsupported-version warning while still loading — watch console after updates.

Source: https://essentialsx.net/wiki/Home.html  
Source: https://hangar.papermc.io/EssentialsX/Essentials/versions/2.22.0  
Source: `dev/mod-list.md`

## Players

Commands need the matching **LuckPerms** permission (ops usually have everything). If a command says you lack permission, ask an op — not a missing plugin.

Command index: https://essentialsx.net/commands  
Permissions index: https://essentialsx.net/permissions

### Homes

| Command | Purpose |
|---------|---------|
| `/sethome [name]` | Set a home (default name if omitted) |
| `/home [name]` | Teleport to a home |
| `/delhome [name]` | Delete a home |
| `/homes` | List your homes |

**snaxcraft config:** multiple-home ranks in config are `default: 3`, `vip: 5`, `staff: 10` — players still need `essentials.sethome.multiple` (and the rank node) to use more than one. If you have no home, `/home` can send you to spawn (`spawn-if-no-home: true`).

Source: https://essentialsx.net/wiki/Home.html  
Source: `server/plugins/Essentials/config.yml` (`sethome-multiple`, `spawn-if-no-home`)

### Teleport requests (TPA)

| Command | Purpose |
|---------|---------|
| `/tpa <player>` | Ask to teleport **to** them |
| `/tpahere <player>` | Ask them to teleport **to you** |
| `/tpaccept` / `/tpdeny` | Accept / deny |
| `/tpacancel` | Cancel your pending request |

**snaxcraft:** `tpa-accept-cancellation: 120` (seconds), `tpa-max-requests: 5`. Teleport **cooldown** and **delay** are both `0` (instant, no wait). After a command teleport you get **4** seconds of invulnerability (`teleport-invulnerability`).

Source: https://essentialsx.net/commands  
Source: `server/plugins/Essentials/config.yml`

### Warps and spawn

| Command | Purpose |
|---------|---------|
| `/warp <name>` | Go to a server warp |
| `/warps` | List warps |
| `/spawn` | Go to spawn (if set / permitted) |
| `/back` | Return to prior location / death point (if permitted) |

Ops create warps with `/setwarp <name>` and remove with `/delwarp <name>`.

`spawn-on-join` is **false** — joining does not force-teleport everyone to spawn.

Source: https://essentialsx.net/commands  
Source: `server/plugins/Essentials/config.yml` (`spawn-on-join`)

**Note:** Full first-join / group spawn control is an **EssentialsX Spawn** module feature. That module jar is **not** installed on snaxcraft right now; do not assume `/setspawn <group>` works until Spawn is added.

Source: https://essentialsx.net/wiki/Module-Breakdown.html  
Source: `dev/mod-list.md`

### Kits

| Command | Purpose |
|---------|---------|
| `/kit` | List kits you can use |
| `/kit <name>` | Claim a kit |

Defined in `plugins/Essentials/kits.yml`. Default kit **`tools`**: stone sword/shovel/pick/axe, **10s** delay between claims. Other example kits (`dtools`, `notch`, …) exist in the file — gate them with LuckPerms (`essentials.kits.<name>`).

| Command | Purpose |
|---------|---------|
| `/kit quest` | Named **Quest Compass** for QuestsBar / Classic track (**60s** cooldown). Right-click cycles active quest; left-click resets. Permission: `essentials.kits.quest`. |

Config also sets newbie kit name to `tools` (first-join kit behavior is strongest with the Spawn module; see note above).

Source: https://wiki.ess3.net/wiki/Kits  
Source: `server/plugins/Essentials/kits.yml`  
Source: `server/plugins/Essentials/config.yml` (`newbies.kit`)  
Source: https://essentialsx.net/permissions

### MOTD, list, AFK

On join, players see `plugins/Essentials/motd.txt` (welcome, `/help`, `/list`, online count, world time).

| Command | Purpose |
|---------|---------|
| `/list` | Who is online |
| `/afk` | Toggle AFK (if permitted) |
| `/msg <player> …` / `/r` | Private message / reply |

**Auto-AFK:** after **300** seconds idle if the player has `essentials.afk.auto`. Kick-on-AFK timeout is **disabled** (`auto-afk-timeout: -1`).

Source: `server/plugins/Essentials/motd.txt`  
Source: `server/plugins/Essentials/config.yml` (`auto-afk`, `auto-afk-timeout`)  
Source: https://essentialsx.net/commands

## Ops

### Files on snaxcraft

| Path | Role |
|------|------|
| `server/plugins/EssentialsX-2.22.0.jar` | Core plugin |
| `server/plugins/Essentials/config.yml` | Main settings |
| `server/plugins/Essentials/kits.yml` | Kits |
| `server/plugins/Essentials/motd.txt` | Join MOTD |
| `server/plugins/Essentials/userdata/` | Per-player data |
| `server/plugins/Essentials/worth.yml` | Economy worth (unused for play) |

Reload after safe edits: `/essentials reload` (or restart). Prefer editing while few players are online.

Source: https://essentialsx.net/wiki/Home.html

### LuckPerms + VaultUnlocked

Permissions are granted with **LuckPerms**. **VaultUnlocked** provides the Vault API bridge (economy/permissions hooks). Give co-op players only what you want (homes/TPA/warps/kits), not `essentials.*`.

Useful starter nodes (verify on https://essentialsx.net/permissions ):

- `essentials.home`, `essentials.sethome`, `essentials.delhome`, `essentials.homes`
- `essentials.tpa`, `essentials.tpahere`, `essentials.tpaccept`, `essentials.tpdeny`
- `essentials.warp`, `essentials.warps`, `essentials.spawn`, `essentials.back`
- `essentials.kit`, `essentials.kits.tools`
- `essentials.msg`, `essentials.list`, `essentials.motd`, `essentials.afk` / `essentials.afk.auto`

Source: https://essentialsx.net/permissions  
Source: https://essentialsx.net/wiki/Module-Breakdown.html  
Source: `dev/mod-list.md`

### GravesX + `essentials.keepinv` (admins)

**GravesX will not create a grave** if Essentials keeps the inventory on death. That happens when the player has `essentials.keepinv` — including from:

- `essentials.*` or `*` on an admin/staff group
- Bukkit **OP** (many Essentials nodes default to op)

Vanilla `/gamerule keepInventory true` also blocks graves — keep it **false** per world.

Source: https://github.com/EssentialsX/Essentials/issues/2920  
Source: https://github.com/Legoman99573/GravesX/wiki/FAQ  
Source: https://essentialsx.net/permissions

**Fix (LuckPerms):** explicitly set the node to **false**. An exact `false` overrides wildcards like `essentials.*` / `*`.

Source: https://luckperms.net/wiki/Command-Usage  
Source: https://github.com/EssentialsX/Essentials/issues/2920

#### 1) Find the admin group / confirm the node

```text
/lp listgroups
/lp user <YourName> info
/lp user <YourName> permission check essentials.keepinv
/lp user <YourName> permission check essentials.keepxp
```

If check says `true` (from `essentials.*`, `*`, or op defaults), graves will skip for that player.

Source: https://luckperms.net/wiki/Command-Usage

#### 2) Deny keep-inventory for the admin group (preferred)

Replace `admin` with your real staff group name from `/lp listgroups`:

```text
/lp group admin permission set essentials.keepinv false
/lp group admin permission set essentials.keepxp false
```

`keepxp` is optional but recommended so death XP can go into graves the same way as items.

Source: https://github.com/EssentialsX/Essentials/issues/2920  
Source: https://essentialsx.net/permissions  
Source: [`mod-guides/gravesx.md`](gravesx.md)

#### 3) Or deny per admin user

```text
/lp user <AdminName> permission set essentials.keepinv false
/lp user <AdminName> permission set essentials.keepxp false
```

Repeat for each admin who should get graves.

Source: https://github.com/EssentialsX/Essentials/issues/2920

#### 4) Verify, then test

```text
/lp user <AdminName> permission check essentials.keepinv
```

Expect **false**. Die with items in inventory (not empty). You should get a grave, not full keep-inventory.

If it still keeps items: confirm `/gamerule keepInventory` is `false` in that world, then `/graves debug 2` and die again (see Graves guide).

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ  
Source: `server/plugins/LuckPerms/config.yml` (`enable-ops: true` — Bukkit OP still possible; LP `false` still negates Essentials keepinv when LuckPerms is the permission provider)

**Do not** remove `essentials.*` just for this — the targeted `false` nodes are enough. Long-term, prefer staff groups with explicit nodes over bare `/op` + `*`.

Source: https://luckperms.net/wiki/Usage

### Common admin commands

| Command | Purpose |
|---------|---------|
| `/setwarp <name>` / `/delwarp <name>` | Manage warps |
| `/sethome` (others) / `/home <player>:<name>` | Manage others’ homes (with perms) |
| `/tp <player>` / `/tphere <player>` | Direct teleport |
| `/god`, `/fly`, `/heal`, `/feed` | Admin QoL (permission-gated) |
| `/kick`, `/mute`, `/ban` | Moderation (prefer clear co-op policy) |
| `/essentials` | Plugin status / subcommands |
| `/createkit` | Build a kit from inventory |

Full list: https://essentialsx.net/commands

Source: https://essentialsx.net/wiki/improvements  
Source: https://essentialsx.net/commands

### snaxcraft values worth knowing

| Setting | Value | Meaning |
|---------|-------|---------|
| `teleport-cooldown` | `0` | No wait between teleports |
| `teleport-delay` | `0` | No warm-up / move-cancel window |
| `teleport-invulnerability` | `4` | Brief post-TP protection |
| `teleport-safety` | `true` | Avoid unsafe landings when possible |
| `sethome-multiple.default` | `3` | Rank cap (needs multi-home perms) |
| `spawn-on-join` | `false` | No force spawn on join |
| `disabled-commands` | (empty examples) | Nothing disabled by default |
| `starting-balance` | `0` | Economy unused for play |

Source: `server/plugins/Essentials/config.yml`

## Installed but unused / don’t lean on yet

These exist in EssentialsX or config stubs but are **not** a snaxcraft gameplay pillar:

| Area | Why skip for now |
|------|------------------|
| **Economy / shops / worth** | VaultUnlocked is installed, but no shop workflow; `starting-balance: 0`; don’t open `/sell` / sign shops without a plan |
| **Jail** | Moderation jail system — unused for small co-op trust |
| **Nicknames / heavy chat** | No EssentialsX Chat module installed |
| **Protect / AntiBuild** | Modules not installed; creeper grief is handled elsewhere if at all |
| **Discord / GeoIP / XMPP** | Modules not installed |
| **EssentialsX Spawn** | Not installed — limited first-join/spawn group features |

Source: https://essentialsx.net/wiki/Module-Breakdown.html  
Source: `dev/mod-list.md`  
Source: `server/plugins/Essentials/config.yml`

## Troubleshooting

| Symptom | What to try |
|---------|-------------|
| “No permission” | Grant nodes in LuckPerms; ops bypass most checks |
| `/home` does nothing useful | Set a home first; or expect spawn if `spawn-if-no-home` |
| Warps missing | `/warps`; create with `/setwarp`; check `essentials.warp` / per-warp nodes |
| Kit denied | `essentials.kit` + `essentials.kits.<name>`; check delay in `kits.yml` |
| Admin dies with full keep-inv / **no GravesX grave** | Deny `essentials.keepinv` (and usually `essentials.keepxp`) via LuckPerms — see [GravesX + essentials.keepinv](#gravesx--essentialskeepinv-admins) |
| Unsupported / version warning on 26.2 | Expected until EssentialsX lists 26.2; confirm plugin still enables; watch Hangar for a newer build |
| Spawn/group spawn broken | Install matching **EssentialsX Spawn** module or use vanilla spawn only |
| Module mismatch after update | Update **all** EssentialsX jars to the **same** version |

Source: https://hangar.papermc.io/EssentialsX/Essentials/versions/2.22.0  
Source: https://essentialsx.net/wiki/Home.html  
Source: https://essentialsx.net/wiki/Module-Breakdown.html

## Related on this server

- Plugin inventory: `dev/mod-list.md`
- Permissions: LuckPerms (`LuckPerms-Bukkit-5.5.71.jar`)
- Vault bridge: VaultUnlocked (`VaultUnlocked-2.20.2.jar`)
- Live map (separate plugin): `mod-guides/bluemap.md`
- Death graves: [`gravesx.md`](gravesx.md) / player [`guide/death-graves.md`](../guide/death-graves.md) — admins need `essentials.keepinv` **false** (see section above)
- Sit/lay: `mod-guides/gsit.md`

## See also

- Wiki home: https://essentialsx.net/wiki/Home.html  
- Commands: https://essentialsx.net/commands  
- Permissions: https://essentialsx.net/permissions  
- Modules: https://essentialsx.net/wiki/Module-Breakdown.html  
- Hangar 2.22.0: https://hangar.papermc.io/EssentialsX/Essentials/versions/2.22.0  
- Kits wiki: https://wiki.ess3.net/wiki/Kits  
