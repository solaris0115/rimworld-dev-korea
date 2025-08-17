All of the settings specified in this page go inside the `<generalSettings>` tag of your race Def's `<alienRace>` properties.

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <!-- General settings go here. -->
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Unless explicitly specified, **all settings are OPTIONAL**. It is strongly recommended that you omit any setting you do not actually need, especially if you are inheriting your race Def from `HumanRace`.

## Basic Settings
Some basic settings for your race will be set here.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>

<tr><td>

```xml
<maleGenderProbability>0.3</maleGenderProbability>
```
</td><td>
<code>0.5</code>
</td><td>
Sets the gender balance of your race. (For example, a <code>maleGenderProbability</code> of 0.3 means that 30% of your randomly generated race members will be male and 70% will be female.)
</td></tr>
<tr><td>

```xml
<growthAges>
  <li>7</li>
  <li>10</li>
  <li>13</li>
</growthAges>
```
</td><td>
<code>7, 10, 13</code>
</td><td>
Ages when a child will experience a growth moment.<br/>
The lifeStageWorkSettings ages need to match one of these ages, or growth will be reset at these ages too.
</td></tr>
<tr><td>

```xml
<forcedRaceTraitEntries>
  <!-- 25% chance to apply Sanguine to males, 10% chance to apply to females -->
  <li>
    <defName Degree="2">NaturalMood</defName>
    <chance>50</chance>
    <commonalityMale>50</commonalityMale>
    <commonalityFemale>20</commonalityFemale>
  </li>
  <!-- 50% chance to apply Hard Worker or Industrious -->
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
  <!-- flat 50% chance to apply Beautiful -->
  <li>
    <defName Degree="2">Beauty</defName>
    <chance>50</chance>
  </li>
  <!-- flat 50% chance to apply Gay (not a spectrum trait) -->
  <li>
    <defName>Gay</defName>
    <chance>50</chance>
  </li>
  <!-- always apply Psychopath -->
  <li>
    <defName>Psychopath</defName>
  </li>
</forcedRaceTraitEntries>
```
</td><td>
(None)
</td><td>
<strong>RimWorld 1.5+</strong>:<br/><br/>
Adds forced traits to your race, optionally with a specified chance and/or gender commonality. Note that gender commonality acts as a "second roll" during generation; if you have <code>chance</code> set to 50 and <code>maleCommonality</code> set to 50, then there will be a 25% chance that male members of your race get the specified trait.<br/><br/>
Forced traits do not count towards the regular trait limit for your race.<br/><br/>
Multiple entries belonging to the same spectrum trait will be rolled sequentially, with later entries being ignored if an earlier roll succeeds.
</td></tr>
<tr><td>

```xml
<forcedRaceTraitEntries>
  <li>
    <defName>NaturalMood</defName>
    <degree>2</degree>
    <chance>50</chance>
    <commonalityMale>50</commonalityMale>
    <commonalityFemale>20</commonalityFemale>
  </li>
  <li>
    <defName>Nerves</defName>
    <degree>2</degree>
    <chance>50</chance>
    <commonalityMale>50</commonalityMale>
  </li>
  <li>
    <defName>Beauty</defName>
    <degree>2</degree>
    <chance>50</chance>
  </li>
  <li>
    <defName>Gay</defName>
    <chance>50</chance>
  </li>
  <li>
    <defName>Psychopath</defName>
  </li>
</forcedRaceTraitEntries>
```
</td><td>
(None)
</td><td>
<strong>RimWorld 1.4 and earlier</strong>:<br/><br/>
HAR for RimWorld 1.4 and earlier have a more explicit notation for trait degrees and do not support count-selection.
</td></tr>
<tr><td>

```xml
<disallowedTraits>
  <!-- 50% chance to disallow Staggeringly Ugly -->
  <li>
    <defName Degree="-2">Beauty</defName>
    <chance>50</chance>
  </li>
  <!-- disallow Pyromaniac -->
  <li>
    <defName>Pyromaniac</defName>
  </li>
</disallowedTraits>
```
</td><td>
(None)
</td><td>
Disallows traits from generating on your race. Uses the same syntax as <code>forcedRaceTraitEntries</code>.<br/><br/>By default, completely disallows the specified trait; if a <code>chance</code> is specified, then it will effectively reduce the commonality of that trait for your race. For example, if you specify a <code>chance</code> of 10 for a trait, then it will only generate 1/10th as often as it would on humans.
</td></tr>
<tr><td>

```xml
<traitCount>2~3</traitCount>
<additionalTraits>1~5</additionalTraits>
```
</td><td>
<code>2~3</code><br/><code>0</code>
</td><td>
Changes the number of traits that members of your race will generate with.<br/><br/>Note that <code>additionalTraits</code> is effectively redundant as the two ranges are simply added together to determine the number of traits your race generates with.
</td></tr>
<tr><td>

```xml
<immuneToAge>true</immuneToAge>
```
</td><td>
<code>false</code>
</td><td>
Disables age-related ailments from affecting your race, such as Bad Back, Frail, and Dementia. Specifically, this disables HediffGiver_Birthday subclasses from running against your race.
</td></tr>
<tr><td>

