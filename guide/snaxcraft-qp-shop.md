# snaxcraft Quest Point shop

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-20  
**Applies to:** CommandPanels `/qp`

## How to buy

Run `/qp`. The menu spends Quests Classic **Quest Points (QP)**, not Vault money. Your balance is shown in the shop. If you cannot afford an item, the purchase is cancelled and chat says `Not enough Quest Points (need N).`

The root categories are **Eggs, Spawners, Gear, Enchanting, Potions, Blocks, and Loot**.

Source: `server/plugins/CommandPanels/panels/qp-shop.yml`
Source: `server/plugins/CommandPanels/panels/qp-*.yml`

## Eggs and spawners

The egg and spawner pages cover the full Java mob catalog and are split into Passive, Hostile, Nether, End, and Boss pages.

- Spawn eggs: ambient about 20 QP; farm mobs about 40; common hostiles 40-120; pets about 70; Nether mobs 100-200; utility mobs 140-180; elite mobs 240-360; rare/End mobs 400-600; bosses 1000, 1500, or 2000.
- Spawners: normal mobs cost 2400-2800 QP; boss spawners cost 8000-9000 QP.

Source: `server/plugins/CommandPanels/panels/qp-eggs-*.yml`
Source: `server/plugins/CommandPanels/panels/qp-spawners-*.yml`

## Gear

| Page | Stock | QP each |
|------|-------|--------:|
| T1 | Survival diamond armor, sword, axe, spear, pickaxes, shovel, and hoe | 2400 |
| T2 | Survival netherite version of the T1 set | 2600 |
| T3 | God-roll diamond set | 5000 |
| T4 | Strong netherite set | 5600 |
| T5 | Best netherite achievement set | 7600 |
| T6 | Bow, crossbow, fishing rod, trident, mace, shield, and elytra | 600-1000 |
| Hybrids | Copper, iron, or diamond Dolabra and Mattock | 800 / 1400 / 2000 |
| Alloys | Hepatizon, Shakudo, Steel, Electrum, and Adamant equipment | 3200 |

See [hybrid tools](snaxcraft-hybrids.md) and [alloy equipment](snaxcraft-alloys.md) for what those pieces do.

Source: `server/plugins/CommandPanels/panels/qp-gear*.yml`
Source: `dev/qp-shop-catalog.json`

## Enchanting

The shop sells 16 Bottles o' Enchanting for **20 QP** and max-level enchanted books. Book prices use three practical bands:

| Band | Price | Examples |
|------|------:|----------|
| Staple | 280-400 | Aqua Affinity, protection types, Sharpness V, Efficiency V, Unbreaking III |
| Strong | 400-560 | Fortune III, Looting III, Power V, Feather Falling IV, Lunge III |
| Treasure / rare | 640-840 | Frost Walker II, Silk Touch, Soul Speed III, Swift Sneak III, Mending, Wind Burst III |

The pages include weapon, tool, armor, ranged, and treasure books. Enchanting and trading remain useful ways to obtain books without spending QP.

Source: `dev/qp-shop-extra.json`
Source: https://minecraft.wiki/w/Enchanting

## Potions

Potions are a stopgap for players who do not want to brew immediately. Every purchase gives **8 drinkable potions**:

| QP | Potions |
|---:|---------|
| 60 | Weakness 4:00 |
| 80 | Fire Resistance 8:00, Night Vision 8:00, Water Breathing 8:00, Slow Falling 4:00, Invisibility 8:00 |
| 100 | Strength II, Swiftness II, Leaping II, Healing II, Regeneration II, Poison II, Slowness 4:00 |
| 120 | Turtle Master (long) |

Splash and lingering variants are not sold. Brewing still gives more control over form, duration, and strength. Potion of Luck is also not sold because it is not brewable in Java survival.

Source: `dev/qp-shop-extra.json`
Source: https://minecraft.wiki/w/Brewing
Source: https://minecraft.wiki/w/Potion_of_Luck

## Blocks

These are convenience purchases. Mining with the right tool, especially Fortune for ore drops, is normally the better long-term source.

| QP | Stock |
|---:|-------|
| 20 | 64 Grass Blocks |
| 40 | 64 Podzol; 64 Moss Blocks; 64 Cobwebs |
| 50 | 64 Mycelium; 64 Ice; 64 Brown or Red Mushroom Blocks |
| 60 | 64 Crimson or Warped Nylium |
| 80 | 32 Packed Ice; 32 Sculk; 64 Coal Ore |
| 100 | 32 Glowstone; 64 Copper Ore |
| 120 | 16 of any Coral Block |
| 160 | 16 Blue Ice; 32 Redstone Ore; 32 Lapis Ore |
| 200 | 16 Sculk Sensors; 32 Gold Ore |
| 240 | 16 Bee Nests; 64 Iron Ore |
| 320 | 16 Sculk Catalysts |
| 720 | 16 Emerald Ore |
| 800 | 16 Diamond Ore |

Many entries are blocks normally collected with Silk Touch. Budding amethyst is deliberately excluded because it cannot be obtained with Silk Touch.

Source: `dev/qp-shop-extra.json`
Source: https://minecraft.wiki/w/Silk_Touch

## Loot

Loot is soft-sink stock for finds that are not craftable in survival on this version. Horse spawn eggs stay under Eggs; this category does not give a horse.

### Mount gear

| QP | Item |
|---:|------|
| 240 | Iron Horse Armor |
| 340 | Golden Horse Armor |
| 560 | Diamond Horse Armor |

### Adventure loot

| QP | Item |
|---:|------|
| 200 | Nautilus Shell |
| 300 | Echo Shard |
| 480 | Heart of the Sea |
| 760 | Totem of Undying |

Saddle, leather horse armor, name tags, and leads are not sold here because they are craftable. Music discs, goat horns, and netherite horse armor are also not sold.

Source: `server/plugins/CommandPanels/panels/qp-loot.yml`
Source: `server/plugins/CommandPanels/panels/qp-loot-mount.yml`
Source: `server/plugins/CommandPanels/panels/qp-loot-adventure.yml`
Source: https://minecraft.wiki/w/Saddle
Source: https://minecraft.wiki/w/Horse_Armor
Source: https://minecraft.wiki/w/Name_Tag

## Not sold

The shop does **not** sell structure blocks, command blocks, barriers, bedrock, debug sticks, budding amethyst, Potion of Luck, splash/lingering potions, saddles, leather horse armor, name tags, leads, music discs, goat horns, or netherite horse armor.

Source: `server/plugins/CommandPanels/panels/qp-*.yml`
Source: `dev/qp-shop-extra.json`
Source: https://minecraft.wiki/w/Potion_of_Luck
Source: https://minecraft.wiki/w/Saddle
Source: https://minecraft.wiki/w/Name_Tag

## See also

- [Dailies](snaxcraft-dailies.md) - the main source of QP
- [Challenge ladder](snaxcraft-quests.md) - a smaller QP drip
- [Hybrid tools](snaxcraft-hybrids.md)
- [Alloy equipment](snaxcraft-alloys.md)
