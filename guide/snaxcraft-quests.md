# snaxcraft challenge ladder (Quests Classic)

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-14 (Kitchen + Hybrids + Alloys + Fisher + Abbey branches, Together loops)
**Applies to:** `plugins/Quests/storage/quests.yml` (branched progression)  
**Plugin guide:** [`mod-guides/quests-classic.md`](../mod-guides/quests-classic.md)

Optional side content: [dailies](snaxcraft-dailies.md), [QP shop](snaxcraft-qp-shop.md), [kitchen recipes](snaxcraft-kitchen.md), [hybrid tools](snaxcraft-hybrids.md), and [alloy equipment](snaxcraft-alloys.md). Separate from this ladder. **`/qc`** = completed ladder/Together history (not dailies).

## Summary

Full catalog: **296** quests - starter + **166** personal tips across **15** branches, plus **63** global Kill steps and **66** global Mine steps. Progression locks keep most quests inactive so you usually have ~**16** current quests (<=**50** hard cap).

| Track | How it starts | Progress |
|-------|---------------|----------|
| **Personal** (15 branches) | Take **Gotta Start Somewhere**, break 1 short grass | Yours only; finishing auto-gives the next tip in that branch |
| **Global Kill / Mine** | Given when you finish the starter | Shared; 3 tiers per mob/block, then loops back to root |

Locked personal quests are **hidden** from `/quests list` (`ignore-locked-quests: true`) until unlocked. You do not browse ahead - finish the current tip and the next one is given.

**Doable objectives:** Quests Classic `items-to-craft` only counts the **crafting table** (not smithing, not filling buckets, not drops). Ladder crafts must be real table recipes. Plant crops with `place-block-names` using the **block** id (`WHEAT` when planting wheat seeds).

Source: https://minecraft.wiki/w/Wheat_Seeds  
Source: https://minecraft.wiki/w/Smithing  
Source: https://minecraft.wiki/w/Water_Bucket  
Source: Quests 5.3.2 `BukkitItemListener.onCraftItem`