```xml
<chemicalSettings>
  <li>
    <chemical>Smokeleaf</chemical>
    <reactions>
      <li Class="IngestionOutcomeDoer_GiveHediff">
        <hediffDef>LungFailure</hediffDef>
        <severity>0.75</severity>
      </li>
    </reactions>
  </li>
  <li>
    <chemical>Luciferium</chemical>
    <ingestible>false</ingestible>
  </li>
</chemicalSettings>
```
</td><td>
(None)
</td><td>
Lets you alter the way your race members react to certain drugs by adding <code>IngestionOutcomeDoer</code> nodes or disable certain drugs from being taken by your race at all. Note that <code><chemical</code> refers to ChemicalDef defNames such as <code>Psychite</code> or <code>Alcohol</code> and not ingestible ThingDefs such as <code>Yayo</code> or <code>Beer</code>.
</td></tr>
<tr><td>

```xml
<validBeds>
  <li>AlienRaceDefName</li>
</validBeds>
```
</td><td>
(None)
</td><td>
If set, makes it so that members of your race can only sleep on the specified beds. By default (or if left empty), your race members can sleep on any bed that is also valid for humans.
</td></tr>
<tr><td>

```xml
<maxDamageForSocialfight>6</maxDamageForSocialfight>
```
</td><td>
<code>INTMAX</code>
</td><td>
Allows you to limit the amount of melee damage a member of your race can inflict with a single attack in a social fight. Useful for races with powerful unarmed attacks, as ones significantly more powerful than human attacks might inflict serious damage in a social fight.
</td></tr>
<tr><td>

```xml
<allowHumanBios>true</allowHumanBios>
```
</td><td>
<code>false</code>
</td><td>
Allows you to enable human <code>PawnBio</code> entries to be used for your race. These are the "preset" or "backer" pawns that are included in the vanilla game that represent specific characters created by Ludeon staff and early backers. May not work well if your race uses all custom backstories.
</td></tr>
<tr><td>

```xml
<immuneToXenophobia>true</immuneToXenophobia>
```
</td><td>
<code>false</code>
</td><td>
If set to <code>true</code>, then humans will not have xenophobic or xenophilic thoughts towards members of your race (from the Xenophobia and Xenophilia traits, respectively).
</td></tr>
<tr><td>

```xml
<notXenophobistTowards>
  <li>OtherAlien</li>
  <li>AnotherAlien</li>
</notXenophobistTowards>
```
</td><td>
(None)
</td><td>
Allows you to specify races that your race will not consider a different race for Xenophobia or Xenophilia.<br/><br/>Generally used to designate genetically similar subraces.
</td></tr>
<tr><td>

```xml
<minAgeForAdulthood>315</minAgeForAdulthood>
```
</td><td>
<code>20</code>
</td><td>
Sets the minimum age for members of your race to be eligible for an adulthood backstory.
</td></tr>
<tr><td>

```xml
<humanRecipeImport>true</humanRecipeImport>
```
</td><td>
<code>false</code>
</td><td>
If set to <code>true</code>, copies all human surgery recipes to your race.<br/><br/>Note that if you inherited your race Def from HumanRace, then your race will already inherit the recipes specifically listed in the <code>Human</code> ThingDef unless you specifically set <code>Inherit="False"</code> on your race's <code>recipe</code> list; enabling this setting will also copy indirectly added recipes such as those for adding bionics and implants.
</td></tr>
<tr><td>


```xml
<ageSkillFactorCurve>
  <points>
    <li>(3, 0.2)</li>
    <li>(18, 1)</li>
    <li>(35, 1)</li>
    <li>(60, 1.6)</li>
  </points>
</ageSkillFactorCurve>
```
</td><td>
As shown
</td><td>
The factor curve for skills on pawn generation by age.
</td></tr>
<tr><td>

```xml
<lovinIntervalHoursFromAge>
  <points>
    <li>(16, 1.5)</li>
    <li>(22, 1.5)</li>
    <li>(30, 4)</li>
    <li>(50, 12)</li>
    <li>(75, 36)</li>
  </points>
</lovinIntervalHoursFromAge>
```
</td><td>
As Shown
</td><td>
<strong>RimWorld 1.4 Only</strong>:<br/><br/>
Allows you to customize the value curve for how often members of your race will engage in romantic interactions, where the left side value is the age in years and the right side is the mean time between interactions in hours. For example, using the default human curve as shown, a pawn with an age of 26 will have a midpoint value between 1.5 and 4.0 of approximately 3.25.
</td></tr>
<tr><td>

```xml
<canLayDown>false</canLayDown>
```
</td><td>
<code>true</code>
</td><td>
Determines whether your race sleeps on beds at all. If set to <code>false</code>, then your race members will sleep upright instead.
</td></tr>
<tr><td>

```xml
<factionRelations>
  <li>
    <factions>
      <li>FactionExample</li>
    </factions>
    <goodwill>
      <min>-100</min>
      <max>100</max>
    </goodwill>
  </li>
</factionRelations>
```
</td><td>
(None)
</td><td>
Allows you to set a custom starting goodwill for a faction using a member of your race as a <code>basemember</code>. The default behavior for factions without <code>permanentEnemy</code> or <code>naturalEnemy</code> set will be set to a random starting goodwill.
</td></tr>
<tr><td>

