# Chunky — chunk pregeneration

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-10  
**Applies to:** `Chunky` (`Chunky-Bukkit-1.5.3.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`  
**Pregen:** target sizes completed 2026-08-10 (OW 3500 / Nether 440 / End 2500)

## Summary

Chunky pre-generates terrain **before players explore**, so the server spends less time generating chunks on the fly. On snaxcraft it is already installed as a Paper (Bukkit) plugin. Prefer running large jobs from the **host console** with few or no players online.

Source: https://hangar.papermc.io/pop4959/Chunky  
Source: https://github.com/pop4959/Chunky/wiki/Pregeneration

## What it does (and does not)

- **Does:** Ask Paper to generate all chunks inside a selected region (shape + center + radius), report progress (chunks done, %, ETA, cps), and let you pause/continue/cancel tasks.
- **Does not:** Replace the vanilla world border by itself (that is vanilla `/worldborder`, or the optional **ChunkyBorder** addon — not installed on snaxcraft).
- **Safe on existing worlds:** Already-generated chunks are skipped; only missing chunks are created.

Source: https://hangar.papermc.io/pop4959/Chunky  
Source: https://github.com/pop4959/Chunky/wiki/FAQ

## snaxcraft install

| Item | Value |
|------|--------|
| Jar | `server/plugins/Chunky-Bukkit-1.5.3.jar` |
| Config folder | Created on first run under `server/plugins/Chunky/` (re-pull after first use if missing locally) |
| Level name | `world` (`server.properties` → `level-name=world`) |
| Permissions | Commands default to **op** (`chunky.command` and children) |

Source: https://github.com/pop4959/Chunky/blob/master/bukkit/src/main/resources/plugin.yml

Confirm the plugin loaded: in console type `chunky` (in-game: `/chunky`). You should see the help menu.

Source: https://github.com/pop4959/Chunky/wiki/Pregeneration

### World / dimension names

Names depend on the server and Minecraft version. Common Paper names:

| Dimension | Often named |
|-----------|-------------|
| Overworld | `world` or `overworld` |
| Nether | `world_nether` or `the_nether` |
| End | `world_the_end` or `the_end` |

On snaxcraft the world folder is `server/world/` with nested `dimensions/`. **Always verify** the exact name Chunky expects before starting a long task (use `chunky world <tab>` / selection feedback, or start a tiny test radius).

Source: https://github.com/pop4959/Chunky/wiki/Pregeneration

## Before you pre-generate

1. **Prefer empty server** — faster and avoids gameplay lag while generating.
2. **Start small** — e.g. radius `5000` first; large radii explode in chunk count and disk use.
3. **Disk + RAM** — generation is I/O and memory heavy; FAQ recommends roughly **4GB+** allocated RAM and a fast SSD. Host plan limits still apply on Cybrancee.
4. **Map plugins** — pause BlueMap (or other map renderers) during heavy Chunky pregen. snaxcraft uses **BlueMap** on Paper 26.2 (not Dynmap).
5. **Do not pause the server/game** during pregen. On multiplayer, set `pause-when-empty-seconds=-1` in `server.properties` so an empty server does not pause and stall generation. Avoid `/tick freeze`.

Source: https://github.com/pop4959/Chunky/wiki/Pregeneration  
Source: https://github.com/pop4959/Chunky/wiki/FAQ

### Radius vs border size (important)

Vanilla `/worldborder set <diameter>` uses **diameter** (edge to edge). Chunky `radius` is distance from center to the edge of the selection (half of a square’s side for a square centered at 0,0).

Example from Hangar: border diameter `20000` → use `chunky worldborder` (radius becomes `10000`) then `chunky start`.

Source: https://hangar.papermc.io/pop4959/Chunky

If the world border (or `max-world-size`) is **smaller** than the area you pre-generated, mobs will not spawn outside the border even if chunks exist.

Source: https://github.com/pop4959/Chunky/wiki/FAQ

## Quick start (overworld)

Console (no leading `/`). In-game, prefix with `/`.

Default selection if unchanged: square in the overworld, center `0,0`, radius `500` (1000×1000 blocks).

Source: https://github.com/pop4959/Chunky/wiki/Commands

### Minimal — 5000-block radius around default center

```
chunky radius 5000
chunky start
```

Source: https://github.com/pop4959/Chunky/wiki/Pregeneration

### Recommended snaxcraft pattern — square from spawn, then verify

```
chunky world world
chunky shape square
chunky spawn
chunky radius 5000
chunky selection
chunky start
```

- `spawn` recenters on the world’s spawn (can differ from 0,0).
- `selection` prints what will generate — read it before `start`.

Source: https://github.com/pop4959/Chunky/wiki/Commands

### Match vanilla world border

```
worldborder center 0 0
worldborder set 20000
chunky world world
chunky worldborder
chunky selection
chunky start
```

Source: https://hangar.papermc.io/pop4959/Chunky

### One-liner start (selection inline)

```
chunky start world square 0 0 1000
```

Starts a square in `world`, center `0,0`, radius `1000`.

Source: https://github.com/pop4959/Chunky/wiki/Commands

## Other dimensions

After the overworld task is running (or finished), switch world and start again. Selection radius/shape persist until you change them.

```
chunky world world_nether
chunky start
```

If that world name fails, try `the_nether` / `the_end` / `world_the_end` as listed above.

Circle at nether spawn example (Hangar):

```
chunky world the_nether
chunky shape circle
chunky spawn
chunky radius 1000
chunky start
```

Source: https://hangar.papermc.io/pop4959/Chunky  
Source: https://github.com/pop4959/Chunky/wiki/Pregeneration

You can run **multiple dimension tasks at once** to use more CPU; on a small host, prefer one task at a time.

Source: https://hangar.papermc.io/pop4959/Chunky

## Task control

| Command | Effect |
|---------|--------|
| `chunky pause` / `chunky pause <world>` | Pause and **save** progress |
| `chunky continue` / `chunky continue <world>` | Resume saved/current tasks |
| `chunky cancel` / `chunky cancel <world>` | Stop and **discard** the task (already generated chunks stay) |
| `chunky progress` | Show progress in-game (console also prints updates) |
| `chunky silent` | Toggle progress spam |
| `chunky quiet <seconds>` | Seconds between update messages (`0` = every chunk) |

Source: https://github.com/pop4959/Chunky/wiki/Commands

### Restarts

By default Chunky does **not** auto-resume after restart. Tasks are saved on a normal shutdown and when you `pause`. Enable `continue-on-restart` in Chunky’s config if you want automatic resume, then `chunky reload` (or restart) so the change applies.

Source: https://github.com/pop4959/Chunky/wiki/FAQ

## Selection reference

| Command | Purpose |
|---------|---------|
| `chunky world [world]` | Target world (`chunky world` alone = player’s world) |
| `chunky shape <shape>` | e.g. `square`, `circle` (see wiki shapes list) |
| `chunky center [x] [z]` | Center block; no args = your location |
| `chunky radius <r>` | Radius in blocks; also `10k`, `625c` (chunks), `+1k` / `-1k` |
| `chunky corners <x1> <z1> <x2> <z2>` | Region from two corners |
| `chunky worldborder [world]` | Import center/radius from active world border |
| `chunky spawn` | Center on vanilla spawn |
| `chunky pattern <name>` | Generation order (`concentric`, `loop`, …); default is usually fine |
| `chunky selection` | Print current selection |

Source: https://github.com/pop4959/Chunky/wiki/Commands

## Permissions (LuckPerms)

Parent permission `chunky.command` (default **op**) gates the command tree. Useful nodes include:

- `chunky.command.start` / `pause` / `continue` / `cancel`
- `chunky.command.world` / `radius` / `center` / `shape` / `selection`
- `chunky.command.trim` / `reload` / `progress`

For snaxcraft co-op: leave Chunky as **op/console only** unless you intentionally give a trusted admin group these nodes in LuckPerms.

Source: https://github.com/pop4959/Chunky/blob/master/bukkit/src/main/resources/plugin.yml

## Trim (destructive)

`chunky trim` **deletes** chunks (default: outside the selection). There is no undo without a backup. After trim, **restart the server** so deleted chunks are not kept in memory.

```
chunky trim world square 0 0 10k
```

Loaded chunks (players, spawn, forceloaded) often will not stay deleted — unload / empty the server first. Do not use trim casually on a live co-op world.

Source: https://github.com/pop4959/Chunky/wiki/Commands  
Source: https://github.com/pop4959/Chunky/wiki/Trimming-chunks  
Source: https://github.com/pop4959/Chunky/wiki/FAQ

## Performance tips (Paper)

From the official FAQ (abbreviated for our stack):

- Fast CPU + enough threads; SSD storage; enough heap (avoid both severe under- and over-allocation).
- Paper already helps vs plain Spigot for chunk gen.
- Optional while pregen-only: raise Paper worker threads via `-DPaper.WorkerThreadCount=X` or `config/paper-global.yml` → `worker-threads`, then **restore defaults** when finished.
- If generation stalls or crashes, test with fewer plugins; some worldgen/map addons conflict (see FAQ list — most are Fabric mods; Dynmap-style renderers are the common plugin case).

Source: https://github.com/pop4959/Chunky/wiki/FAQ

## Paper-specific note: treasure maps

After heavy pregen, buried treasure maps can point at empty spots (vanilla bug MC-218156). On Paper, set in `server/config/paper-world-defaults.yml`:

`environment.treasure-maps.find-already-discovered.loot-tables` → `false`

Source: https://github.com/pop4959/Chunky/wiki/FAQ

## snaxcraft target sizes

Square, **center 0,0**. Chunky **radius** = center → edge. Side length = **2 × radius**.

| Dimension | World name (try first) | Radius | Covers (X/Z) | Side |
|-----------|------------------------|--------|--------------|------|
| Overworld | `world` | **3500** | −3500…+3500 | 7000 |
| Nether | `world_nether` | **440** | −440…+440 | 880 (~1/8 of OW travel) |
| End | `world_the_end` | **2500** | −2500…+2500 | 5000 |

Match playable border after gen (OW example):

```
worldborder center 0 0
worldborder set 7000
```

(`set` = **diameter** = 2 × Chunky radius.)

Also raise `max-world-size` in `server.properties` if you extend beyond the current cap (see [Extend +500](#extend-map--500-blocks-each-direction)).

**Host notes (Stone / prior Wood / Dirt):** Prefer **Chunky-only** (other plugin jars disabled) during big pregen. Already-generated chunks are **skipped**. One-shot OW **3500** OOMed on Dirt (1GB); Wood (2GB) was better; Stone (4GB) has more headroom but tiling is still safer for huge OW jobs. End often one-shots fine. Restart between heavy jobs if exit **137** / OOM.

---

## Practical snaxcraft recipes

### A) One-shot (whole dimension in one task)

Use when the dim generates cheaply (often **End**, sometimes **Nether**). Read `chunky selection` before `start`.

**Overworld (3500)** — may OOM on low RAM; use [tiling](#b-tiling-fixed-1000--1000-squares) if it dies:

```
chunky cancel
chunky world world
chunky shape square
chunky center 0 0
chunky radius 3500
chunky selection
chunky start
```

**Nether (440):**

```
chunky cancel
chunky world world_nether
chunky shape square
chunky center 0 0
chunky radius 440
chunky selection
chunky start
```

**End (2500):**

```
chunky cancel
chunky world world_the_end
chunky shape square
chunky center 0 0
chunky radius 2500
chunky selection
chunky start
```

If a world name fails, tab-complete `chunky world` (`the_nether` / `the_end`).

### B) Tiling (fixed 1000×1000 squares)

Each tile is **1000×1000** blocks (= square **radius 500** for that tile). Load stays roughly **flat** (unlike growing rings). Overlap with finished areas is skipped. Restart between tiles if OOM.

Setup once per dimension:

```
chunky cancel
chunky world <name>
chunky shape square
```

#### Overworld — cover −3500…3500 (49 tiles)

```
chunky corners -3500 -3500 -2500 -2500
chunky selection
chunky start
chunky corners -3500 -2500 -2500 -1500
chunky start
chunky corners -3500 -1500 -2500 -500
chunky start
chunky corners -3500 -500 -2500 500
chunky start
chunky corners -3500 500 -2500 1500
chunky start
chunky corners -3500 1500 -2500 2500
chunky start
chunky corners -3500 2500 -2500 3500
chunky start
chunky corners -2500 -3500 -1500 -2500
chunky start
chunky corners -2500 -2500 -1500 -1500
chunky start
chunky corners -2500 -1500 -1500 -500
chunky start
chunky corners -2500 -500 -1500 500
chunky start
chunky corners -2500 500 -1500 1500
chunky start
chunky corners -2500 1500 -1500 2500
chunky start
chunky corners -2500 2500 -1500 3500
chunky start
chunky corners -1500 -3500 -500 -2500
chunky start
chunky corners -1500 -2500 -500 -1500
chunky start
chunky corners -1500 -1500 -500 -500
chunky start
chunky corners -1500 -500 -500 500
chunky start
chunky corners -1500 500 -500 1500
chunky start
chunky corners -1500 1500 -500 2500
chunky start
chunky corners -1500 2500 -500 3500
chunky start
chunky corners -500 -3500 500 -2500
chunky start
chunky corners -500 -2500 500 -1500
chunky start
chunky corners -500 -1500 500 -500
chunky start
chunky corners -500 -500 500 500
chunky start
chunky corners -500 500 500 1500
chunky start
chunky corners -500 1500 500 2500
chunky start
chunky corners -500 2500 500 3500
chunky start
chunky corners 500 -3500 1500 -2500
chunky start
chunky corners 500 -2500 1500 -1500
chunky start
chunky corners 500 -1500 1500 -500
chunky start
chunky corners 500 -500 1500 500
chunky start
chunky corners 500 500 1500 1500
chunky start
chunky corners 500 1500 1500 2500
chunky start
chunky corners 500 2500 1500 3500
chunky start
chunky corners 1500 -3500 2500 -2500
chunky start
chunky corners 1500 -2500 2500 -1500
chunky start
chunky corners 1500 -1500 2500 -500
chunky start
chunky corners 1500 -500 2500 500
chunky start
chunky corners 1500 500 2500 1500
chunky start
chunky corners 1500 1500 2500 2500
chunky start
chunky corners 1500 2500 2500 3500
chunky start
chunky corners 2500 -3500 3500 -2500
chunky start
chunky corners 2500 -2500 3500 -1500
chunky start
chunky corners 2500 -1500 3500 -500
chunky start
chunky corners 2500 -500 3500 500
chunky start
chunky corners 2500 500 3500 1500
chunky start
chunky corners 2500 1500 3500 2500
chunky start
chunky corners 2500 2500 3500 3500
chunky start
```

#### Nether — cover −440…440 (4 tiles)

```
chunky world world_nether
chunky shape square
chunky corners -440 -440 0 0
chunky selection
chunky start
chunky corners -440 0 0 440
chunky start
chunky corners 0 -440 440 0
chunky start
chunky corners 0 0 440 440
chunky start
```

Or one-shot nether (see [A](#a-one-shot-whole-dimension-in-one-task)).

#### End — cover −2500…2500 (25 tiles)

```
chunky world world_the_end
chunky shape square
chunky corners -2500 -2500 -1500 -1500
chunky selection
chunky start
chunky corners -2500 -1500 -1500 -500
chunky start
chunky corners -2500 -500 -1500 500
chunky start
chunky corners -2500 500 -1500 1500
chunky start
chunky corners -2500 1500 -1500 2500
chunky start
chunky corners -1500 -2500 -500 -1500
chunky start
chunky corners -1500 -1500 -500 -500
chunky start
chunky corners -1500 -500 -500 500
chunky start
chunky corners -1500 500 -500 1500
chunky start
chunky corners -1500 1500 -500 2500
chunky start
chunky corners -500 -2500 500 -1500
chunky start
chunky corners -500 -1500 500 -500
chunky start
chunky corners -500 -500 500 500
chunky start
chunky corners -500 500 500 1500
chunky start
chunky corners -500 1500 500 2500
chunky start
chunky corners 500 -2500 1500 -1500
chunky start
chunky corners 500 -1500 1500 -500
chunky start
chunky corners 500 -500 1500 500
chunky start
chunky corners 500 500 1500 1500
chunky start
chunky corners 500 1500 1500 2500
chunky start
chunky corners 1500 -2500 2500 -1500
chunky start
chunky corners 1500 -1500 2500 -500
chunky start
chunky corners 1500 -500 2500 500
chunky start
chunky corners 1500 500 2500 1500
chunky start
chunky corners 1500 1500 2500 2500
chunky start
```

Or one-shot End (preferred if it holds): [A](#a-one-shot-whole-dimension-in-one-task).

### Extend map — +500 blocks each direction

Grows the square **outward by 500** on every side (new radius = old + 500). Inner area is skipped.

| Dim | Old radius | New radius | New covers | New border diameter |
|-----|------------|------------|------------|---------------------|
| Overworld | 3500 | **4000** | −4000…+4000 | `worldborder set 8000` |
| Nether | 440 | **500** | −500…+500 | (optional) |
| End | 2500 | **3000** | −3000…+3000 | (optional) |

1. Set `max-world-size` ≥ new radius in `server.properties`, push, restart.
2. Pregen (one-shot or tile the **new rim** only).

**One-shot extend:**

```
chunky world world
chunky shape square
chunky center 0 0
chunky radius 4000
chunky selection
chunky start
```

```
chunky world world_nether
chunky shape square
chunky center 0 0
chunky radius 500
chunky start
```

```
chunky world world_the_end
chunky shape square
chunky center 0 0
chunky radius 3000
chunky start
```

**Tile only the new +500 rim (OW example)** — 1000×1000 tiles that sit on the outer frame (inner −3500…3500 already done = mostly skip). Corner pairs for the new band to **±4000**:

```
chunky world world
chunky shape square
# North strip (z 3500→4000), x -4000→4000 in 1000 steps
chunky corners -4000 3500 -3000 4000
chunky start
chunky corners -3000 3500 -2000 4000
chunky start
chunky corners -2000 3500 -1000 4000
chunky start
chunky corners -1000 3500 0 4000
chunky start
chunky corners 0 3500 1000 4000
chunky start
chunky corners 1000 3500 2000 4000
chunky start
chunky corners 2000 3500 3000 4000
chunky start
chunky corners 3000 3500 4000 4000
chunky start
# South strip (z -4000→-3500)
chunky corners -4000 -4000 -3000 -3500
chunky start
chunky corners -3000 -4000 -2000 -3500
chunky start
chunky corners -2000 -4000 -1000 -3500
chunky start
chunky corners -1000 -4000 0 -3500
chunky start
chunky corners 0 -4000 1000 -3500
chunky start
chunky corners 1000 -4000 2000 -3500
chunky start
chunky corners 2000 -4000 3000 -3500
chunky start
chunky corners 3000 -4000 4000 -3500
chunky start
# West strip (x -4000→-3500), z -3500→3500 (corners avoid double-counting N/S ends if you already did full N/S; these fill the sides)
chunky corners -4000 -3500 -3500 -2500
chunky start
chunky corners -4000 -2500 -3500 -1500
chunky start
chunky corners -4000 -1500 -3500 -500
chunky start
chunky corners -4000 -500 -3500 500
chunky start
chunky corners -4000 500 -3500 1500
chunky start
chunky corners -4000 1500 -3500 2500
chunky start
chunky corners -4000 2500 -3500 3500
chunky start
# East strip (x 3500→4000)
chunky corners 3500 -3500 4000 -2500
chunky start
chunky corners 3500 -2500 4000 -1500
chunky start
chunky corners 3500 -1500 4000 -500
chunky start
chunky corners 3500 -500 4000 500
chunky start
chunky corners 3500 500 4000 1500
chunky start
chunky corners 3500 1500 4000 2500
chunky start
chunky corners 3500 2500 4000 3500
chunky start
```

Simpler extend if RAM allows: one-shot `radius 4000` / `500` / `3000` and let skip eat the inside.

Then update border:

```
worldborder center 0 0
worldborder set 8000
```

### C) Border-sized world then generate

1. Agree border diameter with the group.
2. Set vanilla border (`worldborder center` / `worldborder set <diameter>`).
3. `chunky worldborder` → `chunky selection` → `chunky start`.
4. Repeat for nether/end with matching relative sizes if you want those pre-filled too.

### D) Check status without console spam

```
chunky quiet 30
chunky progress
```

## Troubleshooting

| Symptom | What to try |
|---------|-------------|
| No help from `chunky` | Jar missing/wrong; not op; check startup logs for plugin enable errors |
| Wrong dimension / empty task | Wrong world name — verify with `chunky world` / `selection` |
| No progress messages | Watch **server console**; or `chunky progress` / disable `silent` |
| ETA huge | Shrink radius; run off-peak; one dimension at a time |
| High RAM use | Expected during gen; raise host RAM or shrink selection; tune JVM if you control flags |
| Task gone after restart | `continue-on-restart` false (default) — use `chunky continue` or enable the config option |
| Trim “did nothing” | Chunks still loaded; empty server, trim again, restart |
| No mobs far out | World border / `max-world-size` smaller than generated area |

Source: https://github.com/pop4959/Chunky/wiki/FAQ  
Source: https://github.com/pop4959/Chunky/wiki/Trimming-chunks

## Related on this server

- Plugin inventory: `dev/mod-list.md`
- Live jar: `server/plugins/Chunky-Bukkit-1.5.3.jar`
- Paper configs: `server/config/paper-global.yml`, `server/config/paper-world-defaults.yml`

## See also

- BlueMap (pause during heavy pregen): [`bluemap.md`](bluemap.md)  
- Author wiki home: https://github.com/pop4959/Chunky/wiki  
- Hangar (Paper): https://hangar.papermc.io/pop4959/Chunky  
- Optional border addon (not installed): ChunkyBorder on Hangar
