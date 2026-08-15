# Sit, lay, and crawl (players)

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-11  
**Applies to:** GSit plugin on snaxcraft  
**Ops / config:** [`mod-guides/gsit.md`](../mod-guides/gsit.md)

## Summary

You can sit on stairs and carpets, pile on friends, or use pose commands. No client mod needed — it works as soon as you join.

Source: https://hangar.papermc.io/Gecolay/GSit  
Source: `server/plugins/GSit/config.yml`

## Sit on furniture

1. Empty your **main hand**.
2. Right-click the **top** of stairs, slabs, carpets, or snow.
3. **Sneak** to stand up.

Turn click-sitting off/on with `/sit toggle`.

Source: `server/plugins/GSit/config.yml`  
Source: https://hangar.papermc.io/Gecolay/GSit

## Sit on players

Empty hand → right-click a friend to sit on them (stacks allowed). They (or you) **sneak** to get off. Toggle with `/sit playertoggle`.

Source: `server/plugins/GSit/config.yml`

## Pose commands

| Command | What it does |
|---------|----------------|
| `/sit` | Sit where you are |
| `/lay` | Lie down |
| `/crawl` | Crawl |
| `/bellyflop` | Bellyflop |
| `/spin` | Spin |

Sneak to cancel. If a command says you lack permission, ask an op.

Source: https://hangar.papermc.io/Gecolay/GSit

## Tips

- Holding an item in your main hand blocks click-to-sit.
- Only the lower half of stairs/slabs works for clicks.
- Lying down can help with rest / night skip when someone is also in a bed (plugin setting).

Source: `server/plugins/GSit/config.yml`

## See also

- Ops guide: [`mod-guides/gsit.md`](../mod-guides/gsit.md)  
- Death graves: [`death-graves.md`](death-graves.md)  
- Challenges: [`snaxcraft-quests.md`](snaxcraft-quests.md)