Source: `server/plugins/Quests/config.yml`  
Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`  
Source: `dev/quests-global-chains.json`  
Source: https://pikamug.gitbook.io/quests/beginner/options.md

## How to play

1. `/ql` (or `/quests list`) -> take **Gotta Start Somewhere** -> break **1 Short Grass**.
2. You receive the **15 personal branch tips** plus **Together - Kill 100 Zombies** and **Together - Mine 2048 Dirt**.
3. Finish a tip -> next step in that branch (or next global tier/target) is auto-given.
4. `/q` (or `/quests journal`) for active quests; `/quest` for chat objectives; vanilla advancements stay on **`L`**.
5. Track progress on the **boss bar**: `/kit quest` for a Quest Compass, or `/track` (`/qt`). **Right-click** the compass to cycle which quest is active; **left-click** resets. **Left-click** a quest in `/q` to set or clear the track; the compass cycle still works. Finishing a different quest does not steal your track.

| Command | Use |
|---------|-----|
| `/ql` | Available / unlocked (alias -> `/quests list`) |
| `/q` | Active quests GUI (alias -> `/quests journal`) — left-click sets or clears the track |
| `/track` `/qt` | See tracked quest + get Quest Compass kit |
| `/tabsettings` `/ts` | Configure what Tab shows (footer blocks + other players) |
| `/kit quest` | Named compass to cycle QuestsBar / track (60s cooldown) |
| `/qc` | Completed ladder + Together history (no dailies) |
| `/qs` | Quest stats / QP (alias -> `/quests stats`) |
| `/quest` | Current objectives (chat) |

Finishing tips, dailies, and Together steps also grants **item packages** (bread and torches early, then iron, then diamonds) on top of QP and exp.

Source: `server/commands.yml`  
Source: `server/plugins/Quests/storage/quests.yml`  
Source: `server/plugins/CommandPanels/panels/qc.yml`  
Source: `server/plugins/CommandPanels/panels/track.yml`  
Source: `server/plugins/CommandPanels/panels/tabsettings.yml`  
Source: `server/plugins/Essentials/kits.yml`  
Source: https://www.spigotmc.org/resources/questsbar.100634/  
Source: https://pikamug.gitbook.io/quests/setup/commands-and-permissions  
Source: [`mod-guides/questsbar.md`](../mod-guides/questsbar.md)  
Source: [`mod-guides/snax-quest-track.md`](../mod-guides/snax-quest-track.md)

## Starter

1. **Gotta Start Somewhere** (`snaxUnlockBranches`) - Gotta start somewhere. Break 1 Short Grass to unlock your challenge branches.

Source: `server/plugins/Quests/storage/quests.yml`

## Personal branches

Each branch is linear: finish step *n* to unlock step *n+1*. Roots unlock together after the starter. Work any branches in parallel (one active tip per branch).

| Branch | Steps | Starts with |
|--------|-------|-------------|
| [Tools](#tools-branch) | 12 | **Minecraft Story** |
| [Armor](#armor-branch) | 6 | **Suit Up** |
| [Nether](#nether-branch) | 16 | **We Need to Go Deeper** |
| [End](#end-branch) | 13 | **Eye Spy** |
| [Combat](#combat-branch) | 20 | **Adventure Tab** |
| [Farm](#farm-branch) | 30 | **Husbandry Tab** |
| [Explore](#explore-branch) | 18 | **Sweet Dreams** |
| [Ocean](#ocean-branch) | 8 | **What a Deal** |
| [Magic](#magic-branch) | 10 | **Enchanter** |
| [Boss](#boss-branch) | 8 | **Spooky Scary Skeleton** |
| [Kitchen](#kitchen-branch) | 11 | **Plant Wheat** |

Source: `dev/quests-branch-map.json`  
Source: `server/plugins/Quests/storage/quests.yml`

### Tools branch

12 steps. Finish each to unlock the next.

1. **Minecraft Story** - Craft a Crafting Table. (Advancement: Minecraft)
2. **Stone Age** - Break 8 Cobblestone. (Advancement: Stone Age)
3. **Getting an Upgrade** - Craft a Stone Pickaxe. (Advancement: Getting an Upgrade)
4. **Acquire Hardware** - Smelt 1 Iron Ingot. (Advancement: Acquire Hardware)
5. **Isnt It Iron Pick** - Craft an Iron Pickaxe. (Advancement: Isnt It Iron Pick)
6. **Diamonds** - Mine 1 Diamond Ore. (Advancement: Diamonds!)
7. **Copper Age** - Mine 32 Copper Ore.
8. **Deepslate Iron** - Mine 16 Deepslate Iron Ore.
9. **Deepslate Diamonds** - Mine 3 Deepslate Diamond Ore.
10. **Hot Stuff** - Craft a Bucket. (Proxy: Hot Stuff - fill with lava for L)
11. **Ice Bucket Challenge** - Mine 1 Obsidian. (Advancement: Ice Bucket Challenge)
12. **Oak Forest Sweep** - Chop 64 Oak Logs.

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Armor branch

6 steps. Finish each to unlock the next.

1. **Suit Up** - Craft an Iron Chestplate. (Advancement: Suit Up)
2. **Not Today Thank You** - Craft a Shield. (Proxy: deflect a projectile for L)
3. **Cover Me with Diamonds** - Craft a Diamond Chestplate. (Advancement: Cover Me with Diamonds)
4. **Crafting a New Look** - Craft a Smithing Table. (Proxy: trim armor for L)
5. **Smithing with Style** - Craft a Smithing Table. (Proxy: all exclusive trims for L)
6. **Cover Me in Debris** - Craft a Netherite Ingot. (Proxy: full netherite set for L; smithing does not count)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Nether branch

16 steps. Finish each to unlock the next.

1. **We Need to Go Deeper** - Kill 3 Zombified Piglins. (Proxy: enter the Nether for L)
2. **Nether Tab** - Kill 1 Magma Cube. (Proxy: enter the Nether for L)
3. **A Terrible Fortress** - Kill 5 Blazes. (Proxy: find a fortress for L)
4. **Into Fire** - Kill 5 Blazes. (Advancement: Into Fire)
5. **Return to Sender** - Kill 1 Ghast. (Proxy: deflect fireball kill for L)
6. **Those Were the Days** - Kill 5 Piglins. (Proxy: find a bastion for L)
7. **War Pigs** - Kill 3 Piglin Brutes. (Proxy: loot bastion chest for L)
8. **Oh Shiny** - Craft 8 Gold Ingots. (Proxy: distract a piglin for L)
9. **Hidden in the Depths** - Mine 1 Ancient Debris. (Advancement: Hidden in the Depths)
10. **This Boat Has Legs** - Craft a Warped Fungus on a Stick. (Proxy: ride a strider for L)
11. **Feels Like Home** - Craft a Warped Fungus on a Stick. (Proxy: strider on OW lava for L)
12. **Who is Cutting Onions** - Mine 1 Crying Obsidian. (Advancement)
13. **Not Quite Nine Lives** - Craft a Respawn Anchor. (Proxy: charge to max for L)
14. **Hot Tourist Destinations** - Kill 1 Hoglin, 1 Magma Cube, and 1 Ghast. (Proxy: visit all Nether biomes for L)
15. **Subspace Bubble** - Kill 10 Magma Cubes. (Proxy: 7km Nether travel for L)
16. **Uneasy Alliance** - Kill 1 Ghast. (Proxy: kill ghast with Overworld credit for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### End branch

13 steps. Finish each to unlock the next.

1. **Eye Spy** - Craft 1 Eye of Ender. (Proxy: find a stronghold for L)
2. **The End Question** - Kill 5 Endermen. (Proxy: enter The End for L)
3. **The End Tab** - Kill 3 Endermen. (Proxy: enter The End for L)
4. **Free the End** - Kill the Ender Dragon. (Advancement: Free the End)
5. **The Next Generation** - Craft 4 End Crystals. (Proxy: hold Dragon Egg for L)
6. **Remote Getaway** - Kill 10 Endermen. (Proxy: enter an End gateway for L)
7. **City at the End** - Kill 5 Shulkers. (Proxy: find an End city for L)
8. **Skys the Limit** - Kill 8 Shulkers. (Proxy: obtain Elytra for L)
9. **Great View From Up Here** - Kill 10 Shulkers. (Proxy: levitate 50 blocks for L)
10. **You Need a Mint** - Craft 8 Glass Bottles. (Proxy: collect dragon breath for L)
11. **The End Again** - Craft 4 End Crystals. (Proxy: respawn the dragon for L)
12. **Pocket Storage** - Craft an Ender Chest.
13. **Moving Day** - Craft a Shulker Box.

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Combat branch

20 steps. Finish each to unlock the next.

1. **Adventure Tab** - Kill 1 Zombie. (Advancement: Adventure)
2. **Monster Hunter** - Kill 1 Creeper. (Advancement: Monster Hunter)
3. **Take Aim** - Craft a Bow. (Proxy: shoot a mob for L)
4. **Sniper Duel** - Craft a Bow. (Proxy: snipe a skeleton from 50m for L)
5. **Bullseye** - Craft a Target. (Proxy: bullseye from 30m for L)
6. **Ol Betsy** - Craft a Crossbow. (Proxy: shoot a crossbow for L)
7. **Two Birds One Arrow** - Craft a Crossbow. (Proxy: piercing double phantom for L)
8. **Whos the Pillager Now** - Kill 5 Pillagers. (Proxy: crossbow-kill a pillager for L)
9. **Arbalistic** - Craft a Crossbow. (Proxy: 5 unique mobs one shot for L)
10. **Throwaway Joke** - Kill 5 Drowned. (Proxy: hit a mob with a trident for L)
11. **Very Very Frightening** - Kill 5 Drowned. (Proxy: Channeling strike a villager for L)
12. **Postmortal** - Kill 5 Evokers. (Proxy: use a Totem of Undying for L)
13. **Mob Kabob** - Craft an Iron Sword. (Proxy: spear charge hitting 5 mobs for L)
14. **Monsters Hunted** - Kill 20 Creepers, 20 Skeletons, 20 Zombies, and 10 Spiders. (Proxy: every hostile for L)
15. **Skeleton Crew** - Kill 25 Skeletons.
16. **Phantom Menace** - Kill 10 Phantoms.
17. **Village Visitor** - Kill 3 Vindicators.
18. **Blowback** - Kill 1 Breeze. (Proxy: deflect breeze charge kill for L)
19. **Who Needs Rockets** - Kill 3 Breezes. (Proxy: launch 8 blocks with wind charge for L)
20. **Over Overkill** - Craft a Mace. (Proxy: 50 hearts in one mace hit for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Farm branch

30 steps. Finish each to unlock the next.

1. **Husbandry Tab** - Craft 1 Bread. (Proxy: eat food for L)
2. **A Seedy Place** - Plant 16 Wheat Seeds on farmland. (Proxy: plant a crop for L)
3. **Parrots and the Bats** - Craft 16 Wheat (unpack a hay bale, or craft wheat from hay). (Proxy: breed any animal for L)
4. **Best Friends Forever** - Tame 1 Wolf. (Advancement: Best Friends Forever)
5. **Fishy Business** - Catch 1 fish. (Advancement: Fishy Business)
6. **A Balanced Diet** - Craft 1 Bread, then eat everything on L. (Proxy: eat every food for L)
7. **Bee Our Guest** - Craft 8 Glass Bottles. (Proxy: bottle honey safely for L)
8. **Wax On** - Craft a Honeycomb Block. (Proxy: wax copper for L)
9. **Wax Off** - Craft an Iron Axe. (Proxy: scrape waxed copper for L)
10. **Total Beelocation** - Craft a Beehive. (Proxy: silk touch nest with 3 bees for L)
11. **Complete Catalogue** - Tame 3 Cats. (Proxy: all cat variants for L)
12. **Serious Dedication** - Craft a Diamond Hoe. (Advancement: netherite hoe for L; smithing does not count)
13. **Two by Two** - Craft 64 Wheat. (Proxy: breed every animal for L)
14. **Bread Basket** - Craft 64 Bread.
15. **Fish Master** - Catch 30 fish.
16. **Stay Hydrated** - Place 1 Dried Ghast. (Proxy: place in water for L)
17. **Friend in Me** - Kill 3 Evokers. (Proxy: allay delivery for L)
18. **Whatever Floats Your Goat** - Craft an Oak Boat. (Proxy: boat with a goat for L)
19. **Glow and Behold** - Kill 4 Glow Squid. (Proxy: glow a sign for L)
20. **Bukkit Bukkit** - Craft a Bucket. (Proxy: bucket a tadpole for L)
21. **Uh Oh** - Craft 1 TNT. (Proxy: sulfur cube absorbs TNT for L)
22. **Smells Interesting** - Craft a Brush. (Proxy: obtain a Sniffer Egg for L)
23. **Birthday Song** - Craft a Cake. (Proxy: allay cake on note block for L)
24. **Squad Hops into Town** - Craft 3 Leads. (Proxy: leash all frog variants for L)
25. **Little Sniffs** - Place 1 Torchflower. (Proxy: feed a snifflet for L)
26. **Powers Combined** - Kill 9 Magma Cubes. (Proxy: all 3 froglights for L)
27. **Planting the Past** - Place 1 Torchflower. (Proxy: plant sniffer seed for L)
28. **Good as New** - Craft a Brush. (Proxy: repair wolf armor with scutes for L)
29. **The Whole Pack** - Tame 3 Wolves. (Proxy: all wolf variants for L)
30. **Shear Brilliance** - Craft Shears. (Proxy: shear wolf armor for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Explore branch

18 steps. Finish each to unlock the next.

1. **Sweet Dreams** - Craft a White Bed. (Proxy: sleep in a bed for L)
2. **Adventuring Time** - Kill 1 Cow, Squid, Polar Bear, Turtle, and Goat. (Proxy: every Overworld biome for L)
3. **Country Lode** - Craft a Lodestone. (Proxy: use a compass on it for L)
4. **Is It a Bird** - Craft a Spyglass. (Proxy: look at a parrot for L)
5. **Is It a Balloon** - Craft a Spyglass. (Proxy: spyglass a ghast for L)
6. **Is It a Plane** - Craft a Spyglass. (Proxy: spyglass the dragon for L)
7. **Caves and Cliffs** - Craft a Bucket. (Proxy: survive world-height fall for L)
8. **Light as a Rabbit** - Craft Leather Boots. (Proxy: walk powder snow for L)
9. **Sound of Music** - Craft a Jukebox. (Proxy: play a disc in a meadow for L)
10. **Sneak 100** - Craft 16 White Wool. (Proxy: sneak near sensor or warden for L)
11. **It Spreads** - Kill 5 Zombies. (Proxy: kill near a sculk catalyst for L)
12. **Cartographer** - Craft an empty Map.
13. **Deep Dark Prep** - Craft 16 White Wool.
14. **Heart Transplanter** - Place 1 Creaking Heart. (Advancement: Heart Transplanter)
15. **Respecting the Remnants** - Craft a Brush. (Proxy: brush a suspicious block for L)
16. **Careful Restoration** - Craft a Decorated Pot. (Proxy: pot from 4 sherds for L)
17. **Isnt It Scute** - Craft a Brush. (Proxy: brush an armadillo for L)
18. **Star Trader** - Craft 16 Ladders. (Proxy: trade at build limit for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Ocean branch

8 steps. Finish each to unlock the next.

1. **What a Deal** - Kill 3 Zombie Villagers. (Proxy: trade with a villager for L)
2. **Hero of the Village** - Kill 10 Pillagers. (Proxy: win a raid for L)
3. **Voluntary Exile** - Kill 1 Pillager. (Proxy: kill a raid captain for L)
4. **Hired Help** - Smelt 36 Iron Ingots. (Proxy: summon an iron golem for L)
5. **Tactical Fishing** - Craft a Bucket. (Proxy: bucket a fish for L)
6. **Cutest Predator** - Craft a Bucket. (Proxy: bucket an axolotl for L)
7. **Healing Power of Friendship** - Kill 5 Drowned. (Proxy: win a fight with axolotl for L)
8. **Ocean Monument Run** - Kill 1 Elder Guardian.

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Magic branch

10 steps. Finish each to unlock the next.

1. **Enchanter** - Craft an Enchanting Table. (Proxy: enchant an item for L)
2. **Local Brewery** - Craft a Brewing Stand. (Proxy: brew a potion for L)
3. **A Furious Cocktail** - Craft 16 Glass Bottles. (Proxy: every potion effect for L)
4. **How Did We Get Here** - Kill 1 Elder Guardian, 1 Evoker, and 1 Wither Skeleton. (Proxy: every effect for L)
5. **Power of Books** - Craft a Chiseled Bookshelf. (Proxy: read with comparator for L)
6. **Zombie Doctor** - Craft a Golden Apple. (Proxy: cure a zombie villager for L)
7. **Surge Protector** - Craft a Lightning Rod. (Proxy: protect a villager for L)
8. **Sticky Situation** - Craft 4 Honey Blocks. (Proxy: slide on honey for L)
9. **Crafters Crafting Crafters** - Craft a Crafter. (Proxy: crafter crafts a crafter for L)
10. **Lighten Up** - Craft a Copper Bulb. (Proxy: scrape oxidized lit bulb for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Boss branch

8 steps. Finish each to unlock the next.

1. **Spooky Scary Skeleton** - Kill 10 Wither Skeletons. (Proxy: obtain a skull for L)
2. **Withering Heights** - Kill 15 Wither Skeletons. (Proxy: summon the Wither for L)
3. **Bring Home the Beacon** - Craft a Beacon. (Proxy: activate a beacon for L)
4. **Beaconator** - Smelt 64 Iron Ingots for pyramid prep. (Proxy: full beacon for L)
5. **Wither Showdown** - Kill the Wither.
6. **Trials Edition** - Kill 5 Breezes. (Proxy: enter a Trial Chamber for L)
7. **Under Lock and Key** - Kill 8 Breezes. (Proxy: unlock a Vault for L)
8. **Revaulting** - Kill 5 Breezes. (Proxy: ominous vault for L)

Source: `server/plugins/Quests/storage/quests.yml`  
Source: `dev/quests-branch-map.json`

### Kitchen branch

11 steps. Custom recipe chain.

**Plant Wheat** -> Bake Bread -> Cook Steak -> Make Jam -> Cook Curry -> Blast Gravel -> Blast Sand -> Leather Shulker -> Calcite Prismarine -> Log Chests -> Clay Statue.

Uses custom recipes where available: flour from wheat, jam from berries (shows as poisonous potato), leather shulkers (8 leather + chest), calcite prismarine (calcite + raw copper), clay statues (clay -> goat horn). Vanilla alternatives remain available.

Source: `dev/kitchen-chain.json`  
Source: `mod-guides/snax-kitchen.md`

### Hybrids branch

4 steps. Craft copper/iron/diamond Dolabra and Mattock (Quests tracks the vanilla axe/hoe id; ask-messages name the hybrid).

Source: `dev/hybrids-chain.json`

### Alloys branch

4 steps. Craft the vanilla base pieces, then smith Hepatizon / Shakudo / Steel / Electrum. The built-in enchantments stay on the smithing result. No netherite-craft objective.

Source: `dev/alloys-chain.json`

### Fisher branch

Catch fish, then get an emerald. Fishermen buy biome fish for emeralds.

Source: `dev/fisher-chain.json`

### Abbey / warding branch

Craft and place a Warding Stone, then map new chunks. Abbeys only generate in ungenerated terrain. No Papal Outpost (that would rewrite pillager outposts).

Source: `dev/abbey-chain.json`

## Global Kill path

Shared progress (`share-progress-level: 1`). One tip active at a time. Tier counts scale by mob difficulty. Full chain order:

| # | Mob | Tier 1 | Tier 2 | Tier 3 |
|---|-----|--------|--------|--------|
| 1 | Zombie | 100 | 500 | 1000 |
| 2 | Skeleton | 100 | 500 | 1000 |
| 3 | Spider | 100 | 500 | 1000 |
| 4 | Creeper | 50 | 250 | 500 |
| 5 | Drowned | 50 | 200 | 500 |
| 6 | Slime | 50 | 200 | 500 |
| 7 | Witch | 25 | 100 | 250 |
| 8 | Pillager | 50 | 200 | 500 |
| 9 | Enderman | 25 | 100 | 250 |
| 10 | Guardian | 25 | 100 | 250 |
| 11 | Phantom | 25 | 100 | 250 |
| 12 | Piglin | 50 | 200 | 500 |
| 13 | Hoglin | 50 | 200 | 500 |
| 14 | Blaze | 50 | 200 | 500 |
| 15 | MagmaCube | 50 | 200 | 500 |
| 16 | WitherSkeleton | 25 | 100 | 250 |
| 17 | Ghast | 25 | 100 | 250 |
| 18 | Shulker | 25 | 100 | 250 |
| 19 | Cow | 50 | 200 | 500 |
| 20 | Sheep | 50 | 200 | 500 |
| 21 | Chicken | 50 | 200 | 500 |

### Kill quest list (in order)

1. **Together - Kill 100 Zombies** - Server goal: kill 100 Zombies together. (shared progress)
2. **Together - Kill 500 Zombies** - Server goal: kill 500 Zombies together. (shared progress)
3. **Together - Kill 1000 Zombies** - Server goal: kill 1000 Zombies together. (shared progress)
4. **Together - Kill 100 Skeletons** - Server goal: kill 100 Skeletons together. (shared progress)
5. **Together - Kill 500 Skeletons** - Server goal: kill 500 Skeletons together. (shared progress)
6. **Together - Kill 1000 Skeletons** - Server goal: kill 1000 Skeletons together. (shared progress)
7. **Together - Kill 100 Spiders** - Server goal: kill 100 Spiders together. (shared progress)
8. **Together - Kill 500 Spiders** - Server goal: kill 500 Spiders together. (shared progress)
9. **Together - Kill 1000 Spiders** - Server goal: kill 1000 Spiders together. (shared progress)
10. **Together - Kill 50 Creepers** - Server goal: kill 50 Creepers together. (shared progress)
11. **Together - Kill 250 Creepers** - Server goal: kill 250 Creepers together. (shared progress)
12. **Together - Kill 500 Creepers** - Server goal: kill 500 Creepers together. (shared progress)
13. **Together - Kill 50 Drowned** - Server goal: kill 50 Drowned together. (shared progress)
14. **Together - Kill 200 Drowned** - Server goal: kill 200 Drowned together. (shared progress)
15. **Together - Kill 500 Drowned** - Server goal: kill 500 Drowned together. (shared progress)
16. **Together - Kill 50 Slimes** - Server goal: kill 50 Slimes together. (shared progress)
17. **Together - Kill 200 Slimes** - Server goal: kill 200 Slimes together. (shared progress)
18. **Together - Kill 500 Slimes** - Server goal: kill 500 Slimes together. (shared progress)
19. **Together - Kill 25 Witches** - Server goal: kill 25 Witches together. (shared progress)
20. **Together - Kill 100 Witches** - Server goal: kill 100 Witches together. (shared progress)
21. **Together - Kill 250 Witches** - Server goal: kill 250 Witches together. (shared progress)
22. **Together - Kill 50 Pillagers** - Server goal: kill 50 Pillagers together. (shared progress)
23. **Together - Kill 200 Pillagers** - Server goal: kill 200 Pillagers together. (shared progress)
24. **Together - Kill 500 Pillagers** - Server goal: kill 500 Pillagers together. (shared progress)
25. **Together - Kill 25 Endermen** - Server goal: kill 25 Endermen together. (shared progress)
26. **Together - Kill 100 Endermen** - Server goal: kill 100 Endermen together. (shared progress)
27. **Together - Kill 250 Endermen** - Server goal: kill 250 Endermen together. (shared progress)
28. **Together - Kill 25 Guardians** - Server goal: kill 25 Guardians together. (shared progress)
29. **Together - Kill 100 Guardians** - Server goal: kill 100 Guardians together. (shared progress)
30. **Together - Kill 250 Guardians** - Server goal: kill 250 Guardians together. (shared progress)
31. **Together - Kill 25 Phantoms** - Server goal: kill 25 Phantoms together. (shared progress)
32. **Together - Kill 100 Phantoms** - Server goal: kill 100 Phantoms together. (shared progress)
33. **Together - Kill 250 Phantoms** - Server goal: kill 250 Phantoms together. (shared progress)
34. **Together - Kill 50 Piglins** - Server goal: kill 50 Piglins together. (shared progress)
35. **Together - Kill 200 Piglins** - Server goal: kill 200 Piglins together. (shared progress)
36. **Together - Kill 500 Piglins** - Server goal: kill 500 Piglins together. (shared progress)
37. **Together - Kill 50 Hoglins** - Server goal: kill 50 Hoglins together. (shared progress)
38. **Together - Kill 200 Hoglins** - Server goal: kill 200 Hoglins together. (shared progress)
39. **Together - Kill 500 Hoglins** - Server goal: kill 500 Hoglins together. (shared progress)
40. **Together - Kill 50 Blazes** - Server goal: kill 50 Blazes together. (shared progress)
41. **Together - Kill 200 Blazes** - Server goal: kill 200 Blazes together. (shared progress)
42. **Together - Kill 500 Blazes** - Server goal: kill 500 Blazes together. (shared progress)
43. **Together - Kill 50 Magma Cubes** - Server goal: kill 50 Magma Cubes together. (shared progress)
44. **Together - Kill 200 Magma Cubes** - Server goal: kill 200 Magma Cubes together. (shared progress)
45. **Together - Kill 500 Magma Cubes** - Server goal: kill 500 Magma Cubes together. (shared progress)
46. **Together - Kill 25 Wither Skeletons** - Server goal: kill 25 Wither Skeletons together. (shared progress)
47. **Together - Kill 100 Wither Skeletons** - Server goal: kill 100 Wither Skeletons together. (shared progress)
48. **Together - Kill 250 Wither Skeletons** - Server goal: kill 250 Wither Skeletons together. (shared progress)
49. **Together - Kill 25 Ghasts** - Server goal: kill 25 Ghasts together. (shared progress)
50. **Together - Kill 100 Ghasts** - Server goal: kill 100 Ghasts together. (shared progress)
51. **Together - Kill 250 Ghasts** - Server goal: kill 250 Ghasts together. (shared progress)
52. **Together - Kill 25 Shulkers** - Server goal: kill 25 Shulkers together. (shared progress)
53. **Together - Kill 100 Shulkers** - Server goal: kill 100 Shulkers together. (shared progress)
54. **Together - Kill 250 Shulkers** - Server goal: kill 250 Shulkers together. (shared progress)
55. **Together - Kill 50 Cows** - Server goal: kill 50 Cows together. (shared progress)
56. **Together - Kill 200 Cows** - Server goal: kill 200 Cows together. (shared progress)
57. **Together - Kill 500 Cows** - Server goal: kill 500 Cows together. (shared progress)
58. **Together - Kill 50 Sheep** - Server goal: kill 50 Sheep together. (shared progress)
59. **Together - Kill 200 Sheep** - Server goal: kill 200 Sheep together. (shared progress)
60. **Together - Kill 500 Sheep** - Server goal: kill 500 Sheep together. (shared progress)
61. **Together - Kill 50 Chickens** - Server goal: kill 50 Chickens together. (shared progress)
62. **Together - Kill 200 Chickens** - Server goal: kill 200 Chickens together. (shared progress)
63. **Together - Kill 500 Chickens** - Server goal: kill 500 Chickens together. (shared progress) 

**Loops:** Final kill quest (Kill 500 Chickens) loops back to first kill quest (Kill 100 Zombies).

Source: `dev/quests-global-chains.json`  
Source: `server/plugins/Quests/storage/quests.yml`

## Global Mine path

Shared progress. Commons use high break counts (**2048 / 8192 / 32768** for dirt-netherrack band). One tip active at a time.

| # | Block | Tier 1 | Tier 2 | Tier 3 |
|---|-------|--------|--------|--------|
| 1 | `DIRT` | 2048 | 8192 | 32768 |
| 2 | `COBBLESTONE` | 2048 | 8192 | 32768 |
| 3 | `STONE` | 2048 | 8192 | 32768 |
| 4 | `DEEPSLATE` | 2048 | 8192 | 32768 |
| 5 | `NETHERRACK` | 2048 | 8192 | 32768 |
| 6 | `GRAVEL` | 1024 | 4096 | 16384 |
| 7 | `SAND` | 1024 | 4096 | 16384 |
| 8 | `ANDESITE` | 1024 | 4096 | 16384 |
| 9 | `DIORITE` | 1024 | 4096 | 16384 |
| 10 | `GRANITE` | 1024 | 4096 | 16384 |
| 11 | `COBBLED_DEEPSLATE` | 1024 | 4096 | 16384 |
| 12 | `OAK_LOG` | 512 | 2048 | 8192 |
| 13 | `SPRUCE_LOG` | 512 | 2048 | 8192 |
| 14 | `BIRCH_LOG` | 512 | 2048 | 8192 |
| 15 | `COAL_ORE` | 256 | 1024 | 4096 |
| 16 | `COPPER_ORE` | 256 | 1024 | 4096 |
| 17 | `IRON_ORE` | 128 | 512 | 2048 |
| 18 | `DEEPSLATE_IRON_ORE` | 128 | 512 | 2048 |
| 19 | `GOLD_ORE` | 64 | 256 | 1024 |
| 20 | `DIAMOND_ORE` | 64 | 256 | 1024 |
| 21 | `DEEPSLATE_DIAMOND_ORE` | 64 | 256 | 1024 |
| 22 | `ANCIENT_DEBRIS` | 8 | 24 | 48 |

### Mine quest list (in order)

1. **Together - Mine 2048 Dirt** - Server goal: mine 2048 Dirt together. (shared progress)
2. **Together - Mine 8192 Dirt** - Server goal: mine 8192 Dirt together. (shared progress)
3. **Together - Mine 32768 Dirt** - Server goal: mine 32768 Dirt together. (shared progress)
4. **Together - Mine 2048 Cobblestone** - Server goal: mine 2048 Cobblestone together. (shared progress)
5. **Together - Mine 8192 Cobblestone** - Server goal: mine 8192 Cobblestone together. (shared progress)
6. **Together - Mine 32768 Cobblestone** - Server goal: mine 32768 Cobblestone together. (shared progress)
7. **Together - Mine 2048 Stone** - Server goal: mine 2048 Stone together. (shared progress)
8. **Together - Mine 8192 Stone** - Server goal: mine 8192 Stone together. (shared progress)
9. **Together - Mine 32768 Stone** - Server goal: mine 32768 Stone together. (shared progress)
10. **Together - Mine 2048 Deepslate** - Server goal: mine 2048 Deepslate together. (shared progress)
11. **Together - Mine 8192 Deepslate** - Server goal: mine 8192 Deepslate together. (shared progress)
12. **Together - Mine 32768 Deepslate** - Server goal: mine 32768 Deepslate together. (shared progress)
13. **Together - Mine 2048 Netherrack** - Server goal: mine 2048 Netherrack together. (shared progress)
14. **Together - Mine 8192 Netherrack** - Server goal: mine 8192 Netherrack together. (shared progress)
15. **Together - Mine 32768 Netherrack** - Server goal: mine 32768 Netherrack together. (shared progress)
16. **Together - Mine 1024 Gravel** - Server goal: mine 1024 Gravel together. (shared progress)
17. **Together - Mine 4096 Gravel** - Server goal: mine 4096 Gravel together. (shared progress)
18. **Together - Mine 16384 Gravel** - Server goal: mine 16384 Gravel together. (shared progress)
19. **Together - Mine 1024 Sand** - Server goal: mine 1024 Sand together. (shared progress)
20. **Together - Mine 4096 Sand** - Server goal: mine 4096 Sand together. (shared progress)
21. **Together - Mine 16384 Sand** - Server goal: mine 16384 Sand together. (shared progress)
22. **Together - Mine 1024 Andesite** - Server goal: mine 1024 Andesite together. (shared progress)
23. **Together - Mine 4096 Andesite** - Server goal: mine 4096 Andesite together. (shared progress)
24. **Together - Mine 16384 Andesite** - Server goal: mine 16384 Andesite together. (shared progress)
25. **Together - Mine 1024 Diorite** - Server goal: mine 1024 Diorite together. (shared progress)
26. **Together - Mine 4096 Diorite** - Server goal: mine 4096 Diorite together. (shared progress)
27. **Together - Mine 16384 Diorite** - Server goal: mine 16384 Diorite together. (shared progress)
28. **Together - Mine 1024 Granite** - Server goal: mine 1024 Granite together. (shared progress)
29. **Together - Mine 4096 Granite** - Server goal: mine 4096 Granite together. (shared progress)
30. **Together - Mine 16384 Granite** - Server goal: mine 16384 Granite together. (shared progress)
31. **Together - Mine 1024 Cobbled Deepslate** - Server goal: mine 1024 Cobbled Deepslate together. (shared progress)
32. **Together - Mine 4096 Cobbled Deepslate** - Server goal: mine 4096 Cobbled Deepslate together. (shared progress)
33. **Together - Mine 16384 Cobbled Deepslate** - Server goal: mine 16384 Cobbled Deepslate together. (shared progress)
34. **Together - Mine 512 Oak Log** - Server goal: mine 512 Oak Log together. (shared progress)
35. **Together - Mine 2048 Oak Log** - Server goal: mine 2048 Oak Log together. (shared progress)
36. **Together - Mine 8192 Oak Log** - Server goal: mine 8192 Oak Log together. (shared progress)
37. **Together - Mine 512 Spruce Log** - Server goal: mine 512 Spruce Log together. (shared progress)
38. **Together - Mine 2048 Spruce Log** - Server goal: mine 2048 Spruce Log together. (shared progress)
39. **Together - Mine 8192 Spruce Log** - Server goal: mine 8192 Spruce Log together. (shared progress)
40. **Together - Mine 512 Birch Log** - Server goal: mine 512 Birch Log together. (shared progress)
41. **Together - Mine 2048 Birch Log** - Server goal: mine 2048 Birch Log together. (shared progress)
42. **Together - Mine 8192 Birch Log** - Server goal: mine 8192 Birch Log together. (shared progress)
43. **Together - Mine 256 Coal Ore** - Server goal: mine 256 Coal Ore together. (shared progress)
44. **Together - Mine 1024 Coal Ore** - Server goal: mine 1024 Coal Ore together. (shared progress)
45. **Together - Mine 4096 Coal Ore** - Server goal: mine 4096 Coal Ore together. (shared progress)
46. **Together - Mine 256 Copper Ore** - Server goal: mine 256 Copper Ore together. (shared progress)
47. **Together - Mine 1024 Copper Ore** - Server goal: mine 1024 Copper Ore together. (shared progress)
48. **Together - Mine 4096 Copper Ore** - Server goal: mine 4096 Copper Ore together. (shared progress)
49. **Together - Mine 128 Iron Ore** - Server goal: mine 128 Iron Ore together. (shared progress)
50. **Together - Mine 512 Iron Ore** - Server goal: mine 512 Iron Ore together. (shared progress)
51. **Together - Mine 2048 Iron Ore** - Server goal: mine 2048 Iron Ore together. (shared progress)
52. **Together - Mine 128 Deepslate Iron Ore** - Server goal: mine 128 Deepslate Iron Ore together. (shared progress)
53. **Together - Mine 512 Deepslate Iron Ore** - Server goal: mine 512 Deepslate Iron Ore together. (shared progress)
54. **Together - Mine 2048 Deepslate Iron Ore** - Server goal: mine 2048 Deepslate Iron Ore together. (shared progress)
55. **Together - Mine 64 Gold Ore** - Server goal: mine 64 Gold Ore together. (shared progress)
56. **Together - Mine 256 Gold Ore** - Server goal: mine 256 Gold Ore together. (shared progress)
57. **Together - Mine 1024 Gold Ore** - Server goal: mine 1024 Gold Ore together. (shared progress)
58. **Together - Mine 64 Diamond Ore** - Server goal: mine 64 Diamond Ore together. (shared progress)
59. **Together - Mine 256 Diamond Ore** - Server goal: mine 256 Diamond Ore together. (shared progress)
60. **Together - Mine 1024 Diamond Ore** - Server goal: mine 1024 Diamond Ore together. (shared progress)
61. **Together - Mine 64 Deepslate Diamond Ore** - Server goal: mine 64 Deepslate Diamond Ore together. (shared progress)
62. **Together - Mine 256 Deepslate Diamond Ore** - Server goal: mine 256 Deepslate Diamond Ore together. (shared progress)
63. **Together - Mine 1024 Deepslate Diamond Ore** - Server goal: mine 1024 Deepslate Diamond Ore together. (shared progress)
64. **Together - Mine 8 Ancient Debris** - Server goal: mine 8 Ancient Debris together. (shared progress)
65. **Together - Mine 24 Ancient Debris** - Server goal: mine 24 Ancient Debris together. (shared progress)
66. **Together - Mine 48 Ancient Debris** - Server goal: mine 48 Ancient Debris together. (shared progress)

**Loops:** Final mine quest (Mine 48 Ancient Debris) loops back to first mine quest (Mine 2048 Dirt).

Source: `dev/quests-global-chains.json`  
Source: `server/plugins/Quests/storage/quests.yml`

## See also

- [`mod-guides/quests-classic.md`](../mod-guides/quests-classic.md)
- [Dailies](snaxcraft-dailies.md)
- [Quest Point shop](snaxcraft-qp-shop.md)
- [Kitchen recipes](snaxcraft-kitchen.md)
- [Hybrid tools](snaxcraft-hybrids.md)
- [Alloy equipment](snaxcraft-alloys.md)
- Modrinth Quests Classic: https://modrinth.com/plugin/quests.classic

