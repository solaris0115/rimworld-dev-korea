This is a guide to changes to vanilla RimWorld as well as compatibility functions for the Biotech DLC, aimed at modders who are updating their races from 1.3 to 1.4. All information directly relevant to HAR should be represented in their respective wiki pages for new mods for RimWorld 1.4;  if you have any questions, if something doesn't match up, or you've found something we've overlooked, please join us on the [Alien Races Discord](http://discord.gg/XMCRj46)!

The live version of HAR is now updated with all major components for 1.4 and Biotech compatibility and should be used for updating race mods: **[Humanoid Alien Races - Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=839005762)**

The development version of HAR for RimWorld 1.4 can be found here: **[Humanoid Alien Races ~ Dev](https://steamcommunity.com/sharedfiles/filedetails/?id=2640710953)** - Note that since it has a different packageId from the live version of HAR, mods may throw an error about missing dependencies. This is normal and can safely be ignored; loading both at the same time will break your game.

# RimWorld v1.4 Changes

## `BackstoryDef`

BackstoryDefs are now vanilla Def types, and vanilla backstories are now stored as Defs along with all other XML. However, vanilla has a smaller feature set than HAR backstories, so HAR backstories `AlienRace.BackstoryDef` are now `AlienRace.AlienBackstoryDef` entries, which are a subclass of the vanilla BackstoryDef. They are different in the following ways:

* `baseDescription` is now `baseDesc`
* `forcedTraits` is now vanilla and does not allow for a chance factor. HAR's field with the chance field intact is now `forcedTraitsChance`
* `disallowedTraits` is now vanilla and does not allow for a chance factor. HAR's field with the chance field intact is now `disallowedTraitsChance`
* `skillGains` are now a vanilla Dictionary, and thus use `key` and `value` instead of `defName` and `amount`. At the time of this writing, failing to change these keys will result in a massive red error cascade in Dictionary.
* Vanilla BackstoryDefs have a `shuffleable` field. If set to false, it will not be randomly selected and can only be used by `SolidBio` entries. All backer pawn backstories have this set to false.
* Vanilla BackstoryDefs have a `possessions` field. If an item is specified here, then it will be added to starting resources on a new game start if this pawn is used as a starting colonist. Note that during pawn generation, this item will only be used if inventory items are not pre-generated for a pre-existing addiction, baby food need (for babies), or hemogen need (for hemophages); those take higher priority.

Here is an example of a backstory converted for use in 1.4:

```xml
<!-- Sun caste engineer -->
<AlienRace.AlienBackstoryDef>
  <defName>Heruan_Adulthood_Engineer</defName>
  <slot>Adulthood</slot>
  <title>Sun caste engineer</title>
  <titleShort>engineer</titleShort>
  <baseDesc>[PAWN_nameDef] served as a ship engineer for the Expedition.
    [PAWN_pronoun] was adept at the operation and maintenance of ship systems
    as well as the maintenance of tools of the trade.</baseDesc>
  <skillGains>
    <li>
      <key>Construction</key>
      <value>3</value>
    </li>
    <li>
      <key>Crafting</key>
      <value>3</value>
    </li>
    <li>
      <key>Medicine</key>
      <value>-1</value>
    </li>
  </skillGains>
  <forcedTraitsChance>
    <li>
      <defName>Industriousness</defName>
      <degree>1</degree>
      <chance>50</chance>
    </li>
  </forcedTraitsChance>
  <spawnCategories>
    <li>Heruan</li>
    <li>Heruan_Adulthood</li>
    <li>Heruan_SunAdulthood</li>
  </spawnCategories>
  <bodyTypeMale>Male</bodyTypeMale>
  <bodyTypeFemale>Female</bodyTypeFemale>
</AlienRace.AlienBackstoryDef>
```

## Crown Types

Vanilla now has HeadTypeDefs (under `Defs\HeadTypeDefs`) associated with crowntypes, which were previously just a string. These have a gender field and a texture path field; custom crowntypes will now require new HeadTypeDefs. The `<aliencrowntypes>` tag is now the `<headTypes>` tag as well, and the default value for `HumanRace` is now:

```xml
<alienPartGenerator>
  <headTypes>
    <li>Male_AverageNormal</li>
    <li>Male_AverageWide</li>
    <li>Male_AveragePointy</li>
    <li>Male_NarrowNormal</li>
    <li>Male_NarrowPointy</li>
    <li>Male_NarrowWide</li>
    <li>Female_AverageNormal</li>
    <li>Female_AverageWide</li>
    <li>Female_AveragePointy</li>
    <li>Female_NarrowNormal</li>
    <li>Female_NarrowPointy</li>
    <li>Female_NarrowWide</li>
  </headTypes>
</alienPartGenerator>
```

**Note**: Vanilla `HeadTypeDef` defNames and file names do not match. For example, the texture `Male_Average_Normal.png` is used by the `Male_AverageNormal` Def.

If you were using `crownTypes` offsets inside BodyAddons, that field has been renamed to `headTypes` as well. There are three options for updating custom head types to 1.4:

### Using Vanilla HeadTypeDefs (Recommended for new mods)

If you were using vanilla crowntype names with an optional Graphic Paths override, then all you should have to do is change your former `crowntypes` to the new `HeadTypeDef` defNames. This is the simplest way to implement custom heads, and if you only have one or two custom head textures, then changing to this method might be appealing. Remember that even if you have multiple different head textures, you can use variant textures as well.

`alienPartGenerator`:
```xml
<headTypes Inherit="False">
  <li>Male_AverageNormal</li>
  <li>Female_AverageNormal</li>
</headTypes>
```

Textures:
```
Textures/Path/To/Custom/Textures/Male_Average_Normal_east.png
Textures/Path/To/Custom/Textures/Male_Average_Normal_north.png
Textures/Path/To/Custom/Textures/Male_Average_Normal_south.png
Textures/Path/To/Custom/Textures/Female_Average_Normal_east.png
Textures/Path/To/Custom/Textures/Female_Average_Normal_north.png
Textures/Path/To/Custom/Textures/Female_Average_Normal_south.png
```

`graphicPaths`:
```xml
<graphicPaths>
  <head>Path/To/Custom/Textures/</head>
</graphicPaths>
```

### Using [[Extension Graphics|Extension-Graphics]] Overrides

If you were previously using non-vanilla `crowntypes` and do not want to rename your texture files, you can use the new [[Extension Graphics|Extension-Graphics]] system to specify your alternative textures:

`alienPartGenerator`:
```xml
<headTypes Inherit="False">
  <li>Male_AverageNormal</li>
  <li>Female_AverageNormal</li>
</headTypes>
```

Textures:
```
Textures/Path/To/Custom/Textures/Male_Custom_east.png
Textures/Path/To/Custom/Textures/Male_Custom_north.png
Textures/Path/To/Custom/Textures/Male_Custom_south.png
Textures/Path/To/Custom/Textures/Female_Custom_east.png
Textures/Path/To/Custom/Textures/Female_Custom_north.png
Textures/Path/To/Custom/Textures/Female_Custom_south.png
```

`graphicPaths`:
```xml
<graphicPaths>
  <head>
    <path>Path/To/Custom/Textures/</path>
    <headtypeGraphics>
      <Male_AverageNormal>Path/To/Custom/Textures/Male_Custom</Male_AverageNormal>
      <Female_AverageNormal>Path/To/Custom/Textures/Female_Custom</Female_AverageNormal>
    </headtypeGraphics>
  </head>
</graphicPaths>
```

You can also use this system to replicate non-gendered heads:
```xml
<graphicPaths>
  <head>
    <path>Path/To/Custom/Textures/</path>
    <headtypeGraphics>
      <li>
        <headType>Male_AverageNormal</headType>
        <genderGraphics>
          <Male>Path/To/Custom/Textures/Ungendered_Custom</Male>
          <Female>Path/To/Custom/Textures/Ungendered_Custom</Female>
        </genderGraphics>
      </li>
    </headtypeGraphics>
  </head>
</graphicPaths>
```

### Custom HeadTypes

Finally, you can use custom `HeadTypeDef` entries, which can make it easier to make ungendered heads. Note that even if you specify a custom path in these HeadTypeDefs, you still have to use a [[Graphic Paths|Graphic-Paths]] override for it to resolve correctly, since the default value for Graphic Paths will point it back at the vanilla path.

`alienPartGenerator`:
```xml
<headTypes Inherit="False">
  <li>MyRace_Custom</li>
</headTypes>
```

`HeadTypeDef`:
```xml
<HeadTypeDef ParentName="AverageBase">
  <defName>MyRace_Custom</defName>
  <graphicPath>Path/To/Custom/Textures/Ungendered_Custom</graphicPath>
  <gender>None</gender>
</HeadTypeDef>
```

Textures:
```
Textures/Path/To/Custom/Textures/Ungendered_Custom_east.png
Textures/Path/To/Custom/Textures/Ungendered_Custom_north.png
Textures/Path/To/Custom/Textures/Ungendered_Custom_south.png
```

## `FactionDef`

FactionDefs no longer have a `geneticVariance` or `centralMelanin` field. They have been supplanted by the `melaninRange` field.

Note that previously, the default value for `geneticVariance` was 1f and `centralMelanin` was 0.5f, which were clamped to `0~1` in code. This means that amongst other things, `geneticVariance` values above 0.5f actually didn't do anything with the default centralMelanin value. The new `melaninRange` field defaults to `0~1` for humans and gives more direct control over skin color ranges.

## `PawnKindDef`

PawnKindDefs no longer have a `baseRecruitDifficulty` field. On closer inspection, this value was required but not actually used by any live code in 1.3. It can safely be deleted.

## `TraderKindDef`

`StockGenerator_WeaponsRanged`, `StockGenerator_WeaponsMelee`, `StockGenerator_Clothes`, and `StockGenerator_Art` no longer exist, and vanilla usages of these StockGenerators are now using `StockGenerator_MarketValue`. If you have custom traders, please check out the vanilla Defs under `Defs/TraderKindDefs` for examples of the new usage.

You can see a direct diff of `TraderKinds_Caravan_Outlander.xml` [here](https://www.diffchecker.com/CjoXq8Ib).

## `StatDef`

`ToxicSensitivity` no longer exists. It has been replaced by `ToxicResistance` and `ToxicEnvironmentResistance`. The former works exactly as ToxicSensitivity did before except the value is inverted, with humans defaulting to 0f and 1f making a pawn immune to all toxic effects. The latter is only used against certain external effects, such as toxic fallout, rot stink, and tox gas (Biotech) and is generally intended for apparel; the former grants complete resistance to poisons and toxins which includes injected venom.

Note that the two stack multiplicatively: if a pawn has both 0.5 ToxicResistance and 0.5 ToxicEnvironmentResistance, then they will suffer 75% less buildup/damage from environmental effects such as toxic fallout. Having 1f in either value will make them completely immune.

Also note that if you have apparel that is meant to serve in the same capacity as a gas mask, tox gas has a separate Hediff meant to represent the physical irritation caused by eye and lung exposure to the gas. To prevent this hediff, your apparel needs the `immuneToToxGasExposure` tag:

```xml
<ThingDef>
  <apparel>
    <immuneToToxGasExposure>true</immuneToToxGasExposure>
  </apparel>
</ThingDef>
```

## `SoundDef`

`AudioGrain_Folder` has been "fixed" to properly only work when pointed at an entire Folder and will randomly use a sound clip within that folder. It was previously possible to misuse `AudioGrain_Folder` to point to a single clip, but this was unintended and you should use `AudioGrain_Clip` which is intended for this purpose:

```xml
<SoundDef>
  <defName>Interact_Grenade</defName>  
  <context>MapOnly</context>   
  <maxSimultaneous>1</maxSimultaneous>  
  <subSounds>
    <li>
      <grains>
        <li Class="AudioGrain_Clip">
          <clipPath>Weapon/GrenadePin</clipPath>
        </li>
      </grains>      
      <volumeRange>23.91304~23.91304</volumeRange>      
      <pitchRange>0.9576087~1.084783</pitchRange>
    </li>
  </subSounds>
</SoundDef>
```

# HAR Framework Updates

Update: At the time of this writing, xenotype and gene restrictions are now available in the live version of Humanoid Alien Races and are documented under [[Race Restriction|Race-Restriction]].

Additional reproduction and children compatibility features are documented under [[General Settings|General-Settings]].

## `AlienRace.ThingDef_AlienRace`

### General Settings

`<useGenderedHeads>` and `<useGenderedBodies>` no longer exist,
and several new fields have been added to support Biotech reproduction and children.

Please check out [[General Settings|General-Settings]] for more details.

### Body Addons
`<bodyPart>` has been split into `<bodyPart>` which requires a `BodyPartDef` `defName`
and `<bodyPartLabel>` which targets `label` tags.
Both can be used at the same time to target a `BodyPartDef` with a specific `label`.

`<geneRequirement>` has been added for Gene-based BodyAddons.

[[Extension Graphics|Extension-Graphics]] can now be used for Body Addons.

### Graphic Paths

`<graphicPaths>` is no longer a list but a single node. It can also support [[Extension Graphics|Extension-Graphics]] now.

Please see [[Graphic Paths|Graphic-Paths]] for more details.

## Body Types

`alienbodytypes` in `alienPartGenerator` has been renamed to `bodyTypes`.

## Biotech / Children Compatibility

Biotech children and babies do not use downscaled body graphics, but two dedicated BodyTypeDefs. You can add conditional support for them like so:

```xml
<bodyTypes>
  <li>...</li>
  <li MayRequire="Ludeon.RimWorld.Biotech">Baby</li>
  <li MayRequire="Ludeon.RimWorld.Biotech">Child</li>
</bodyTypes>
```

Human `LifeStageDef` entries have changed. There is no longer a `HumanlikeToddler` Def, and there is now a Biotech-exclusive `HumanlikePreTeenager` Def. If you use custom LifeStages, you should check out these changes. `LifeStageDef` now also has a `workerClass` field contingent on Biotech being loaded that controls various aspects of the pawn on generation and when lifestages change:

```xml
  <LifeStageDef ParentName="HumanlikeAdolescent">
    <defName>HumanlikeTeenager</defName>
    <label>teenager</label>
    <workerClass MayRequire="Ludeon.RimWorld.Biotech">LifeStageWorker_HumanlikeAdult</workerClass>
    <!-- ... -->
  </LifeStageDef>
```

Race age generation curves need to be adjusted to allow for babies and children. This can be done conditionally, the new human ageGenerationCurve looks like this:

```xml
<ageGenerationCurve>
  <points>
    <li MayRequire="Ludeon.RimWorld.Biotech">(0,0)</li>
    <li MayRequire="Ludeon.RimWorld.Biotech">(0.001,43)</li>
    <li MayRequire="Ludeon.RimWorld.Biotech">(8,86)</li>
    <li MayRequire="Ludeon.RimWorld.Biotech">(12.5,118)</li>  <!-- Exclude 12.5-13 years to avoid spawning pawns who are very close to becoming adults -->  
    <li MayRequire="Ludeon.RimWorld.Biotech">(12.51,0)</li>  
    <li MayRequire="Ludeon.RimWorld.Biotech">(13,0)</li>      
    <li MayRequire="Ludeon.RimWorld.Biotech">(13.001,122)</li><!-- End exclude -->
    <li MayRequire="Ludeon.RimWorld.Biotech">(13.999,130)</li>
    <li>(14,0)</li>
    <li MayRequire="Ludeon.RimWorld.Biotech">(14.001,130)</li>
    <li>(16,100)</li>
    <li>(50,100)</li>
    <li>(60,30)</li>
    <li>(70,18)</li>
    <li>(80,10)</li>
    <li>(90,3)</li>
    <li>(100,0)</li>
  </points>
</ageGenerationCurve>
```

Finally, the gestation period for humans was changed from <code>30</code> in 1.3 and prior to <code>18</code> in 1.4. If you previous balanced your race's gestation period around the human value, you should update this value or it will result in unusually long pregnancies.

```xml
<AlienRace.ThingDef_AlienRace>
  <race>
    <gestationPeriodDays>18</gestationPeriodDays>
  </race>
</AlienRace.ThingDef_AlienRace>
```

**Additional Settings** (Now available on Live):

Additional settings can be found in [[General Settings|General-Settings]] and [[Race Restriction|Race-Restriction]] for reproduction and children compatibility.

## Xenotypes and GeneDefs

**Now available in Live:**
Fields for restricting `GeneDef` usages have been added to [[Race Restrictions|Race-Restriction]].
Please see the Race Restriction page for more details.

A Gene requirement option has been added to [[Body Addons|Body-Addons]]
and alternate graphics for Genes have also been added to [[Extension Graphics|Extension-Graphics]].
