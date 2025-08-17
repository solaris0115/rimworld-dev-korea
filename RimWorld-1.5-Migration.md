This a guide to vanilla RimWorld changes and compatibility updates for Humanoid Alien Races for RimWorld 1.5 and the upcoming Anomaly DLC. This is a work in progress and will be updated as new information is available; please join the **[Alien Races Discord](http://discord.gg/XMCRj46)** for the latest information!

This document is primarily focused on game changes specific to Humanoid Alien Races; for a broader record of game changes, please also check out the [RimWorld 1.5 Mod Updates](https://rimworldwiki.com/wiki/Modding_Tutorials/RimWorld_1.5_Mod_Updates) page on the regular RimWorld Wiki.

You can get the current development version of Humanoid Alien Races by downloading the Dev branch from GitHub or by using the Steam Workshop item here: **[Humanoid Alien Races - Dev](https://steamcommunity.com/sharedfiles/filedetails/?id=2640710953)** Note that since it has a different packageId from the live version of HAR, mods may throw an error about missing dependencies. This is normal and can safely be ignored; loading both at the same time will break your game.

# RimWorld Core Changes

## ```BackstoryDef```
The ```baseDesc``` field is now ```description``` to be consistent with other vanilla Def types.

Skill notation in vanilla BackstoryDef has been improved with a custom parser:
```xml
<skillGains>
  <Construction>4</Construction>
  <Crafting>2</Crafting>
  <Mining>2</Mining>
  <Plants>2</Plants>
  <Artistic>-1</Artistic>
  <Cooking>-1</Cooking>
  <Shooting>-1</Shooting>
</skillGains>
```
The following regular expression can be used to convert from the old <key><value> notation:
```
<li>\s*<key>(.*)</key>\s*<value>(.*)</value>\s*</li>

<$1>$2</$1>
```
You can use them to search and replace in entire files rather than changing them manually. A screenshot showing how to do a regex search and replace in Notepad++ is shown here:

![Regular expression search and replace in Notepad++](https://i.imgur.com/supZDeG.png)

HAR-specific forcedTraitsChance and disallowedTraitsChance entries have new, updated syntax. Please see the HAR-specific section further down.

## ```BodyDef```
The Human ```BodyDef``` has been altered:
* Tongue coverage changed from 0 to 0.001. This is presumably to fix issues with attacks throwing errors when damaged.
* ```visibleHediffRots``` tag added to left and right eyes, which is a list of rotations for which hediffs for those eyes should be drawn.
* ```flipGraphic``` tag added to left eye, left ear, left shoulder, clavicle, left arm, left hand. This seems to be used by the animation system, such as for when pawns are crawling to safety.

## ```FleshTypeDef```
Now has a ```isOrganic``` flag, which is now checked by ```RaceProperties.IsFlesh``` instead of being hardcoded to return false only for mechanoids.

## ```LifeStageDef```
Custom lifestages can define custom ```silhouetteGraphicData``` for when the vanilla camera is zoomed out. Please check out the vanilla humanlike LifeStageDefs for more information.

## ```PawnKindDef```
* ```mutant``` field of type MutantDef. Presumably used by Anomaly in some way.
* ```studiableAsPrisoner```, also presumably used by Anomaly in some way.
* ```canStrip``` - Currently used by mech kinds.
* ```nakedChance``` - 0~1, sets a chance that the pawn skips all apparel generation except for ```specificApparelRequirements```. Only works for non-colonist kinds.

## ```RaceProperties```
* ```deathActionWorkerClass``` has been replaced by ```deathAction```, which is a ```DeathActionProperties``` object with more configuration and some caching capability.
* ```doesntMove``` - If set, makes it so that a pawn is not considered Downed if its Moving capacity falls below 15%.
* ```renderTree``` - Sets the PawnRenderTreeDef for this race. _If you are inheriting from the Human ThingDef, then most HAR races should not have to change this unless they are not using BodyAddons and are instead doing entirely custom rendering. If you inherit from BasePawn, then you should set your renderTree to "Humanlike"._
* ```startingAnimation``` - New AnimationDef object. Unused in any Core race, probably something used by Anomaly.
* ```linkedCorpseKind``` - Allows a race to use the corpse from another race. Also unused in Core and probably an Anomaly feature.
* ```canOpenFactionlessDoors``` - Defaults to ```true``` and is not currently overridden by any Core race.
* ```alwaysAwake``` - Makes a race considered conscious even if its Consciousness drops below 30%. Also used by any Core race.
* ```alwaysViolent``` - Used as a shortcut in pawn generation; skips over work tag and Manipulation checks if true.
* ```isImmuneToInfection``` - If set to ```true```, then this race cannot contract diseases or lung rot.
* ```bleedRateFactor``` - Default 1.0, multiplied into injury and missing part calculations. Pawn_HealthTracker returns `CanBleed=false` if this value is 0.
* ```canBecomeShambler``` - Presumably something to do with Anomaly.
* ```disableIgniteVerb``` - Disallows this race from setting buildings on fire when hostile.
* ```detritusLeavings``` - List of possible things to spawn when a member of this race dies
* ```overrideShouldHaveAbilityTracker``` - If set to ```true```, creates a `Pawn_AbilityTracker` for this race even if it isn't Humanlike or a mechanoid. Does not affect HAR races.
* ```ShouldHaveAbilityTracker``` property - Reads the above field in addition to Humanlike and IsMechanoid.
* ```hasMeat``` - Default ```true```. If set to ```false```, no meat def is generated for this race.
* ```hasCorpse``` - Default ```true```. If set to ```false```, then no corpse is generated for this race.
* ```corpseHiddenWhileUndiscovered``` - If set to ```true```, then this race's corpse is added to ```HiddenItemsManager``` and won't show up in storage filters until the player sees one for the first time.
* ```soundMoving``` - New field of type ```SoundDef```, can be used to specify a Sustainer sound that plays and is maintained while the pawn is actively moving.
* ```Animal``` property now checks !IsAnomalyEntity (in addition to checking !ToolUser && IsFlesh).
* ```bloodDef``` will no longer default to `Filth_Blood` if left blank. Pawns with no bloodDef will not show bleeding on the health tab, cannot bleed to death, and generate no filth when injured. **Those inheriting from `BasePawn' will need to add this field for their race to bleed normally. If you do not do this, then your race will no longer be able to have their wounds tended properly.**
* ```bloodSmearDef``` - Default ```null```. Defines the filth Def used for blood smears when a pawn is crawling while bleeding.

## Miscellaneous
* Corpse ThingDefs now have RaceProperties copied over from their source race. This can cause false positives if you previously only used ```def.race != null``` to check if a ThingDef was a race; you should also check ```!def.IsCorpse``` now.

# Humanoid Alien Races

The following are changes to the Humanoid Alien Races Framework for RimWorld 1.5:

## Human ThingDef

The ```Human``` ThingDef now has a Name attribute set by vanilla. If you previously used ```HumanRace``` as the ParentName for your race, then you should change it to ```Human``` instead.

If you inherit directly from ```BasePawn```, then you need to add the Humanlike render tree to your race:

```xml
<AlienRace.ThingDef_AlienRace>
  <race>
    <renderTree>Humanlike</renderTree>
  </race>
</AlienRace.ThingDef_AlienRace>
```

## Framework Defs

The following HAR Def entries have been prefixed for compatibility safety:
* AlienRaceSettings_Humans (RaceSettings) -> HAR_AlienRaceSettings_Humans
* alienCorpseCategory (ThingCategoryDef) -> HAR_AlienCorpseCategory
* XenophobeVsXenophile (ThoughtDef) -> HAR_XenophobeVsXenophile
* XenophobiaVsAlien (ThoughtDef) -> HAR_XenophobiaVsAlien
* AlienVsXenophobia (ThoughtDef) -> HAR_AlienVsXenophobia
* Xenophobia (TraitDef) -> HAR_Xenophobia

## Removed Fields

The following fields which were previously marked as Obsolete have been fully removed:
* ThingDef_AlienRace/alienRace/alienPartGenerator/getsGreyAt - use oldHairAgeRange, oldHairAgeCurve, or oldHairColorGen instead.
* ThingDef_AlienRace/alienRace/alienPartGenerator/headOffsetSpecific - marked obsolete prior to 1.4, use headOffsetDirectional instead.
* ThingDef_AlienRace/alienRace/alienPartGenerator/headFemaleOffsetSpecific - Renamed to headFemaleOffsetDirectional, which was marked Obsolete prior to 1.4.

## Traits

```forcedTraitsChance``` and ```disallowedTraitsChance``` have been upgraded with a recursive options notation that allows for specific random outcomes. This applies to ```forcedRaceTraitEntries``` and ```disallowedRaceTraitEntries``` on the race definition as well.

In this example, generated pawns have a 50% chance to generate with either Hard Worker or Industrious and cannot have Slowpoke:
```xml
<forcedTraitsChance>
  <li>
    <options>
      <li>
        <defName Degree="1">Industriousness</defName>
      </li>
      <li>
        <defName Degree="2">Industriousness</defName>
      </li>
    </options>
    <count>1</count>
    <chance>50</chance>
  </li>
</forcedTraitsChance>
<disallowedTraitsChance>
  <li>
    <defName Degree="-1">SpeedOffset</defName>
  </li>
</disallowedTraitsChance>
```

In this example, male pawns would be given the Tough trait while female pawns would be given Pretty:
```xml
<forcedTraitsChance>
  <li>
    <defName>Tough</defName>
    <commonalityFemale>0</commonalityFemale>
  </li>
  <li>
    <defName Degree="1">Beauty</defName>
    <commonalityMale>0</commonalityMale>
  </li>
</forcedTraitsChance>
```

## BodyAddons

Conditions for rendering BodyAddons has a new mandatory, nestable syntax. All examples below are optional, use only the ones you wish to change.
```xml
<conditions>
  <!-- Draw for the specified stages -->
  <!-- i.e. if you want to replicate drawnDesiccated=false, then use Fresh,Rotting -->
  <RotStage>Fresh,Rotting,Dessicated</RotStage>

  <!-- Draw if the specified body part exists and is not destroyed -->
  <BodyPart>
    <bodyPart>BodyPartDef</bodyPart>
    <bodyPartLabel>distinguishing label</bodyPartLabel>
    <drawWithoutPart>false</drawWithoutPart>
  </BodyPart>

  <!-- Draw only for the specified drafted state -->
  <Drafted>true</Drafted>

  <!-- Draw only if the pawn is actively using the specified JobDef -->
  <Job>LayDown</Job>

  <!-- Draw only if the pawn is in the specified movement state -->
  <Moving>false</Moving>

  <!-- Hide if certain apparel is being worn -->
  <Apparel>
    <hiddenUnderApparelFor>
      <li>Head</li>
      <li>Torso</li>
      <li>Legs</li>
    </hiddenUnderApparelFor>
    <hiddenUnderApparelTag>
      <li>Warcasket</li>
    </hiddenUnderApparelTag>
  </Apparel>

  <!-- Draw only if the specified apparel is worn -->
  <ApparelDef>
    <apparel>Apparel_Tribalwear</apparel>
    <stuff>Leather_Human</stuff>
  </ApparelDef>

  <!-- Draw only for the specified postures -->
  <Posture>
    <drawnStanding>false</drawnStanding>
    <drawnLaying>false</drawnLaying>
    <drawnInBed>false</drawnInBed>
  </Posture>

  <!-- Draw only if the linked body part's health is at or below the specified threshold -->
  <!-- values are a fraction of total health, i.e. 0.0~1.0 -->
  <Damage>1.0</Damage>

  <!-- Draw only for the specified LifeStageDef -->
  <Age>HumanlikeAdult</Age>

  <!-- Draw only if the specified hediff is present -->
  <!-- Hediffs will only be checked on the last resolved BodyPart -->
  <Hediff>BionicSpine</Hediff>
  <Hediff>Burn</Hediff>
  <Severity>0.5</Severity>

  <!-- Draw only if the pawn has the specified BackstoryDef -->
  <Backstory>AlienHulk</Backstory>

  <!-- Draw only for the specified gender -->
  <Gender>Male</Gender>
  <Gender>Female</Gender>

  <!-- Draw only if the pawn has the specified TraitDef -->
  <Trait>Psychopath</Trait>

  <!-- Draw only if the pawn has the specified BodyTypeDef -->
  <BodyType>Hulk</BodyType>

  <!-- Draw only if the pawn has the specified HeadTypeDef -->
  <HeadType>Male_AverageNormal</HeadType>

  <!-- Draw only if the pawn has the specified GeneDef -->
  <Gene>Robust</Gene>

  <!-- Draw only if the pawn is of the specified race ThingDef -->
  <!-- Useful for Universal BodyAddons -->
  <Race>MyAlienRace</Race>

  <!-- Draw only for the specified MutantDef -->
  <!-- speculative feature, actual defNames from Anomaly are currently unknown -->
  <Mutant>Shambler</Mutant>

  <!-- Draw only for the specified CreepJoinerFormKindDef -->
  <!-- speculative feature, actual usage in Anomaly is currently unknown -->
  <CreepJoinerFormKind>???</CreepJoinerFormKind>
  
</conditions>
```

The new conditions system also has logic nodes for defining "and" and "or" relationships:

```xml
<conditions>
  <BodyPart>
    <bodyPartLabel>tail</bodyPartLabel>
  </BodyPart>
  <Or>
    <ApparelDef>Apparel_PowerArmor</ApparelDef>
    <Moving>true</Moving>
  </Or>
</conditions>
```

Extension Graphics also has new syntax, though it should be able to read previous syntax for the time being. Please update at your earliest convenience as backwards compatibility will be dropped in a future update:
```xml
<extendedGraphics>
  <Hediff For="BionicTail">Path/To/Texture</Hediff>
  <Backstory For="AlienMutant">Path/To/Texture</Backstory>
  <Age For="HumanlikeChild">Path/To/Texture</Age>
  <Damage For="0.5">Path/To/Texture</Damage>
  <Gender For="Male">Path/To/Texture</Gender>
  <Trait For="Pyromaniac">Path/To/Texture</Trait>
  <BodyType For="Fat">Path/To/Texture</BodyType>
  <HeadType For="Female_AveragePointy">Path/To/Texture</HeadType>
  <Gene For="Robust">Path/To/Texture</Gene>
  <Race For="MyAlienRace">Path/To/Texture</Race><!-- for universal bodyaddons -->
</extendedGraphics>

<extendedGraphics>
  <BodyType For="Hulk">
    <path>Path/To/Texture</path>
    <extendedGraphics>
      <HeadType For="Male_AverageNormal">Path/To/Texture</HeadType>
    </extendedGraphics>
   </BodyType>
</extendedGraphics>
```

Body addons that are meant to be attached to the head (such as ears and horns) **must** use ```<alignWithHead>true</alignWithHead>``` now in order to be drawn correctly in 1.5. If this is not set, then they will be hidden whenever the body is hidden (such as when a pawn is in bed).

Here is an example of a working addon utilizing the new syntax for both ```conditions``` and ```extensionGraphics```, in this case a Universal BodyAddon from Eccentric Tech - Cosmetic Modifications:

```xml
<!-- left ears -->
<li>
  <name>cosmetic left ear (hair-colored)</name>
  <userCustomizable>false</userCustomizable>
  <path>Addons/Eccentric/Ears/None</path>
  <inFrontOfBody>true</inFrontOfBody>
  <colorChannel>hair</colorChannel>
  <alignWithHead>true</alignWithHead>
  <drawSize>0.96</drawSize>
  <scaleWithPawnDrawsize>true</scaleWithPawnDrawsize>
  <conditions>
    <BodyPart>
      <bodyPart>EccentricCosmetics_SideCrown</bodyPart>
      <bodyPartLabel>left crown</bodyPartLabel>
    </BodyPart>
  </conditions>
  <extendedGraphics>
    <Hediff For="Eccentric_Hediff_Ears_Cat">Addons/Eccentric/Ears/Feline/CatLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_AmericanCurl">Addons/Eccentric/Ears/Feline/AmericanCurlLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_MaineCoon">Addons/Eccentric/Ears/Feline/MaineCoonLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_ScottishFold">Addons/Eccentric/Ears/Feline/ScottishFoldLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Siamese">Addons/Eccentric/Ears/Feline/SiameseLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_FoxGray">Addons/Eccentric/Ears/Canine/FoxLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Fox">Addons/Eccentric/Ears/Canine/RedFoxLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Labrador">Addons/Eccentric/Ears/Canine/LabradorLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Shepherd">Addons/Eccentric/Ears/Canine/ShepherdLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Terrier">Addons/Eccentric/Ears/Canine/TerrierLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Wolf">Addons/Eccentric/Ears/Canine/WolfLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_BlackBear">Addons/Eccentric/Ears/Misc/BlackBearLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_BrownBear">Addons/Eccentric/Ears/Misc/BrownBearLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Mouse">Addons/Eccentric/Ears/Misc/MouseLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Rabbit">Addons/Eccentric/Ears/Misc/RabbitLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_SquirrelGray">Addons/Eccentric/Ears/Misc/SquirrelGrayLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_SquirrelRed">Addons/Eccentric/Ears/Misc/SquirrelRedLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Ears_Horse">Addons/Eccentric/Ears/Misc/HorseLeft</Hediff>
    <Hediff For="Eccentric_Hediff_Horn_GreatHornedOwl">Addons/Eccentric/Horns/Double/GreatHornedOwlLeft</Hediff>
  </extendedGraphics>
  <offsets>
    <south>
      <layerOffset>-0.270</layerOffset>
    </south>
    <north>
      <layerOffset>-0.330</layerOffset>
    </north>
    <east>
      <layerOffset>-0.330</layerOffset>
    </east>
    <west>
      <layerOffset>-0.270</layerOffset>
    </west>
  </offsets>
</li>
```