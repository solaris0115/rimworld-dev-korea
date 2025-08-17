The Humanoid Alien Races framework lets you create alien races easily without writing your own code, however alien races in general are still a relatively advanced topic. It's highly recommended that you read up on or review the following topics on the main RimWorld wiki's tutorial section:

* [Mod folder structure](https://rimworldwiki.com/wiki/Modding_Tutorials/Mod_folder_structure) - How to create a mod folder and where files need to be placed for them to be read correctly by RimWorld.
* XML Defs (link TBD)

## Important Tip

* Most features in the HAR framework fall back to human defaults if omitted. If you are unsure what something does or whether you need it, then leave it out unless the game complains about it!

# First Steps

The first milestone in making a custom race is creating a race Def using HAR's `AlienRace.ThingDef_AlienRace` custom subclass and at least one `PawnKindDef`.

## `AlienRace.ThingDef_AlienRace`

This is the class that represents the base stats and configuration for your alien race. For the purpose of this example we are going to inherit from `Human`, as that will allow our race to inherit all of its base stats from the normal human Def.

```xml
<AlienRace.ThingDef_AlienRace ParentName="Human">
    <defName>ExampleAlien</defName>
    <label>example alien</label>
    <description>This is an example alien race that was created for the wiki tutorial.</description>
</AlienRace.ThingDef_AlienRace>
```

For more advanced users with races that are highly divergent from human norms, inheriting from `BasePawn` will make it easier to override values, but you will also need to fill in more missing values before your race will work properly.

## `PawnKindDef`

`PawnKindDefs` are Defs that define preset spawn configurations for races. You must have at least one in order to spawn your race's pawns using Development Mode.

```xml
<PawnKindDef ParentName="BasePlayerPawnKind">
    <defName>ExampleAlienColonist</defName>
    <label>colonist</label>
    <race>ExampleAlien</race>
    <defaultFactionType>PlayerColony</defaultFactionType>

    <!-- This is a required field. 13~21 is the default value for Crashlanded player colonists. -->
    <initialResistanceRange>13~21</initialResistanceRange>
</PawnKindDef>
```

As before, we are using the vanilla `BasePlayerPawnKind` as a parent so as to inherit some default values.

## Test It!

At this point, you should be able to load your mod in RimWorld and spawn one of your pawns, going to the Dev Tools, selecting "Spawn Pawn", choosing ExampleAlienColonist, and clicking on the map to create an instance of that PawnKind. It is strongly recommended that you add or enable features for your race one at a time and test after doing so each time. If you enable several features at once and the game stops loading, then you will have a much harder time figuring out what's broken!

![Dev Mode Screenshot 1](https://i.imgur.com/N01k514.png)  
![Arrow](https://i.imgur.com/KtCisWJ.png)  
![Dev Mode Screenshot 2](https://i.imgur.com/xnJ3Py3.png)  
![Arrow](https://i.imgur.com/KtCisWJ.png)  
![Dev Mode Screenshot 3](https://i.imgur.com/SLBArh1.png)  
![Arrow](https://i.imgur.com/KtCisWJ.png)  
![Dev Mode Screenshot 4](https://i.imgur.com/uWZ8Pue.png)

## Example Race Repository

A repository with a working example of the above along with some additional comments for context is available [here](https://github.com/Aelanna/ExampleAlienRace).

# Next Steps

After you've created the scaffolding for your race, you can dive into the specific features of HAR! If you are a new modder in general, be sure to check out the [[New Modder Tips & Resources|New-Modder-Tips-and-Resources]] as well!

## Intermediate Topics

These are some of the core features of Humanoid Alien Races and that which is used most often to make a race unique:

* [[General Settings]] - Sets most of a race's core features. Includes color channels, body addons (additional drawn textures), age settings, and so on.
* [[Graphic Paths]] - Allows you to use custom graphics for heads, bodies, skulls, and skeletons.
* [[Style Settings]] - (1.3) Allows you to add, restrict, or disable categories for hair, beards, and tattoos.
* [[Thought Settings]] - Allows you to restrict or replace thoughts.
* [[Relation Settings]] - Allows you to disable or adjust the chances of specific family relations generating for your race, as well as rename specific relationships.
* [[Race Restriction]] -- Allows you to allow or disallow research projects, apparel, weapons, buildings, recipes, plants, traits, food, animal handling, and WorkGivers. Also lets you add Learning Helper entries triggers when a member of your race joins the colony.
* [[Compatibility]] - Allows you to set certain properties for your race for compatibility with certain mods.
* [[Backstories]] - Allows you to create custom backstories for your race.
* [[PawnBios|PawnBioDef]] - Allows you to create preset characters for your race with specific names and backstories.
* [[Royalty Compatibility|Royalty-Compatibility]] - Instructions on making your race compatible with Royalty DLC mechanics.
* [[Miscellaneous|Misc]] - Additional customization options for custom races.

## Advanced Topics

* (PH) Creating Custom Factions
