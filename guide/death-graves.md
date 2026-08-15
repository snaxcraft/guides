# Death graves (players)

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11  
**Applies to:** GravesX plugin on snaxcraft  
**Ops / config:** [`mod-guides/gravesx.md`](../mod-guides/gravesx.md)

## Summary

When you die with items, snaxcraft usually puts your gear in a **grave** (player head + hologram) near the death spot instead of dumping everything on the ground. You have about **3 hours** to recover it.

Source: `server/plugins/GravesX/config/grave.yml`  
Source: https://hangar.papermc.io/Legoman99573/GravesX

This is a **plugin** — not the vanilla keep-inventory gamerule.

Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

## After you die

1. Respawn. You may get a **compass** that points toward your grave for a short time.
2. Find the head/hologram (shows your name and time left).
3. Open / break the grave to get your stuff back (auto-loot pulls into your inventory when it can).
4. Or use `/graves` to open a list of your graves and **teleport** to one.

Source: `server/plugins/GravesX/config/grave.yml`  
Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation

## Commands

| Command | Use |
|---------|-----|
| `/graves` | Your graves menu (teleport, manage) |
| `/graves help` | Plugin help |
| `/graves list` | List your graves |

Source: https://www.spigotmc.org/resources/gravesx.118271/field?field=documentation

## What to expect on snaxcraft

| Fact | Detail |
|------|--------|
| Lifetime | About **3 hours**, then items drop on the ground |
| Look | Player-head block + floating text |
| XP | Most of your XP is stored in the grave (~70%); some may still be lost |
| Explosions | Graves resist blowing up |
| Empty death | No grave if you had nothing to drop |

Source: `server/plugins/GravesX/config/grave.yml`  
Source: https://github.com/Legoman99573/GravesX/wiki/FAQ

## Tips

- Don’t wait out the timer if the death was far away — use `/graves` and teleport.
- Friends can usually open graves too (timed owner-lock is **off** right now). Be nice.
- If you die and **keep** all items with no grave, you likely have Essentials **keep inventory** (common for admins). Ask an op to run the LuckPerms denies in [`mod-guides/essentialsx.md`](../mod-guides/essentialsx.md#gravesx--essentialskeepinv-admins) (`essentials.keepinv` / `essentials.keepxp` → `false`).

Source: `server/plugins/GravesX/config/grave.yml`  
Source: https://github.com/Legoman99573/GravesX/wiki/FAQ  
Source: [`mod-guides/essentialsx.md`](../mod-guides/essentialsx.md)

## See also

- Ops guide: [`mod-guides/gravesx.md`](../mod-guides/gravesx.md)  
- Sit / lay: [`sit-lay-crawl.md`](sit-lay-crawl.md)  
- Homes / `/back`: [`mod-guides/essentialsx.md`](../mod-guides/essentialsx.md) (players: ask ops for homes/TPA)