```xml
<corpseCategory>CategoryDef</corpseCategory>
```
</td><td>
<code>alienCorpseCategory</code>
</td><td>
Sets the <code>ThingCategoryDef</code> that corpses of your race should be stored under. Defaults to the HAR-added <code>alienCorpseCategory</code>.
</td></tr>
</tbody>
</table>

### Abilities

<strong>RimWorld 1.4+ only</strong> - You can add vanilla-compatible <code>AbilityDef</code> entries to your race by using the following syntax:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <abilities>
    
        <!-- always added -->
        <li>FireSpew</li>
    
        <!-- 50% chance of being added to any given pawn -->
        <li>
          <defName>FoamSpray</defName>
          <chance>50</chance>
        </li>
    
        <!-- randomly select 2 distinct options -->
        <li>
          <options>
            <li>AcidSpray</li>
            <li>FireBurst</li>
            <li>AnimalWarcall</li>
          </options>
          <count>2</count>
        </li>
    
        <!-- always added for male pawns -->
        <li>
          <defName>MyRace_CustomMaleAbility</defName>
          <commonalityFemale>0</commonalityFemale>
        </li>
    
        <!-- 75% chance of adding both for female pawns -->
        <li>
          <options>
            <li>MyRace_CustomFemaleAbilityA</li>
            <li>MyRace_CustomFemaleAbilityB</li>
          </options>
          <commonalityFemale>75</commonalityFemale>
          <commonalityMale>0</commonalityMale>
        </li>
    
      </abilities>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Similar to Extension Graphics, entries can also be nested for complex logic:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <abilities>
  
        <li>
          <!-- always added -->
          <defName>FoamSpray</defName>
          <chance>100</chance>
          <options>
            <li>
              <!-- 50% chance that two of the following are added -->
              <chance>50</chance>
              <options>
                <li>AcidSpray</li>
                <li>FireBurst</li>
                <li>AnimalWarcall</li>
              </options>
              <count>2</count>
            </li>
            <!-- always added -->
            <li>FireSpew</li>
          </options>
          <count>2</count>
        </li>
  
      </abilities>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

## Alien Part Generator
These settings let you customize various graphical aspects of your race.

All tags in this section go into the <code>alienPartGenerator</code> tag, which itself is inside the <code>generalSettings</code> tag.

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <alienPartGenerator>
        <!-- Alien part generator settings go here -->
      </alienPartGenerator>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

### Color Channels

Sets the color color channels for your race. Color values for each channel are chosen upon pawn generation, so they will be consistent for that pawn throughout its existence.

**NOTE**: As of RimWorld v1.4, skin and hair color genes take precedence over color channels. As such, if you want to use color channels for skin and hair, you need to disable those genes for your race. See [[Race Restrictions|Race-Restriction]] for more details.

```xml
<colorChannels>
  <li>
    <name>skin</name>
    <first Class="AlienRace.ColorGenerator_SkinColorMelanin">
      <minMelanin>0</minMelanin>
      <maxMelanin>1</maxMelanin>
    </first>
    <second Class="AlienRace.ColorGenerator_CustomAlienChannel">
      <colorChannel>skin_1</colorChannel>
    </second>
  </li>
  <li>
    <name>hair</name>
    <first Class="ColorGenerator_Options">
      <options>
        <li>
          <weight>10</weight>
          <only>RGBA(0.000, 1.000, 0.000, 1.000)</only>
        </li>
        <li>
          <weight>10</weight>
          <only>RGBA(0, 128, 255, 255)</only>
        </li>
        <li>
          <weight>10</weight>
          <only>RGBA(0.000, 0.000, 1.000, 1.000)</only>
        </li>
      </options>
    </first>
    <second Class="ColorGenerator_Single">
      <color>RGBA(128, 255, 0, 255)</color>
    </second>
  </li>
</colorChannels>
```

The <code>second</code> part of each channel is not used by default, but is still required. Setting it to white is recommended if you don't intend to use it.

By default, the four color channels are automatically created for vanilla compatibility:

<table>
<thead>
<tr><th align="left">Channel</th><th align="left">Value</th></tr>
</thead>
<tbody>
<tr><td>
<code>base</code>
</td><td>
No color application (white)
</td></tr>
<tr><td>
<code>skin</code>
</td><td>
Skin color (melanin-based)
</td></tr>
<tr><td>
<code>hair</code>
</td><td>
Hair color (vanilla palette)
</td></tr>
<tr><td>
<code>tattoo</code>
</td><td>
Tattoo color (vanilla palette)
</td></tr>
<tr><td>
<code>favorite</code>
</td><td>
<strong>RimWorld v1.4 and later:</strong><br/>
Favorite color (vanilla palette)<br/>
The second channel contains the original color if the favorite color is changed by mods.
</td></tr>
<tr><td>
<code>ideo</code>
</td><td>
<strong>RimWorld v1.5 and later:</strong><br/>
Ideoligion colors<br/>
The second channel contains the ideoligion apparel color.
</td></tr>
<tr><td>
<code>mech</code>
</td><td>
<strong>RimWorld v1.5 and later:</strong><br/>
Faction Mech colors<br/>
</td></tr>
</tbody>
</table>

