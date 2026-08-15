# GSit — sit, lay, and crawl

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11  
**Applies to:** `GSit` (`GSit-3.5.1.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

**GSit** lets players sit on stairs/slabs/carpets (right-click), sit on other players, and use pose commands (`/lay`, `/crawl`, etc.). It is server-side only — no client mod. Hangar/Modrinth list support through **Paper 26.2**.

Source: https://hangar.papermc.io/Gecolay/GSit  
Source: https://modrinth.com/plugin/gsit  
Source: `dev/mod-list.md`

## Players

Most sit/pose nodes are **default-allowed** by the plugin. If a command fails with a permission message, ask an op to grant the matching `GSit.*` node in **LuckPerms**.

Source: https://hangar.papermc.io/Gecolay/GSit

### Sit by clicking

With an **empty main hand**, right-click the top of:

- stairs, slabs, carpets (including wool / moss / pale moss carpets)
- snow

Only the **bottom** half of stairs/slabs counts (`bottom-part-only: true`). Click-to-sit is on by default; turn it off with `/sit toggle`.

Source: `server/plugins/GSit/config.yml` (`Options.Sit`)  
Source: https://hangar.papermc.io/Gecolay/GSit

### Sit on players

Right-click another player (empty main hand) to sit on them / stack. Sneak ejects passengers (`sneak-ejects: true`). Toggle with `/sit playertoggle`.

Source: `server/plugins/GSit/config.yml` (`Options.PlayerSit`)

### Commands

| Command | Purpose |
|---------|---------|
| `/sit` (`/gsit`) | Sit on the block you are on / looking at |
| `/lay` (`/glay`) | Lie down |
| `/bellyflop` (`/gbellyflop`) | Bellyflop pose |
| `/spin` (`/gspin`) | Spin pose |
| `/crawl` (`/gcrawl`) | Crawl |
| `/sit toggle` | Toggle click-to-sit on blocks |
| `/sit playertoggle` | Toggle click-to-sit on players |

Stand up with **sneak** (`get-up-sneak: true`). Taking damage does **not** force stand (`get-up-damage: false`).

Source: https://hangar.papermc.io/Gecolay/GSit  
Source: `server/plugins/GSit/config.yml`

**Note:** Upstream also added `/layback` in GSit **3.0.0** (`GSit.LayBack`). It may work on **3.5.1** even if older Hangar overview text omits it — try in-game if needed.

Source: https://github.com/gecolay/GSit/releases/tag/3.0.0

### Night / phantoms

Lying down can reset rest time (`lay-rest: true`) and can count toward night skip when at least one player is in a bed (`lay-night-skip: true`). Snoring sounds are **off** on snaxcraft.

Source: `server/plugins/GSit/config.yml` (`Options.Pose`)

## Ops

### Install snapshot (live)

| Item | Value |
|------|--------|
| Jar | `server/plugins/GSit-3.5.1.jar` |
| Config | `server/plugins/GSit/config.yml` |
| Lang | `server/plugins/GSit/lang/` (default `en_us`) |
| Data | `server/plugins/GSit/data/` |

Source: `server/plugins/`  
Source: https://hangar.papermc.io/Gecolay/GSit/versions/3.5.1

### Reload

`/gsitreload` (`/gsitrl`) — needs `GSit.Reload` (ops / `GSit.*`).

Source: https://hangar.papermc.io/Gecolay/GSit

### Useful permissions

| Permission | Purpose |
|------------|---------|
| `GSit.Sit` | `/sit` |
| `GSit.SitClick` | Click blocks to sit |
| `GSit.SitToggle` | `/sit toggle` |
| `GSit.PlayerSit` | Sit on players |
| `GSit.PlayerSitToggle` | `/sit playertoggle` |
| `GSit.Lay` / `GSit.BellyFlop` / `GSit.Spin` / `GSit.Crawl` | Pose commands |
| `GSit.Reload` | Reload config |
| `GSit.*` | All |

Source: https://hangar.papermc.io/Gecolay/GSit

### snaxcraft config notes

Defaults after first run — no custom tuning yet beyond what the jar generated:

- Click sit + player sit **enabled**; empty-hand required
- `WorldBlacklist` / `WorldWhitelist` empty (all worlds)
- `trusted-region-only: false` (no GriefPrevention/PlotSquared restriction; GP is not installed)
- Command blacklist while sitting/posing: `skin`, `nick`

Source: `server/plugins/GSit/config.yml`

Edit `config.yml`, then `/gsitreload` (or full restart if reload misbehaves). Prefer restart after large permission/LuckPerms changes.

## Troubleshooting

| Symptom | Check |
|---------|--------|
| Can’t click-sit | Empty main hand; target is in `SitMaterials`; `/sit toggle` not off; permission `GSit.SitClick` |
| Can’t sit on friends | `PlayerSit.allow-sit`; `/sit playertoggle`; `GSit.PlayerSit` |
| Features dead in one world | `WorldBlacklist` / non-empty `WorldWhitelist` |
| Unsafe / mid-air sit blocked | `allow-unsafe: false` (default) |

Source: `server/plugins/GSit/config.yml`  
Source: https://hangar.papermc.io/Gecolay/GSit

## See also

- Player guide: [`guide/sit-lay-crawl.md`](../guide/sit-lay-crawl.md)
- [`gravesx.md`](gravesx.md) — death graves (separate plugin)
- [`essentialsx.md`](essentialsx.md) — homes / TPA
- `dev/mod-list.md`
