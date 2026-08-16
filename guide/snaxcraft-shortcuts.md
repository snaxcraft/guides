# snaxcraft crafting and material shortcuts

**Edition:** Java  
**Version:** 26.2 Paper  
**Last verified:** 2026-08-15  
**Applies to:** snaxcraft server content

These non-food recipes make common building, storage, and decorative items easier to obtain. Food recipes are in the [snaxcraft kitchen cookbook](snaxcraft-kitchen.md).

## Material conversion

### Cobblestone or cobbled deepslate to gravel

Put **1 Cobblestone or 1 Cobbled Deepslate** in a blast furnace to make **1 Gravel**.

**Time:** 5 seconds  
**Experience:** 0.1

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/gravel_from_blasting_cobble.json`

### Gravel to sand

Put **1 Gravel** in a blast furnace to make **1 Sand**.

**Time:** 5 seconds  
**Experience:** 0.1

Together, the two blasting recipes make this chain:

```text
Cobblestone or Cobbled Deepslate -> Gravel -> Sand
```

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/sand_from_blasting_gravel.json`

## Building and storage

### Leather shulker box

Surround a Chest with 8 Leather to make **1 Shulker Box**:

```text
LLL
LCL
LLL
```

`L` = Leather and `C` = Chest.

This is an extra shortcut. The vanilla recipe with two Shulker Shells and a Chest still works.

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/leather_shulker_box.json`
Source: https://minecraft.wiki/w/Shulker_Box

### Four chests from logs

Use 8 Logs in the normal chest outline to make **4 Chests**:

```text
LLL
L L
LLL
```

`L` = any item in the Logs item tag, including supported log and stem types.

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/chest_from_logs.json`

### Prismarine from calcite and raw copper

Use a 2x2 checker pattern to make **4 Prismarine**:

```text
CR
RC
```

`C` = Calcite and `R` = Raw Copper. The pattern can occupy any 2x2 corner of the crafting table.

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/prismarine_from_calcite.json`

## Decorations

### Cheerful clay statue

Craft **4 Clay Balls + 1 Yellow Dye** shapelessly to make **1 Cheerful Clay Statue**.

The statue can be used like a horn and carries the description **Rejoice**.

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/cheerful_clay_statue.json`

### Mournful clay statue

Craft **4 Clay Balls + 1 Black Dye** shapelessly to make **1 Mournful Clay Statue**.

The statue can be used like a horn and carries the description **Lament**.

Source: `dev/snaxcraft-content-pack/datapack/data/snax/recipe/mournful_clay_statue.json`

## Credit and license

Recipes and assets adapted from Matcha Flavoured by **klei_wright**, licensed **CC-BY-NC-SA 4.0**.

Source: https://modrinth.com/datapack/matcha-flavoured

## See also

- [Kitchen recipes](snaxcraft-kitchen.md)
- [Kitchen branch in the challenge ladder](snaxcraft-quests.md#kitchen-branch)
