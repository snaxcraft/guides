# SnaxCraft Content and SnaxKitchen (ops)

**Plugin:** SnaxKitchen  
**Jar:** `server/plugins/SnaxKitchen.jar`  
**Content bundle:** SnaxCraft Content
**Role:** SnaxKitchen gates Kitchen recipe ingredients; SnaxCraft Content supplies all custom datapack and resource-pack features
**License:** Matcha Flavoured assets and recipes by klei_wright, CC-BY-NC-SA 4.0  
**Last verified:** 2026-08-21  
**Host:** Cybrancee **Stone** (4GB) -- see `dev/host-profile.md`

## Purpose

SnaxCraft Content is the combined datapack and resource pack for custom food, QoL recipes, hybrid tools, alloys, fishing, Abbey structures, and warding. The separately named SnaxKitchen plugin only gates Kitchen recipe ingredients so plain carrier items cannot be used as custom ingredients.

## Key recipes

- **Flour from wheat:** Mill wheat into flour using custom recipes
- **Jam from berries:** Craft sweet berry jam (poisonous-potato carrier with snax model)
- **Cheese / Milk Bottle:** Cookie and beetroot-soup carriers with snax models (Matcha painted those vanilla textures; we copy them under `snax:` so plain cookies/soup stay vanilla)
- **Curry cooking:** Smelt uncooked curry into cooked meals
- **Gravel from cobble:** Blast furnace cobblestone/deepslate into gravel
- **Sand from gravel:** Blast gravel into sand
- **Leather shulkers:** Craft shulker boxes using 8 leather + chest (End recipe still available)
- **Calcite prismarine:** Craft prismarine from calcite + raw copper (vanilla shards still work)
- **Clay statues:** Craft goat horns from clay (cheerful/mournful variants)

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/`

## Installation components

1. **Datapack:** Install the built zip on the host as `world/datapacks/snaxcraft-content-datapack.zip`. This is a dangerous world path, so SFTP deployment requires `-ForceDangerous` and explicit user intent. Remove any older renamed copy so the same namespaces are not loaded twice.
2. **Plugin jar:** Install as `server/plugins/SnaxKitchen.jar`.
3. **Resource pack:** Publish the pack as a GitHub Release in `snaxcraft/resourcePack` during an approved stable promotion.

## Resource pack deployment

- **Host:** GitHub public repo `snaxcraft/resourcePack`
- **Distribution:** Release asset URL in `server.properties`
- **Update process:** Build zip locally, upload GitHub Release, update server.properties with new URL + sha1

## Hybrid tools, alloys, fishing, Abbey

The same datapack zip also ships:

- Copper / iron / diamond Dolabra and Mattock
- Hepatizon, Shakudo, Steel, Electrum, Adamant smithing (Matcha built-in enchantments kept)
- Biome fish loot and fisherman emerald trades
- Warding stones and Abbey structures in **new chunks only**
- No Papal Outpost (that Matcha feature rewrites pillager outposts)

Source: `dev/snaxcraft-content-pack/datapack/data/snax_tools/recipe/`
Source: `server/plugins/CommandPanels/panels/qp-gear-hybrids.yml`
Source: `server/plugins/CommandPanels/panels/qp-gear-alloys.yml`

## Quest integration

Kitchen / daily **smelt** quests use Quests Classic `items-to-smelt` (result material).

| Cook kind | Stations that advance Quests |
|-----------|------------------------------|
| Food (steak, bread, cooked meats) | Furnace, smoker, campfire |
| Materials (ingots, gravel, sand, glass) | Furnace, blast furnace |

Quests natively counts result takes from furnace / smoker / blast-furnace GUIs. Campfires have no result GUI, so **SnaxKitchen** credits `SMELT_ITEM` when food finishes cooking on a campfire the player recently used.

Smokers cook raw meats/fish/potato into `cooked_*` / baked first. **Charred meat, fish, and potato** are a second smoke: put the already-cooked food back in the smoker.

Quests Classic rejects snax foods that carry lore against plain `items-to-smelt` stacks. SnaxKitchen credits a meta-less copy when you take snax food from a furnace/smoker result (and when campfire cooking finishes), so Kitchen/daily food smelt quests advance.

Source: `server/plugins/Quests/storage/quests.yml`
Source: `dev/snax-kitchen/src/main/java/com/snaxcraft/kitchen/FoodCookQuestListener.java`

## Performance notes

Minimal impact on Stone 4GB - datapack recipes only load on world start. Resource pack is client-side.

## Commands

None - recipe integration is automatic through datapack.

## Config

Recipe configurations are built into the datapack. No runtime config files.

## Smoke test

After a full restart, test the following on the host:

1. Run `/reload` and confirm chat shows `[snax] kitchen datapack loaded`.
2. Craft flour from 3 wheat.
3. Craft dough from flour plus egg, or from flour plus a water bottle.
4. Smelt dough into bread (furnace, smoker/naan path, or campfire).
5. Cook raw beef into steak in a **furnace, smoker, or campfire**; confirm Kitchen / daily steak smelt progress.
6. Blast cobblestone into gravel, then blast gravel into sand (blast furnace; furnace also counts for Quests if the recipe runs there).
7. Craft a shulker box from 8 leather around a chest.
8. Confirm `Kitchen - Plant Wheat` advances when wheat is planted.
9. Confirm `Kitchen - Bake Bread` advances when dough is cooked into bread.
10. Inspect every `snaxKitchen*` quest in `server/plugins/Quests/storage/quests.yml`; each must contain `give-at-login: false` and `share-progress-level: 0`.

## License and attribution

The adapted Matcha Flavoured recipes and assets are by klei_wright and are licensed under CC-BY-NC-SA 4.0. Keep attribution, share adaptations under the same license, and do not sell them.

## Troubleshooting

- **Recipes not working:** Verify datapack is in `world/datapacks/` and enabled
- **Missing textures:** Check resource pack URL in server.properties and client download
- **Quest not completing:** Ensure crafting produces the correct vanilla item ID (not custom variants)

---

Source: `dev/snaxcraft-content-pack/CREDITS.txt`
Source: https://modrinth.com/datapack/matcha-flavoured