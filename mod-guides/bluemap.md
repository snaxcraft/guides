# BlueMap — live web map

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-10  
**Applies to:** `BlueMap` (`bluemap-5.23-paper.jar`)  
**Host:** Cybrancee **Stone** (4GB) — see `dev/host-profile.md`

## Summary

BlueMap renders snaxcraft’s worlds into a **3D web map** and hosts it on an extra panel port. Use the **Paper** jar only. **Do not use Dynmap** on this host — Dynmap 3.7 fails on Paper 26.2.

Source: https://bluemap.bluecolored.de/wiki/getting-started/Installation.html  
Source: https://cybrancee.com/learn/knowledge-base/how-to-set-up-bluemap-on-your-minecraft-server/  
Source: `dev/host-profile.md`

## Players

### Open the map

1. Ask an op for the current map URL (server address + BlueMap port).
2. Open it in a browser: `http://<host>:<bluemap-port>/`
3. Switch Overworld / Nether / End from the web UI map list.

On snaxcraft the integrated webserver listens on port **50005** (`plugins/BlueMap/webserver.conf`). The public host/IP is whatever Cybrancee assigns — ops publish that; do not hardcode secrets or panel credentials here.

Source: https://bluemap.bluecolored.de/wiki/getting-started/Installation.html  
Source: `server/plugins/BlueMap/webserver.conf`

### Live players on the map

With the webserver enabled, BlueMap can show online players in near-real time (`live-player-markers: true`).

You are **hidden** from the map when:

| Condition | snaxcraft setting |
|-----------|-------------------|
| Spectator mode | Hidden (`hidden-game-modes` includes `spectator`) |
| Vanished (plugin vanish) | Hidden (`hide-vanished: true`) |
| Invisibility potion | Hidden (`hide-invisible: true`) |
| Sneaking | Still visible (`hide-sneaking: false`) |

Source: `server/plugins/BlueMap/plugin.conf`

The map is a viewer — it does not claim land, teleport you, or replace in-game navigation.

## Ops

### Install snapshot (already live)

| Item | Value |
|------|--------|
| Jar | `server/plugins/bluemap-5.23-paper.jar` |
| Config folder | `server/plugins/BlueMap/` |
| Webroot / map data | `bluemap/web` (relative to server root) |
| Webserver | Enabled, port **50005** |
| Render threads | `1` (`core.conf` → `render-thread-count`) |
| Mojang resources | `accept-download: true` in `core.conf` (required) |

Source: https://bluemap.bluecolored.de/wiki/getting-started/Installation.html  
Source: `server/plugins/BlueMap/core.conf`  
Source: `server/plugins/BlueMap/webserver.conf`

Always download the **Paper** build that matches your MC version. Wrong platform jars will not load correctly.

Source: https://github.com/BlueMap-Minecraft/BlueMap/releases

### Cybrancee extra port

BlueMap needs a **second port** besides the Minecraft game port (`10007` on this host).

1. Panel → **Ports** → **Add Port** → copy the allocated port.
2. Set `port:` in `plugins/BlueMap/webserver.conf` to that value (snaxcraft: **50005**).
3. Ensure `accept-download: true` in `core.conf`.
4. Restart or `/bluemap reload`.
5. Browse `http://<server-ip>:<port>/`.

Source: https://cybrancee.com/learn/knowledge-base/how-to-set-up-bluemap-on-your-minecraft-server/  
Source: `dev/host-profile.md`

### Maps on snaxcraft

Configs under `plugins/BlueMap/maps/`:

| Config file | Dimension | Display name |
|-------------|-----------|--------------|
| `world.conf` | `minecraft:overworld` | world (overworld) |
| `world_the_nether.conf` | `minecraft:the_nether` | world (the_nether) |
| `world_the_end.conf` | `minecraft:the_end` | world (the_end) |

Map IDs for commands usually match the filename without `.conf` (e.g. `world`, `world_the_nether`, `world_the_end`). Confirm with `/bluemap maps`.