Adding a list entry using one of the above names will override it. Note that if you inherited your race from <code>HumanRace</code>, it will inherit a list entry for <code>skin</code> already; if you want to specify your own, then you should add <code>Inherit="False"</code> to the <code>colorChannels</code> tag.

### Custom ColorGenerators

If using any of the default ColorGenerators, the framework will use either all specific <code>options</code> or a limited number of range samples between <minValue> and <maxValue> to populate Ideology's styling station as color options. If you want to add additional options, you can create a custom ColorGenerator in C# using the following interface:

```cs
public interface IAlienChannelColorGenerator
{
  public List<Color> AvailableColors(Pawn pawn);

  public List<ColorGenerator> AvailableGenerators(Pawn pawn);
}
```

You can see an example of the interface in use [here](https://github.com/solaris0115/rimworld-dev-korea/blob/Dev/Source/AlienRace/AlienRace/ColorGenerators.cs#L41-L68).

### Additional Settings

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<borderScale>2.0</borderScale>
```
</td><td>
<code>1.0</code>
</td><td>
<strong>RimWorld v1.3 and later</strong><br/><br/>
Sets the physical dimensions of the pawn atlas (render cache) for your race. Increasing this is only necessary if you have very large drawSizes or BodyAddons that get clipped off.<br/><br/>
Note that if you are using HD Pawn Rendering, Vanilla Expanded Framework, or similar mods to disable the pawn render cache, then this setting will have no effect (but also won't be necessary).
</td></tr>
<tr><td>

```xml
<atlasScale>2</atlasScale>
```
</td><td>
<code>1</code>
</td><td>
<strong>RimWorld v1.3 and later</strong><br/><br/>
Sets the resolution scale of the pawn atlas (render cache). Increasing this value will reduce the blurriness of pawns, especially when you are using mods such as Camera+ to zoom in further than vanilla would normally allow. However, this will also result in an exponential increase in the amount of memory taken up by your pawns.<br/><br/>
Note that if you are using HD Pawn Rendering, Vanilla Expanded Framework, or similar mods to disable the pawn render cache, then this setting will have no effect (but also won't be necessary).
</td></tr>
<tr><td>

```xml
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
```
</td><td>
(See Desc.)
</td><td>
<strong>RimWorld v1.4 and later</strong><br/><br/>
<code>headTypes</code> determines the HeadTypeDefs that are allowed for your race.<br/><br/>
If you inherit your race from <code>BasePawn</code>, then you must provide this list or your race will spawn without heads. If you inherit from <code>HumanRace</code>, your race will inherit the default values shown; if you do not want all of these values, then you can set the <code>Inherit</code> attribute to <code>false</code>:

```xml
<headTypes Inherit="False">
  <li>MyCustomHeadTypeDef</li>
</headTypes>
```
</td></tr>
<tr><td>

```xml
<aliencrowntypes>
  <li>Average_Normal</li>
  <li>Average_Wide</li>
  <li>Average_Pointy</li>
  <li>Narrow_Normal</li>
  <li>Narrow_Pointy</li>
  <li>Narrow_Wide</li>
</aliencrowntypes>
```
</td><td>
(See Desc.)
</td><td>
<strong>RimWorld v1.3 and earlier only</strong> - this has been replaced by <code>headTypes</code> after 1.4<br/><br/>
Crown types are the head shapes that are used by your race. You can use any of the six vanilla head shapes or define your own custom types. Crown types are arbitrary strings, not references to any Def. However, if a texture matching the specified type is not found, it will cause errors and crash the pawn renderer.<br/><br/>
If you inherit your race from <code>BasePawn</code>, then <code>aliencrowntypes</code> will default to <code>Average_Normal</code> only. If you inherit from <code>HumanRace</code>, your race will inherit the six vanilla crown types; if you do not want all of these values, then you can set the <code>Inherit</code> attribute to <code>false</code>:

```xml
<aliencrowntypes Inherit="False">
  <li>MyCustomCrownType</li>
</aliencrowntypes>
```
</td></tr>
<tr><td>

```xml
<alienbodytypes>
  <li>Male</li>
  <li>Female</li>
  <li>Thin</li>
  <li>Hulk</li>
  <li>Fat</li>
</alienbodytypes>
```
</td><td>
(As Shown)
</td><td>
<strong>RimWorld v1.3 and earlier only</strong> - this has been renamed <code>bodyTypes</code> after 1.4<br/><br/>
Specifies the body shapes that can be used by your race. These values are the <code>defName</code>s of <code>BodyTypeDef</code>s. Vanilla body types can be seen in <code>Core/Defs/Misc/BodyTypeDefs</code>.<br/><br/>
You can create custom body shapes by defining your own <code>BodyTypeDef</code>s and listing them here.<br/><br/>
As with crown types, if you inherited your race from <code>HumanRace</code>, then you will also inherit all five vanilla body types (as well as any modded body types that are patched into humans). In order to prevent this, you need to use <code>Inherit="False"</code> (see above).
</td></tr>
<tr><td>

```xml
<useGenderedHeads>false</useGenderedHeads>
```
</td><td>
<code>true</code>
</td><td>
<strong>RimWorld 1.3 and earlier only</strong> - This has been removed in 1.4. To use non-gendered heads, you can either use [[Extension Graphics|Extension-Graphics]] to override gendered textures or create custom <code>HeadTypeDef</code>s with no gender lock.<br/><br/>

If set to <code>false</code>, uses the same textures for male and female pawn heads. Vanilla humans use gendered heads; if you disable this, then you will need to provide custom head textures as all vanilla head textures are gendered.
</td></tr>
<tr><td>

```xml
<useGenderedBodies>true</useGenderedBodies>
```
</td><td>
<code>false</code>
</td><td>
<strong>RimWorld 1.3 and earlier only</strong> - This has been removed in 1.4. To use gendered bodies, you can use [[Extension Graphics|Extension-Graphics]] to specify gendered textures.<br/><br/>

If set to <code>true</code>, will use male and female texture variants for the pawn body. Vanilla humans do not use gendered bodies; if you enable this, then you will need to provide custom body textures as all vanilla body textures are non-gendered.
</td></tr>
<tr><td>

```xml
<customDrawSize>(1.5, 1.5)</customDrawSize>
<customHeadDrawSize>
(1.25, 1.25)
</customHeadDrawSize>
<customPortraitDrawSize>
(0.8, 0.8)
</customPortraitDrawSize>
<customPortraitHeadDrawSize>
(0.7, 0.7)
</customPortraitHeadDrawSize>
```
</td><td>
<code>(1.0, 1.0)</code>
</td><td>
Allow you to scale the size of your race's pawn heads and bodies smaller or larger. Headwear and apparel will always match the drawSize of the head and body, respectively.<br/><br/>
Note that changing the drawSize of heads or bodies may cause rendering misalignment due to the fact that the scale is done with the center of the texture as the anchor point. See <code>headOffset</code> below.
</td></tr>
<tr><td>

```xml
<customFemaleDrawSize />
<customFemaleHeadDrawSize />
<customFemalePortraitDrawSize />
<customFemalePortraitHeadDrawSize />
```
</td><td>
<code>(1.0, 1.0)</code>
</td><td>
<strong>Rimworld v1.4 and later only</strong><br/><br/>
Same as the above values, but specifically for female pawns of your race.
</td></tr>
<tr><td>

```xml
<headOffset>(0.25, 0.15)</headOffset>
```
</td><td>
<code>(0.0, 0.0)</code>
</td><td>
Changes the draw position of the head relative to the body, usually used to correct alignment issues caused by changing head or body drawSize.
</td></tr>
<tr><td>

```xml
<headFemaleOffset>(0.15, 0.25)</headFemaleOffset>
```
</td><td>
<code>(0.0, 0.0)</code>
</td><td>
<strong>Rimworld v1.4 and later only</strong><br/><br/>
Changes the draw position of the head for female pawns.
</td></tr>
<tr><td>

```xml
<headOffsetDirectional>
  <north>
    <layerOffset>0.1</layerOffset>
    <offset>(0.0, 0.1)</offset>
    <bodyTypes>
      <Hulk>(0.0, 0.3)</Hulk>
      <Fat>(0.0, -0.1)</Hulk>
    </bodyTypes>
    <portraitBodyTypes>
      <Hulk>(0.0, 0.3)</Hulk>
      <Fat>(0.0, -0.1)</Hulk>
    </portraitBodyTypes>
    <headTypes>
      <Male_AverageNormal>(0.0, -0.1)</Male_AverageNormal>
      <Female_AverageNormal>(0.0, 0.2)</Female_AverageNormal>
    </headTypes>
    <portraitHeadTypes>
      <Male_AverageNormal>(0.0, -0.1)</Male_AverageNormal>
      <Female_AverageNormal>(0.0, 0.2)</Female_AverageNormal>
    </portraitHeadTypes>
  </north>
  <south>
    <!-- same options as above -->
  </south>
  <east>
    <!-- same options as above -->
  </east>
  <west>
    <!-- same options as above -->
  </west>
</headOffsetDirectional>
```
</td><td>
(None)
</td><td>
<strong>RimWorld 1.5+</strong> - This tag was named headOffsetSpecific in 1.4, it must be renamed in 1.4<br/><br/>
Changes the draw position of the head relative to the body.
These offsets are added to the base <code>headOffset</code> when determining the final
render offset.<br/><br/>
All tags are optional and omitted values will default to <code>0.0, 0.0</code>.
If values for <code>&lt;west&gt;</code> are not provided, they will automatically
be copied from <code>&lt;east&gt;</code>.
</td></tr>
<tr><td>

```xml
<headOffsetDirectional>
  <north>(0.0, 0.1)</north>
  <south>(0.0, 0.1)</south>
  <east>(-0.1, 0.1)</east>
  <west>(0.1, 0.1)</west>
</headOffsetDirectional>
```
</td><td>
<code>(0.0, 0.0)</code>
</td><td>
<strong>RimWorld 1.4 and earlier</strong><br/><br/>
Changes the relative position of the head relative to the body, adjusting each direction individually. Omitting a direction will cause it to default to <code>0.0, 0.0</code>.
</td></tr>
<tr><td>

```xml
<headFemaleOffsetDirectional>
  <!-- see example above -->
</headFemaleOffsetDirectional>
```
</td><td>
(None)
</td><td>
<strong>Rimworld v1.5+</strong> - This tag was named <code>headFemaleOffsetSpecific</code> in RimWorld 1.4<br/><br/>
Changes the draw position of the head for female pawns. Works identically to
<code>&lt;headOffsetSpecific&gt;</code>.
</td></tr>
<tr><td>

```xml
<headBodyPartDef>AlienHead</headBodyPartDef>
```
</td><td>
<code>Head</code>
</td><td>
Determines the <code>BodyPartDef</code> that should be used to determine whether your race's pawns have been visually decapitated.
</td></tr>
<tr><td>

```xml
<getsGreyAt>50</getsGreyAt>
```
</td><td>
<code>40</code>
</td><td>
<strong>RimWorld 1.3 and earlier</strong> - Please use the <code>oldHair</code> options below for
RimWorld v1.4 and later.<br /><br />
Determines the age at which members of your race have their hair turn gray.
</td></tr>
<tr><td>

```xml
<oldHairAgeRange>65.0~85.0</oldHairAgeRange>
```
</td><td>
(None)
</td><td>
<strong>RimWorld v1.4 and later</strong><br /><br />
Sets an age range in which members of your race will have their hair turn color due to age.
Ages within the range will have an increasing chance of turning color;
at or above the maximum value, hair will always turn color.<br /><br />
Overrides <code>getGreyAt</code> if both are set.
</td></tr>
<tr><td>

```xml
<oldHairAgeCurve>
  <points>
    <li>(0, 0)</li>
    <li>(65, 0)</li>
    <li>(75, 0.7)</li>
    <li>(85, 1)</li>
  </points>
</oldHairAgeCurve>
```
</td><td>
(None)
</td><td>
<strong>RimWorld v1.4 and later</strong><br /><br />
Sets a <code>SimpleCurve</code> for determining the age at which members of your race will have
their hair turn color due to age. Overrides both <code>getGreyAt</code> and <code>oldHairAgeRange</code>.
</td></tr>
<tr><td>

```xml
<oldHairColorGen Class="ColorGenerator_Options">
  <options>
    <li>
      <min>(0.65,0.65,0.65)</min>
      <max>(0.85,0.85,0.85)</max>
    </li>
  </options>
</oldHairColorGen>
```
</td><td>
(As Shown)
</td><td>
<strong>RimWorld v1.4 and later</strong><br /><br />
Sets a <code>ColorGenerator</code> that should be used to set the hair color of members of your race when
the above options determine that their hair color should change due to old age.<br /><br />
The shown grey values are used as the human default.
</td></tr>
<tr><td>

```xml
<offsetDefaults>
  <li>
    <name>NewOffset</name>
    <offsets>
      <!-- offsets here -->
    </offsets>
  </li>
</offsetDefaults>
```
</td><td>
(None)
</td><td>
Sets a common, named set of [[BodyAddon|Body-Addons]] offsets that can be used by multiple BodyAddons. Please see the BodyAddons page for more details about options and syntax.
</td></tr>
<tr><td>

```xml
<anchorReplacements>
  <li>
    <originalTag>LeftEye</originalTag>
    <originalGroup>Torso</originalGroup>
    <replacement>
      <rotation>West</rotation>
      <tag>LeftEye</tag>
      <canMirror>false</canMirror>
      <crownType>Narrow</crownType>
      <offset>(-0.12, 0, 0.26)</offset>
      <range>0</range>
      <layer>Head</layer>
      <debugColor>(0,0,0,1)</debugColor>
    </replacement>
    <offsets>
      <!-- Same offset syntax as body addons -->
    </offsets>
  </li>
</anchorReplacements>
```
</td><td>
(None)
</td><td>
Allows race-specific replacements of wound anchors. Offsets use [[BodyAddon|Body-Addons]] options and syntax.
</td></tr>
</tbody>
</table>

### BodyAddons

*(For more information, see the [[BodyAddons|Body-Addons]] page.)*

BodyAddons are used to render additional visible body parts on members of your race, such as distinctive ears, tails, horns, or other distinguishing features. This feature is an extension of the tail drawer in early versions of this framework.

BodyAddons are listed in the <code>bodyAddons</code> tag inside of <code>alienPartGenerator</code>.

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <alienPartGenerator>
        <bodyAddons>
          <!-- Body addons are listed here -->
        </bodyAddons>
      </alienPartGenerator>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

## Reproduction & Children (Biotech DLC Only)

The following settings are used for Biotech compatibility and only apply if the Biotech DLC is active.

### Gene Settings

The following settings are listed directly in the <code>generalSettings</code> tag:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <!-- Gene settings are listed here -->
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Unless otherwise specified, all of the following settings are optional.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<raceGenes>
  <li>
    <defName>Hair_LightTeal</defName>
    <commonalityFemale>0</commonalityFemale>
  </li>
  <li>
    <defName>Hair_Pink</defName>
    <commonalityMale>0</commonalityMale>
  </li>
  <li>
    <defName>WoundHealing_Fast</defName>
    <chance>100</chance>
  </li>
  <li>
    <defName>ViolenceDisabled</defName>
    <chance>50</chance>
  </li>
</raceGenes>
```
</td><td>
Sets genes that your race should have regardless of their xenotype.<br/><br/>
These are applied even on Baseliners.
</td></tr>
<tr><td>

```xml
<growthFactorByAge>
  <points>
    <li>(0,1)</li>
    <li>(6,1)</li>
    <li>(7,0.75)</li>
    <li>(13,0.75)</li>
  </points>
</growthFactorByAge>
```
</td><td>
Sets the rate at which your race's children accumulates growth points by age. The curve shown approximates the human defaults.
</td></tr>
</tbody>
</table>

### Children Settings

The following settings are listed directly in the <code>generalSettings</code> tag:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <!-- Reproduction settings are listed here -->
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Unless otherwise specified, all of the following settings are optional.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<growthAges>
  <li>7</li>
  <li>10</li>
  <li>13</li>
</growthAges>
```
</td><td>
Sets the ages at which children of your race will have growth moments.<br/><br/>
The human default is as shown.
</td></tr>
<tr><td>

```xml
<newbornBackstoryFilter>
  <li>
    <categories>
      <li>CommonAlienCategory</li>
    </categories>
    <commonality>0.75</commonality>
  </li>
  <li>
    <categories>
      <li>UncommonAlienCategory</li>
    </categories>
    <commonality>0.25</commonality>
  </li>
</newbornBackstoryFilter>
```
</td><td>
Overrides the backstory filter used for newborn babies of your race.
</td></tr>
<tr><td>

```xml
<childBackstoryFilter>
  <li>
    <categories>
      <li>CommonAlienCategory</li>
    </categories>
    <commonality>0.75</commonality>
  </li>
  <li>
    <categories>
      <li>UncommonAlienCategory</li>
    </categories>
    <commonality>0.25</commonality>
  </li>
</childBackstoryFilter>
```
</td><td>
Overrides the backstory filter used when a Baby of your race grows into a Child.<br/><br/>
Only applies if you are using the vanilla <code>LifeStageWorker_HumanlikeChild</code> used by <code>HumanlikeChild</code>.
</td></tr>
<tr><td>

```xml
<adultBackstoryFilter>
  <li>
    <categories>
      <li>CommonAlienCategory</li>
    </categories>
    <commonality>0.75</commonality>
  </li>
  <li>
    <categories>
      <li>UncommonAlienCategory</li>
    </categories>
    <commonality>0.25</commonality>
  </li>
</adultBackstoryFilter>
```
</td><td>
Overrides the backstory filter used when a Child of your race grows into a Teenager.<br/><br/>
Only applies if you are using the vanilla <code>LifeStageWorker_HumanlikeAdult</code> used by <code>HumanlikeTeenager</code>.
</td></tr>
<tr><td>

```xml
<adultVatBackstoryFilter>
  <li>
    <categories>
      <li>CommonAlienCategory</li>
    </categories>
    <commonality>0.75</commonality>
  </li>
  <li>
    <categories>
      <li>UncommonAlienCategory</li>
    </categories>
    <commonality>0.25</commonality>
  </li>
</adultVatBackstoryFilter>
```
</td><td>
Overrides the backstory filter used when a member of your race is produced from a Growth Vat.
</td></tr>
</tbody>
</table>

### StatPart_Age Overrides

You can override age curves used in StatPart_Age nodes used in StatDefs via the <code>ageStatoverrides</code> node, which goes directly inside <code>generalSettings</code> as follows:

```xml
<AlienRace.ThingDef_AlienRace>
  <generalSettings>
    <ageStatOverrides>

      <!-- Individual StatDef overrides here -->

    </ageStatOverrides>
  </generalSettings>
</AlienRace.ThingDef_AlienRace>
```

Any StatDef with a StatPart_Age component can be overridden in this way, including those from mods. The following are all vanilla StatDefs with such a node, with the human default curves shown:

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<WorkSpeedGlobal>
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(4,0.2)</li>
      <li>(12,0.8)</li>
      <li>(18,1)</li>
    </points>
  </curve>
</WorkSpeedGlobal>
```
</td><td>
Children usually perform work much slower than adults.
</td></tr>
<tr><td>

```xml
<ShootingAccuracyChildFactor MayRequire="Ludeon.RimWorld.Biotech">
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(4,0.95)</li>
      <li>(12,0.98)</li>
      <li>(13,1)</li>
    </points>
  </curve>
</ShootingAccuracyChildFactor>
```
</td><td>
Children have slightly reduced shooting accuracy. Note that this StatDef is unique to Biotech, thus it should have a <code>MayRequire</code> attribute or it will generate errors without Biotech loaded.
</td></tr>
<tr><td>

```xml
<MarketValue>
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(3,0.5)</li>
      <li>(13,0.9)</li>
      <li>(18,1)</li>
    </points>
  </curve>
</MarketValue>
```
</td><td>
Children are usually worth less in terms of colony wealth and to slavers.
</td></tr>
<tr><td>

```xml
<MeleeHitChance>
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(4,0.05)</li>
      <li>(12,0.8)</li>
      <li>(13,1)</li>
    </points>
  </curve>
</MeleeHitChance>
```
</td><td>
Children have a significant penalty to melee accuracy.
</td></tr>
<tr><td>

```xml
<AimingDelayFactor>
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(4,1.8)</li>
      <li>(12,1.1)</li>
      <li>(13,1)</li>
    </points>
  </curve>
</AimingDelayFactor>
```
</td><td>
Children fire ranged weapons significantly slower than adults.
</td></tr>
<tr><td>

```xml
<ImmunityGainSpeed>
  <curve>
    <points>
      <li>(0.65,1)</li>
      <li>(0.8,0.95)</li>
      <li>(1.0,0.9)</li>
      <li>(1.2,0.8)</li>
      <li>(1.5,0.5)</li>
    </points>
  </curve>
</ImmunityGainSpeed>
```
</td><td>
Elderly pawns have significantly reduced immunity gain speed, making them more vulnerable to diseases. Note that this is the only vanilla StatDef that does not use biologicalYears as it's used by animals in addition to humanlikes; the left side value is a factor of the race's life expectancy.
</td></tr>
<tr><td>

```xml
<ArrestSuccessChance>
  <useBiologicalYears>true</useBiologicalYears>
  <curve>
    <points>
      <li>(3, 0.05)</li>
      <li>(13, 0.8)</li>
      <li>(18, 1)</li>
    </points>
  </curve>
</ArrestSuccessChance>
```
</td><td>
Children have a significantly lower chance of arresting individuals.
</td></tr>
</tbody>
</table>

### Reproduction Settings

The following settings are listed in the <code>reproduction</code> tag inside of <code>generalSettings</code>:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <reproduction>
        <!-- Reproduction settings are listed here -->
      </reproduction>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Unless otherwise specified, all of the following settings are optional.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<childKindDef>AlienColonist</childKindDef>
```
</td><td>
Overrides the <code>PawnKindDef</code> that newborn children of your race should use.<br/><br/>
By default, Biotech uses the <code>PawnKindDef</code> of the mother at birth.
</td></tr>
<tr><td>

```xml
<maleFertilityAgeFactor>
  <points>
    <li>(14, 0)</li>
    <li>(18, 1)</li>
    <li>(50, 1)</li>
    <li>(90, 0)</li>
  </points>
</maleFertilityAgeFactor>
```
</td><td>
Sets the fertility of male members of your race.<br/><br/>
The human default is as shown.
</td></tr>
<tr><td>

```xml
<femaleFertilityAgeFactor>
  <points>
    <li>(14, 0)</li>
    <li>(20, 1)</li>
    <li>(28, 1)</li>
    <li>(35, 0.5)</li>
    <li>(40, 0.1)</li>
    <li>(45, 0.02)</li>
    <li>(50, 0)</li>
  </points>
</femaleFertilityAgeFactor>
```
</td><td>
Sets the fertility of female members of your race.<br/><br/>
The human default is as shown.
</td></tr>
<tr><td>

```xml
<hybridSpecific>

  <!-- single outcome -->
  <li>
    <partnerRace>BlueAlien</partnerRace>
    <childKindDef>BlueHybrid</childKindDef>
  </li>

  <!-- multiple outcomes -->
  <li>
    <partnerRace>GreenAlien</partnerRace>
    <probability>100</probability>
    <childKindDef>GreenHybrid</childKindDef>
  </li>
  <li>
    <partnerRace>GreenAlien</partnerRace>
    <probability>50</probability>
    <childKindDef>YellowHybrid</childKindDef>
  </li>

</hybridSpecific>
```
</td><td>
Specifies the <code>PawnKindDef</code> that should be used if a mother of your race has a baby
with a father of the specified race.<br/><br/>
<code>probability</code> is an optional weight value that can be used to adjust the chance
of any one particular outcome if more than one <code>childKindDef</code> is possible for a given father race.
</td></tr>
<tr><td>

```xml
<fertilizingGender>Male</fertilizingGender>
```
</td><td>
Set which gender(s) of your race perform fertilization in reproduction. Options are <code>Male</code>, <code>Female</code>, or<code>Either</code>.<br/><br/>
Defaults to <code>Male</code>.
</td></tr>
<tr><td>

```xml
<gestatingGender>Femle</gestatingGender>
```
</td><td>
Set which gender(s) of your race perform gestation in reproduction. Options are <code>Male</code>, <code>Female</code>, or<code>Either</code>.<br/><br/>
Defaults to <code>Female</code>.
</td></tr>
</tbody>
</table>
