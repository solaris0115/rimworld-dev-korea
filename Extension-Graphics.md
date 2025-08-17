*(This is a sub-page of [[General Settings|General-Settings]].)*

**RimWorld / Alien Races 1.4 Only** - This feature is not availble for RimWorld 1.3 and earlier.

Extension Graphics are an expansion of the old <code>hediffGraphics</code> alternate textures for [[Body Addons|Body-Addons]] that uses a [tree structure](https://en.wikipedia.org/wiki/Tree_structure) to specify a large variety of potential alternate graphics.

## Basic Layout

The primary use of Extension Graphics are in [Body Addons](https://github.com/solaris0115/rimworld-dev-korea/wiki/Body-Addons), where they replace the aforementioned <code>hediffGraphics</code> options:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <alienPartGenerator>
        <bodyAddons>
          <li>
            <path>Path/To/Base/Texture</path>
            <!-- Extension Graphics settings here -->
          </li>
        </bodyAddons>
      </alienPartGenerator>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Extension Graphics can also be used instead of simple path strings in [[Graphic Paths|Graphic-Paths]] fields:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <graphicPaths>
      <body>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </body>
      <bodyMasks>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </bodyMasks>
      <head>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </head>
      <headMasks>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </headMasks>
      <skeleton>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </skeleton>
      <skull>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </skull>
      <stump>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </stump>
      <swaddle>
        <path>Base/Texture/Path</path>
        <!-- Extension Graphics settings here -->
      </swaddle>
    </graphicPaths>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```
**Note that if using Extension Graphics, paths specified in Graphics Paths must be file paths instead of folder paths.** (i.e. <code>Path/To/Folder/SpecificHead</code> instead of <code>Path/To/Folder/</code>) Prefixes will not automatically be added for head or body graphics either. (i.e. <code>Path/To/Folder/Naked_CustomAlienBody</code> instead of just <code>Path/To/Folder/CustomAlienBody</code>)

## Base Settings

The following settings are only available on the root-level tag:

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<debug>true</debug>
```
</td><td>
<code>true</code>
</td><td>
Enables debugging for the specified node. If enabled, will log various bits of data such as how many variants are loaded.
</td></tr>
<tr><td>

```xml
<linkVariantIndexWithPrevious>
  true
</linkVariantIndexWithPrevious>
```
</td><td>
<code>false</code>
</td><td>
If enabled and this node has one or more variant textures, then the exact variant used will be matched to the index of the node that directly precedes this one in the list. This can be used to match variants on paired nodes such as ear or horn BodyAddons.<br/><br/>

For Body Addons, this is resolved in the order of the list entries. For Graphics Paths, this is resolved in the following order:<br/><br/>

<code>body &gt; bodyMasks &gt; skeleton &gt; head &gt; headMasks &gt; skull &gt; stump &gt; swaddle</code>
</td></tr>
<tr><td>

```xml
<drawSize>(1.0,1.0)</drawSize>
```
</td><td>
<code>(1.0,1.0)</code>
</td><td>
Sets the draw size of this graphic in tile units.
</td></tr>
<tr><td>

```xml
<drawSizePortrait>(0.0,0.0)</drawSizePortrait>
```
</td><td>
<code>(0.0,0.0)</code>
</td><td>
Sets the draw size of this graphic when used in portraits. By default or if set to (0,0), the default <code>drawSize</code> is used.
</td></tr>
</table>

## Texture Path

Each of the following options can be specified in a similar fashion to [[Body Addons|Body-Addons]]. Note that texture paths are *not* strictly required for Extension Graphics as if a path is not specified for a node, then it will automatically fall back to the level above it and continue searching for valid graphics.

```xml
<path>Path/To/Texture/MyBodyAddon</path>
```

This uses the <code>Graphic_Multi</code> loader, meaning that textures are directional and the loader will look for files with <code>_north</code>, <code>_south</code>, <code>_east</code>, and <code>_west</code>, though if you omit <code>_west</code>, then the <code>_east</code> texture will automatically be mirrored.<br/><br/>

You can also add variant textures for your BodyAddons simply by appending numbers to additional variants:

```
MyBodyAddon_north.png
MyBodyAddon1_north.png
MyBodyAddon2_north.png
MyBodyAddon3_north.png
etc.
```

Color masks can also be used for by using standard Graphic_Multi mask naming:

```
MyBodyAddon_northm.png
MyBodyAddon1_northm.png
MyBodyAddon2_northm.png
MyBodyAddon3_northm.png
etc.
```

All Extension Graphics support both single and dual color masks, using red (<code>#FF0000</code>) for the <code>first</code> color in the channel, green (<code>#00FF00</code>) for the <code>second</code> color in the channel, and black (<code>#000000</code>) for no color.

## Nested Settings

**RimWorld 1.5+ only** - for Extension Graphics syntax in RimWorld 1.4, see Legacy Nested Settings below.

The following settings are all optional and can be used either inside the <code>extendedGraphics</code> node or nested at any node under that level:

```xml
<bodyAddons>
  <li>
    <path>Path/To/Base/Texture</path>
    <extendedGraphics>
      <!-- Nested settings go here -->
    <extendedGraphics>
  </li>
</bodyAddons>
```
or
```xml
<bodyAddons>
  <li>
    <path>Path/To/Base/Texture</path>
    <extendedGraphics>
      <BodyType For="Hulk">
        <path>Path/To/Hulk/Textures</path>
        <extendedGraphics>
          <!-- Further nested settings go here -->
        </extendedGraphics>
      </BodyType>
    <extendedGraphics>
  </li>
</bodyAddons>
```

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<Hediff For="BionicTail">Path/To/Texture</Hediff>
```
*or*
```xml
<Hediff For="BionicTail">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Hediff>
```
</td><td>
Use this alternate graphic if the specified <code>HediffDef</code> is detected on the pawn. If a <code>bodyPart</code> is specified on the root node, then the specified Hediff must be on the linked body part for this to activate.<br/><br/>

Note: If being used for a missing body part, this needs to be in the first level of nested graphics.
</td></tr>
<tr><td>

```xml
<Severity For="0.5">Path/To/Alternate/Texture</Severity>
```
*or*
```xml
<Severity For="0.5">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Severity>
```
</td><td>
Use this alternate graphic if a parent hediff is at or above the specified severity. Only works when a Hediff is specified before in the hierarchy.
</td></tr>
<tr><td>

```xml
<Gender For="Female">Path/To/Alternate/Texture</Gender>
```
*or*
```xml
<Gender For="Female">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Gender>
```
</td><td>
If the pawn matches the specified Gender, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<BodyType For="Hulk">Path/To/Alternate/Texture</BodyType>
```
*or*
```xml
<BodyType For="Hulk">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</BodyType>
```
</td><td>
If the pawn has the specified <strong>BodyTypeDef</strong>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<HeadType For="Male_AverageNormal">Path/To/Alternate/Texture</HeadType>
```
*or*
```xml
<HeadType For="Male_AverageNormal">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</HeadType>
```
</td><td>
If the pawn has the specified <strong>HeadTypeDef</strong>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<Backstory For="AlienMutant">Path/To/Alternate/Texture</Backstory>
```
*or*
```xml
<Backstory For="AlienMutant">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Backstory>
```
</td><td>
If the pawn has the specified <code>BackstoryDef</code>, then this alternate graphic will be used. Note that this can be any <strong>BackstoryDef</strong>, not just ones created using Alien Races.
</td></tr>
<tr><td>

```xml
<Trait For="Beautiful">Path/To/Alternate/Texture</Trait>
```
*or*
```xml
<Trait For="Beautiful">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Trait>
```
</td><td>
If the pawn has the specified Trait, then this alternate graphic will be used. This can be the <code>defName</code> of a <code>TraitDef</code> or the label of a Trait's degreeData for spectrum traits.
</td></tr>
<tr><td>

```xml
<Age For="HumanlikeChild">Path/To/Alternate/Texture</Age>
```
*or*
```xml
<Age For="HumanlikeChild">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Age>
```
</td><td>
If the pawn is currently at the specified <code>LifeStageDef</code>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<Damage For="0.5">Path/To/Alternate/Texture</Damage>
```
</td><td>
If the pawn's <code>bodyPart</code> is at or below the specified hit point level, then this alternate graphic will be used. This alternate requires that a <code>bodyPart</code> be set on the root tag to work, and should be in <strong>ascending</strong> order.
</td></tr>
<tr><td>


```xml
<Need>
  <need>Food</need>
  <level>0.5</level>
  <percentage>true</percentage>
</Need>
```
</td><td>
If the pawn's <code>Need</code> is at or above the specified level, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<Mood>ABOUT_TO_BREAK, ON_EDGE, STRESSED, BAD, NEUTRAL, CONTENT, HAPPY</Mood>
```
</td><td>
If the pawn's <code>Mood</code> is at one of the specified levels, then this alternate graphic will be used.
The example shows all possible values. <code>BAD</code> is a shorthand for the first three.
</td></tr>
<tr><td>

```xml
<Race For="MyAlienRace">Path/To/Alternate/Texture</Race>
```
*or*
```xml
<Race For="MyAlienRace">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Race>
```
</td><td>
If the pawn is of the specified race, then this alternate texture will be used. Useful for Universal Body Addons.
</td></tr>
<tr><td>

```xml
<Gene For="Robust">Path/To/Alternate/Texture</Gene>
```
*or*
```xml
<Gene For="Robust">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Gene>
```
</td><td>
<strong>Biotech DLC only</strong><br/><br/>
If the pawn has the specified gene, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<Mutant For="Shambler">Path/To/Alternate/Texture</Mutant>
```
*or*
```xml
<Mutant For="Shambler">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</Mutant>
```
</td><td>
<strong>Anomaly DLC only</strong><br/><br/>
If the pawn is the specified MutantDef (such as a ghoul, shambler, or awoken corpse), then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<CreepForm For="LeatheryStranger">Path/To/Alternate/Texture</CreepForm>
```
*or*
```xml
<CreepForm For="LeatheryStranger">
  <path>Path/To/Alternate/Texture</path>
  <!-- nested settings can go here -->
</CreepForm>
```
</td><td>
<strong>Anomaly DLC only</strong><br/><br/>
If the pawn is the specified CreepJoinerFormKind, then this alternate graphic will be used.
</td></tr>
</tbody>
</table>

Prioritization is now implied instead of explicit; all nested settings are checked in the order they are listed and the first one to resolve correctly will be used.

## Example

All of the above settings can be tested to create entire trees of alternate textures.

For example, the following <code>BodyAddon</code> might be used for a race with chicken-like tails:

```xml
<bodyAddons>
  <li>
    <path>ChickenRace/Pawn/Tail/DefaultTail</path>
    <bodyPart>Tail</bodyPart>

    <Gender For="Male">
      <path>ChickenRace/Pawn/Tail/RoosterTail</path>
      <Body For="Hulk">
        <path>ChickenRace/Pawn/Tail/GiantRoosterTail</path>
        <Hediff For="ToxicBuildup">ChickenRace/Pawn/Tail/GiantIrradiatedRoosterTail</Hediff>
        <Hediff For="GoJuice">ChickenRace/Pawn/Tail/GiantSuperRoosterTail</Hediff>
      </Body>
    </Gender>
    <Gender For="Female">
      <path>ChickenRace/Pawn/Tail/HenTail</path>
      <Body For="Thin">ChickenRace/Pawn/Tail/SkinnyHenTail</Body>
      <Trait For="Beautiful">ChickenRace/Pawn/Tail/GorgeousHenTail</Trait>
    </Gender>
  </li>
</bodyAddons>
```

## Legacy Nested Settings

**RimWorld 1.4 and earlier only** - Unlike modern settings, legacy extension graphics were placed directly inside the main tag:


```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <generalSettings>
      <alienPartGenerator>
        <bodyAddons>
          <li>
            <path>Path/To/Base/Texture</path>
            <!-- Legacy nested graphics settings here -->
          </li>
        </bodyAddons>
      </alienPartGenerator>
    </generalSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<hediffGraphics>
  <MyHediffDefName>Path/To/Alternate/Texture</MyHediffDefName>
</hediffGraphics>
```
*or*
```xml
<hediffGraphics>
  <MyHediffDefName>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </MyHediffDefName>
</hediffGraphics>
```
</td><td>
Use this alternate graphic if the specified <code>HediffDef</code> is detected on the pawn. If a <code>bodyPart</code> is specified on the root node, then the specified Hediff must be on the linked body part for this to activate.<br/><br/>

Note: if being used for a missing body part hediff, this needs to be in the first level of subgraphics under the root level
</td></tr>
<tr><td>

```xml
<hediffGraphics>
  <MyHediffDefName>
    <path>Path/To/Alternate/Texture</path>
    <severity>
      <a0.50>Path/To/Alternate/Severity/Texture</a0.50>
      <a0.25>
        <path>Path/To/Another/Alternate/Severity/Texture</path>
        <!-- nested settings can go here -->
      </a0.25>
    </severity>
  </MyHediffDefName>
</hediffGraphics>
```
</td><td>
An additional <code>severity</code> field can be used to specify additional alternate textures based on the severity of the specified <code>HediffDef</code>. This can only be used as a subgraphic underneath a hediffGraphics. A specific alternate texture will be used if the severity of the Hediff is at or above the specified severity. It should be in <strong>descending</strong> order.<br/><br/>

Note: The first character of the severity value tag must be a letter and will be discarded. This is due to XML tag name rules.
</td></tr>
<tr><td>

```xml
<genderGraphics>
  <Female>Path/To/Alternate/Texture</Female>
</genderGraphics>
```
*or*
```xml
<genderGraphics>
  <Female>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </Female>
</genderGraphics>
```
</td><td>
If the pawn matches the specified Gender, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<bodytypeGraphics>
  <Hulk>Path/To/Alternate/Texture</Hulk>
</bodytypeGraphics>
```
*or*
```xml
<bodytypeGraphics>
  <Hulk>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </Hulk>
</bodytypeGraphics>
```
</td><td>
If the pawn has the specified <strong>BodyTypeDef</strong>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<headtypeGraphics>
  <Male_AverageNormal>Path/To/Alternate/Texture</Male_AverageNormal>
</headtypeGraphics>
```
*or*
```xml
<headtypeGraphics>
  <Male_AverageNormal>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </Male_AverageNormal>
</headtypeGraphics>
```
</td><td>
If the pawn has the specified <strong>HeadTypeDef</strong>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<backstoryGraphics>
  <MyCustomBackstoryDefName>Path/To/Alternate/Texture</MyCustomBackstoryDefName>
</backstoryGraphics>
```
*or*
```xml
<backstoryGraphics>
  <MyCustomBackstoryDefName>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </MyCustomBackstoryDefName>
</backstoryGraphics>
```
</td><td>
If the pawn has the specified <code>BackstoryDef</code>, then this alternate graphic will be used. Note that this can be any <strong>BackstoryDef</strong>, not just ones created using Alien Races.
</td></tr>
<tr><td>

```xml
<traitGraphics>
  <Beautiful>Path/To/Alternate/Texture</Beautiful>
</traitGraphics>
```
*or*
```xml
<traitGraphics>
  <Beautiful>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </Beautiful>
</traitGraphics>
```
</td><td>
If the pawn has the specified Trait, then this alternate graphic will be used. This can be the <code>defName</code> of a <code>TraitDef</code> or the label of a Trait's degreeData for spectrum traits.
</td></tr>
<tr><td>

```xml
<ageGraphics>
  <HumanlikeAdult>Path/To/Alternate/Texture</HumanlikeAdult>
</ageGraphics>
```
*or*
```xml
<ageGraphics>
  <HumanlikeAdult>
    <path>Path/To/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </HumanlikeAdult>
</ageGraphics>
```
</td><td>
If the pawn is currently at the specified <code>LifeStageDef</code>, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<damageGraphics>
  <a5>Path/To/Alternate/Texture</a5>
  <a10>
    <path>Path/To/Another/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </a10>
</damageGraphics>
```
</td><td>
If the pawn's <code>bodyPart</code> is at or below the specified hit point level, then this alternate graphic will be used. This alternate requires that a <code>bodyPart</code> be set on the root tag to work, and should be in <strong>ascending</strong> order.<br/><br/>
                                                                                                                                                                                                        
Note: The first character of the severity value tag must be a letter and will be discarded. This is due to XML tag name rules.
</td></tr>
<tr><td>

```xml
<geneGraphics>
  <CustomGene>Path/To/Alternate/Texture</CustomGene>
  <AnotherCustomGene>
    <path>Path/To/Another/Alternate/Texture</path>
    <!-- nested settings can go here -->
  </AnotherCustomGene>
</geneGraphics>
```
</td><td>
<strong>Biotech DLC only</strong><br/><br/>
If the pawn has the specified gene, then this alternate graphic will be used.
</td></tr>
<tr><td>

```xml
<prioritization>
  <li>Severity</li>
  <li>Hediff</li>
  <li>Gender</li>
  <li>Bodytype</li>
  <li>Headtype</li>
  <li>Backstory</li>
  <li>Trait</li>
  <li>Age</li>
  <li>Damage</li>
  <li>Gene</li>
</prioritization>
```
</td><td>
If specified, overrides the order in which alternate graphics nodes are checked. The order listed in the example is the default order, and overriding the priority in a node does not alter the prioritization of any nested child nodes.<br/><br/>
                                                                                                                                                                                                        
Note: if an alternate graphic type is omitted from the list, then it will not be checked at all.
</td></tr>
</tbody>
</table>

## Example

All of the above settings can be tested to create entire trees of alternate textures.

For example, the following <code>BodyAddon</code> might be used for a race with chicken-like tails:

```xml
<bodyAddons>
  <li>
    <path>ChickenRace/Pawn/Tail/DefaultTail</path>
    <bodyPart>Tail</bodyPart>

    <genderGraphics>
      <Male>
        <path>ChickenRace/Pawn/Tail/RoosterTail</path>
        <bodytypeGraphics>
          <Hulk>
            <path>ChickenRace/Pawn/Tail/GiantRoosterTail</path>
            <hediffGraphics>
              <ToxicBuildup>ChickenRace/Pawn/Tail/GiantIrradiatedRoosterTail</ToxicBuildup>
              <GoJuice>ChickenRace/Pawn/Tail/GiantSuperRoosterTail</GoJuice>
            </hediffGraphics>
          </Hulk>
        </bodytypeGraphics>
      </Male>
      <Female>
        <path>ChickenRace/Pawn/Tail/HenTail</path>
        <bodytypeGraphics>
          <Thin>ChickenRace/Pawn/Tail/SkinnyHenTail</Thin>
        </bodytypeGraphics>
        <traitGraphics>
          <Beautiful>ChickenRace/Pawn/Tail/GorgeousHenTail</Beautiful>
        </traitGraphics>
      </Female>
    </genderGraphics>
  </li>
</bodyAddons>
```

## Legacy Example

Here is an example for RimWorld 1.4:

```xml
<bodyAddons>
  <li>
    <path>ChickenRace/Pawn/Tail/DefaultTail</path>
    <bodyPart>Tail</bodyPart>

    <genderGraphics>
      <Male>
        <path>ChickenRace/Pawn/Tail/RoosterTail</path>
        <bodytypeGraphics>
          <Hulk>
            <path>ChickenRace/Pawn/Tail/GiantRoosterTail</path>
            <hediffGraphics>
              <ToxicBuildup>ChickenRace/Pawn/Tail/GiantIrradiatedRoosterTail</ToxicBuildup>
              <GoJuice>ChickenRace/Pawn/Tail/GiantSuperRoosterTail</GoJuice>
            </hediffGraphics>
          </Hulk>
        </bodytypeGraphics>
      </Male>
      <Female>
        <path>ChickenRace/Pawn/Tail/HenTail</path>
        <bodytypeGraphics>
          <Thin>ChickenRace/Pawn/Tail/SkinnyHenTail</Thin>
        </bodytypeGraphics>
        <traitGraphics>
          <Beautiful>ChickenRace/Pawn/Tail/GorgeousHenTail</Beautiful>
        </traitGraphics>
      </Female>
    </genderGraphics>
  </li>
</bodyAddons>
```