Source: `server/plugins/BlueMap/maps/world.conf`  
Source: `server/plugins/BlueMap/maps/world_the_nether.conf`  
Source: `server/plugins/BlueMap/maps/world_the_end.conf`  
Source: https://bluemap.bluecolored.de/wiki/getting-started/Commands.html

### Useful commands

Usually BlueMap **auto-updates** as the world changes; you rarely need force renders.

| Command | Effect |
|---------|--------|
| `/bluemap` | Render status |
| `/bluemap maps` | List maps (incl. frozen) |
| `/bluemap reload` | Reload configs + webserver |
| `/bluemap stop` | Pause **all** rendering (survives restart) |
| `/bluemap start` | Resume rendering |
| `/bluemap freeze <map>` | Freeze one map’s updates |
| `/bluemap unfreeze <map>` | Unfreeze one map |
| `/bluemap update [map] …` | Check/update changed chunks (rarely needed) |
| `/bluemap purge <map>` | Delete map render data (re-renders after; destructive) |
| `/bluemap troubleshoot …` | Suggest fixes for a location |

Source: https://bluemap.bluecolored.de/wiki/getting-started/Commands.html

### Pause during Chunky / heavy load

On **4GB Stone**, BlueMap render threads still compete with Chunky and players. Pause BlueMap during heavy pregen.

Before large pregen:

```
bluemap stop
```

After Chunky finishes:

```
bluemap start
```

(`stop`/`start` persist across restarts.) See `mod-guides/chunky.md`.

Source: https://bluemap.bluecolored.de/wiki/getting-started/Commands.html  
Source: `mod-guides/chunky.md`  
Source: `dev/host-profile.md`

`player-render-limit` is `-1` on snaxcraft (never auto-pauses when players are online). Leave it unless lag appears; then consider a low positive number so rendering pauses while people play.

Source: `server/plugins/BlueMap/plugin.conf`

### Stone RAM notes

- Keep `render-thread-count` at **1** unless spark/logs show headroom.
- Prefer pausing BlueMap during Chunky or other heavy jobs.
- Next host step if map + plugins fight for heap: **Iron (6GB)** -- see `dev/host-profile.md`.

Source: `server/plugins/BlueMap/core.conf`  
Source: `dev/host-profile.md`

## Troubleshooting

| Symptom | What to try |
|---------|-------------|
| Browser can’t connect | Confirm panel **extra port** matches `webserver.conf`; firewall/panel port enabled; use `http://` + IP + port |
| Blank / unfinished map | Wait for first render; check console; `/bluemap` status; ensure `accept-download: true` |
| Wrong / missing dimension | Check `maps/*.conf`; `/bluemap maps`; `/bluemap troubleshoot` |
| Lag with players online | `/bluemap stop` while playing; or set `player-render-limit`; keep render threads low |
| “Use Dynmap instead” advice | Ignore for Paper 26.2 on this host — use BlueMap Paper jar |
| Non-Paper jar | Replace with `*-paper.jar` from BlueMap releases |

Source: https://bluemap.bluecolored.de/wiki/getting-started/Installation.html  
Source: https://bluemap.bluecolored.de/wiki/getting-started/Commands.html  
Source: `dev/host-profile.md`

## Related on this server

- Plugin inventory: `dev/mod-list.md`
- Live jar: `server/plugins/bluemap-5.23-paper.jar`
- Host / ports: `dev/host-profile.md`
- Pregen: `mod-guides/chunky.md`

## See also

- BlueMap wiki (install): https://bluemap.bluecolored.de/wiki/getting-started/Installation.html  
- BlueMap commands: https://bluemap.bluecolored.de/wiki/getting-started/Commands.html  
- Cybrancee BlueMap setup: https://cybrancee.com/learn/knowledge-base/how-to-set-up-bluemap-on-your-minecraft-server/  
- Releases: https://github.com/BlueMap-Minecraft/BlueMap/releases  
