*(This is a sub-page of [[General Settings|General-Settings]].)*

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

You can create any number of BodyAddons simply by creating a <code>&lt;li&gt;</code> tag for each one:

```xml
<bodyAddons>
  <li>
    <!-- Settings for first BodyAddon -->
  </li>
  <li>
    <!-- Settings for second BodyAddon -->
  </li>
  <li>
    <!-- Settings for third BodyAddon, and so on... -->
  </li>
</bodyAddons>
```

## Basic Settings


### Texture Path (Required)

```xml
<path>Path/To/Texture/MyBodyAddon</path>
```

Sets the path to your BodyAddon's textures. Uses the <code>Graphic_Multi</code> loader, meaning that textures are directional and the loader will look for files with <code>_north</code>, <code>_south</code>, <code>_east</code>, and <code>_west</code>, though if you omit <code>_west</code>, then the <code>_east</code> texture will automatically be mirrored. This is the only required field for a BodyAddon.<br/><br/>

You can also add variant textures for your BodyAddons simply by appending numbers to additional variants:

```
MyBodyAddon_north.png
MyBodyAddon1_north.png
MyBodyAddon2_north.png
MyBodyAddon3_north.png
etc.
```

Color masks can also be used for BodyAddons by using standard Graphic_Multi mask naming:

```
MyBodyAddon_northm.png
MyBodyAddon1_northm.png
MyBodyAddon2_northm.png
MyBodyAddon3_northm.png
etc.
```

BodyAddons support both single and dual color masks, using red (<code>#FF0000</code>) for the <code>first</code> color in the channel, green (<code>#00FF00</code>) for the <code>second</code> color in the channel, and black (<code>#000000</code>) for no color.

### Rendering Conditions

**RimWorld 1.5+ only** - See Legacy Optional Settings below for options prior to RimWorld 1.5.

The following options should be placed inside a `<conditions>` tag inside of any body addons you wish to apply them to:

```xml
<bodyAddons>
  <li>
    <path>Path/To/Base/Texture</path>
    <conditions>
      <!-- Body Addon conditions here -->
    </conditions>
  </li>
</bodyAddons>
```

<table>
<thead>
<tr><th align="left">Condition</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<BodyPart>
  <bodyPart>Alien_Tail</bodyPart>
  <drawWithoutPart>false</drawWithoutPart>
</BodyPart>
```
or
```xml
<BodyPart>
  <bodyPartLabel>left horn</bodyPartLabel>
  <drawWithoutPart>false</drawWithoutPart>
</BodyPart>
```
</td><td>
Draws this addon only if the specified body part exists and is not destroyed. <code>drawWithoutPart</code> defaults to <code>false</code>.
</td></tr>
<tr><td>

```xml
<RotStage>Fresh,Rotting,Dessicated</RotStage>
```
</td><td>
Draws this addon only for the specified rot stages. <code>Fresh,Rotting</code> replicates the old option for <code>drawnDesiccated=false</code>.
</td></tr>
<tr><td>

```xml
<Drafted>true</Drafted>
```
</td><td>
Draws this addon only for the specified drafted state. By default, draws for both states.
</td></tr>
<tr><td>

```xml
<Job>LayDown</Job>
```
</td><td>
Draws this addon only if the pawn is actively performing the specified JobDef.
</td></tr>
<tr><td>

```xml
<Moving>false</Moving>
```
</td><td>
Draws this addon only if the pawn is in the specified movement state. Draws for both by default.
</td></tr>
<tr><td>

```xml
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
```
</td><td>
Hides this body addon if apparel is being worn that covers the specified body part groups or uses the specified apparel tags.
</td></tr>
<tr><td>

```xml
<ApparelDef>
  <apparel>Apparel_Tribalwear</apparel>
  <stuff>Leather_Human</stuff>
</ApparelDef>
```
</td><td>
Draws this body addon only if the specified apparel ThingDef is being worn, optionally also using the specified <code>stuff</code> ThingDef.
</td></tr>
<tr><td>

```xml
<Posture>
  <drawnStanding>false</drawnStanding>
  <drawnLaying>false</drawnLaying>
  <drawnInBed>false</drawnInBed>
</Posture>
```
</td><td>
Designates whether this body addon should be drawn for the specified postures. All are defaulted to <code>false</code> if this tag is used.<br/><br/>
NOTE: Without a <code>Posture</code> tag, any body addon with <code>alignWithHead</code> set to true will be drawn in bed, and all other addons will not not be drawn in bed. All addons will be drawn standing and laying. <code>Posture</code> should only be used if you need to change the normal behavior.
</td></tr>
<tr><td>

```xml
<Damage>1.0</Damage>
```
</td><td>
Draws this body addon only if the linked body part's hit points are at or below the specified threshold. <code>1.0</code> designates a healthy body part, whereas <code>0.0</code> is a destroyed body part. Only functions if a <code>BodyPart</code> is specified.
</td></tr>
<tr><td>

```xml
<Age>HumanlikeAdult</Age>
```
</td><td>
Draws this body addon only if the pawn is at the specified LifeStageDef.
</td></tr>
<tr><td>

```xml
<Hediff>BionicSpine</Hediff>
```
of
```xml
<Hediff>
  <hediff>Burn</hediff>
  <severities>
    <li>5</li>
  </severities>
</Hediff>
```
</td><td>
Draws this body addon only if the specified HediffDef is present on the pawn. If one or more <code>BodyPart</code> fields are specified, then only the last one resolved will be checked for the specified Hediff.
</td></tr>
<tr><td>

```xml
<Backstory>AlienHulk</Backstory>
```
</td><td>
Draws this body addon only if the pawn has the specified BackstoryDef.
</td></tr>
<tr><td>

```xml
<Gender>Female</Gender>
```
</td><td>
Draws this body addon only if the pawn is of the specified gender.
</td></tr>
<tr><td>

```xml
<Trait>Psychopath</Trait>
```
</td><td>
Draws this body addon only if the pawn has the specified TraitDef.
</td></tr>
<tr><td>

```xml
<BodyType>Hulk</BodyType>
```
</td><td>
Draws this body addon only if the pawn has the specified BodyTypeDef.
</td></tr>
<tr><td>

```xml
<HeadType>Male_AverageNormal</HeadType>
```
</td><td>
Draws this body addon only if the pawn has the specified HeadTypeDef.
</td></tr>
<tr><td>

```xml
<Gene>Robust</Gene>
```
</td><td>
<strong>Biotech DLC only</strong><br/><br/>
Draws this body addon only if the pawn has the specified GeneDef.
</td></tr>
<tr><td>

```xml
<Race>MyAlienRace</Race>
```
</td><td>
Draws this body addon only if the pawn is of the specified race. Only functions for Universal Body Addons.
</td></tr>
<tr><td>

```xml
<Mutant>Shambler</Mutant>
```
</td><td>
<strong>Anomaly DLC only</strong><br/><br/>
Draws this body addon only if the pawn has the specified MutantDef.
</td></tr>
<tr><td>

```xml
<CreepJoinerFormKind>DarkScholar</CreepJoinerFormKind>
```
</td><td>
<strong>Anomaly DLC only</strong><br/><br/>
Draws this body addon only if the pawn has the specified CreepJoinerFormKindDef.
</td></tr>
</tbody>
</table>

This system can also be used to specify "and" or "or" conditions:

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

Alternatively you can also negate an entry.

```xml
<conditions>
  <Not>
    <Hediff>Cataract</Hediff>
  </Not>
</conditions>
```

### Optional Settings

The following options should be placed directly inside the body addon <code>li</code> tag:

```xml
<bodyAddons>
  <li>
    <path>Path/To/Base/Texture</path>

    <!-- Body Addon options here -->

  </li>
</bodyAddons>
```

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<userCustomizable>false</userCustomizable>
```
</td><td>
<code>true</code>
</td><td>
<strong>RimWorld v1.4 and later</strong><br/><br/>

If set to <code>false</code>, then the specified BodyAddon will not be customizable by players at the Ideology styling station. This should generally only be used for BodyAddons that have no variants or color options and thus cannot be customized anyways.
</td></tr>
<tr><td>

```xml
<allowColorOverride>true</allowColorOverride>
```
</td><td>
<code>false</code>
</td><td>
<strong>RimWorld v1.4 and later</strong><br/><br/>

If set to true, then players will be able to color this BodyAddon separately from the normal color channel assigned to this BodyAddon via the Ideology styling station. By default, players must change the color by changing the assigned color channel (which may be the skin, hair, or tattoo color if appropriate).
</td></tr>
<tr><td>

```xml
<inFrontOfBody>true</inFrontOfBody>
```
</td><td>
<code>false</code>
</td><td>
If set to <code>true</code>, then attempts to render this BodyAddon in front of the body by default, and behind if the pawn is facing north.<br/><br/>
Specifically, this will add <code>0.3</code> to the BodyAddon's y-axis offset while the pawn is facing south and subtract <code>0.3</code> while it is facing north.
</td></tr>
<tr><td>

```xml
<layerInvert>false</layerInvert>
```
</td><td>
<code>true</code>
</td><td>
By default, the y-axis offset of BodyAddons is inverted when a pawn is facing north. If this is set to <code>false</code>, then the y-offset will not be inverted.
</td></tr>
<tr><td>

```xml
<layerOffset>0.02</layerOffset>
```
</td><td>
<code>0.0</code>
</td><td>
<strong>RimWorld v1.2 and earlier only</strong><br/><br/>
Allows for precise control of y-axis offset. Replaced by the <code>offsets</code> tag in RimWorld 1.3 and later.
</td></tr>
<tr><td>

```xml
<angle>20</angle>
```
</td><td>
<code>0</code>
</td><td>
Sets a rotational offset for this BodyAddon.<br/><br/>
This value is measured in degrees and is applied directly to the South and West rotation of the pawn, and is mirrored for the East rotation.
It is ignored for North rotations.
</td></tr>
<tr><td>

```xml
<alignWithHead>true</alignWithHead>
```
</td><td>
<code>false</code>
</td><td>
If set to <code>true</code>, adds the head positional offset to the draw position of this BodyAddon. This adjusts to different head offset values.
</td></tr>
<tr><td>

```xml
<defaultOffset>Center</defaultOffset>
```
</td><td>
<code>Center</code>
</td><td>
Sets the offset to use with this BodyAddon. Available options are <code>Center</code> (default), <code>Head</code>, and <code>Tail</code>.<br /><br />
Unlike <code>alignWithHead</code>, this value does not adjust to head offsets. If you use <code>alignWithHead</code>, leaving this on <code>Center</code> is recommended.
</td></tr>
<tr><td>

```xml
<drawSize>(1.25,0.8)</drawSize>
```
</td><td>
<code>(1.0,1.0)</code>
</td><td>
Sets the default draw size of this BodyAddon in tile units.
</td></tr>
<tr><td>

```xml
<drawSizePortrait>
  (1.25,0.8)
</drawSizePortrait>
```
</td><td>
<code>(0.0,0.0)</code>
</td><td>
Sets the draw size of this BodyAddon when drawn in a portrait, such as on the top colonist bar. If this value is set to the default value of <code>Vector2.zero</code>, then the regular <code>drawSize</code> will be used instead.
</td></tr>
<tr><td>

```xml
<drawRotated>false</drawRotated>
```
</td><td>
<code>true</code>
</td><td>
By default, BodyAddons will use different textures for each pawn direction. If this is set to <code>false</code>, then the North graphic will be used for all directions.
</td></tr>
<tr><td>

```xml
<scaleWithPawnDrawsize>
  true
</scaleWithPawnDrawsize>
```
</td><td>
<code>false</code>
</td><td>
If enabled, then the draw size of this BodyAddon is multiplied by your race's <code>customDrawSize</code>, <code>customHeadDrawSize</code>, <code>customPortraitDrawSize</code>, or <code>customPortraitHeadDrawSize</code> as appropriate.
</td></tr>
<tr><td>

```xml
<colorChannel>skin</colorChannel>
```
</td><td>
<code>skin</code>
</td><td>
Sets the color channel that should be used for this BodyAddon. See [[General Settings]] for more information about color channels.
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
If enabled and this BodyAddon has one or more variant textures, then the exact variant used will be matched to the index of the BodyAddon that directly precedes this one in the <code>bodyaddons</code> list. This can be used to match variants on paired BodyAddons such as ears or horns.
</td></tr>
<tr><td>

```xml
<offsets>
  <south>
    <layerOffset>0.25</layerOffset>
    <offset>(0.42,-0.22)</offset>
    <bodyTypes>
      <Hulk>(0.48,-0.11)</Hulk>
      <Fat>(0.36,-0.18)</Fat>
    </bodyTypes>
    <headTypes>
      <Average_Normal>(0.40,-0.21)</Average_Normal>
    </headTypes>
    <portraitBodyTypes>
      <Hulk>(0.48,-0.11)</Hulk>
      <Fat>(0.36,-0.18)</Fat>
    </portraitBodyTypes>
    <portraitHeadTypes>
      <Average_Normal>(0.40,-0.21)</Average_Normal>
    </portraitHeadTypes>
  </south>
  <north>
    <!-- same structure repeated -->
  </north>
  <east>
    <!-- same structure repeated -->
  </east>
  <west>
    <!-- optional, mirrors east if omitted -->
  </west>
</offsets>
```
</td><td>
(See Desc.)
</td><td>
Sets the draw position offsets for this BodyAddon based on pawn facing direction.<br/><br/>
Each individual list is optional, the base <code>offset</code> (which itself defaults to Vector2.zero (0,0)) will be used for undefined values.<br/><br/>
<code>portraitBodyTypes</code> and <code>portraitHeadTypes</code> are optional and should only be used if the alignment on portraits is off. If omitted, the regular <code>bodyTypes</code> and <code>headTypes</code> or their defaults will be used instead.<br/><br/>
In RimWorld 1.3 and prior, <code>crownTypes</code> and <code>portraitCrownTypes</code> was used instead of <code>headTypes</code> and <code>portraitHeadTypes</code>
</td></tr>
<tr><td>

```xml
<femaleOffsets>
  <!-- same options as above -->
</femaleOffsets>
```
</td><td>
(See Desc.)
</td><td>
(Optional) Sets the draw position offsets for female pawns of your race. 
</td></tr>
<tr><td>

```xml
<shaderType>Transparent</shaderType>
```
</td><td>
<code>Cutout</code>
</td><td>
Sets the ShaderType for this BodyAddon. If a color mask is used for this BodyAddon, this value will be overridden with <code>CutoutComplex</code>.<br/><br/>
<strong>RimWorld v1.3 and later</strong>: Due to the pawn atlas (render cache), this may not behave exactly as expected as it will determine the shader used to draw this BodyAddon to the atlas instead of to the actual world. As such, relying on it to use special ShaderTypes such as <code>TransparentPostLight</code> may not do what you want it to.
</td></tr>
</tbody>
</table>

### Legacy Optional Settings

**RimWorld 1.4 and earlier** - The following settings are no longer available in RimWorld 1.5+

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<bodyPart>CustomBodyPart</bodyPart>
```
or
```xml
<bodyPartLabel>left ear</bodyPartLabel>
```
</td><td>
(None)
</td><td>
If set, then this body addon is only shown if the specified body part exists in the pawn's body and is not missing. This is typically used to link addons to specific body parts such as ears or tails and if the body part is destroyed then the body addon is hidden as well. <code>bodyPart</code> is used to reference a BodyPartDef and <code>bodyPartLabel</code> is used to reference a <code>label</code> in the BodyDef; if both are specified, then a body part that matches both the BodyPartDef and the label must exist and be non-missing in order for this BodyAddon to render.
</td></tr>
<tr><td>

```xml
<drawWithoutPart>true</drawWithoutPart>
```
</td><td>
<code>false</code>
</td><td>
If set to <code>true</code>, then this body addon will render even if it is linked to a body part that is missing. This is useful if you want to show specific alt textures for the <code>MissingBodyPart</code> hediff; see [[Extension Graphics]] for more information.
</td></tr>
<tr><td>

```xml
<geneRequirement>CustomGene</geneRequirement>
```
</td><td>
(None)
</td><td>
<strong>Biotech DLC only</strong><br/><br/>
If set, shows this BodyAddon only on members of your race with the specified <code>GeneDef</code>.
</td></tr>
<tr><td>

```xml
<drawnOnGround>false</drawnOnGround>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn while the pawn is prone, such as if it has been downed or knocked over by a large animal.
</td></tr>
<tr><td>

```xml
<drawnInBed>false</drawnInBed>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn while the pawn is lying down in a bed that normally hides the body. Typically used for torso or lower body parts.<br/><br/>
Does not apply in sleeping spots.
</td></tr>
<tr><td>

```xml
<drawnDesiccated>false</drawnDesiccated>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn while the pawn's corpse is in a dessicated (skeletal) state.
</td></tr>
<tr><td>

```xml
<drawForMale>false</drawForMale>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn for male pawns.
</td></tr>
<tr><td>

```xml
<drawForFemale>false</drawForFemale>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn for female pawns.
</td></tr>
<tr><td>

```xml
<drawDrafted>false</drawDrafted>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn for pawns that are drafted.
</td></tr>
<tr><td>

```xml
<drawUndrafted>false</drawUndrafted>
```
</td><td>
<code>true</code>
</td><td>
If disabled, then this BodyAddon will not be drawn for pawns that are not drafted.
</td></tr>
<tr><td>

```xml
<jobs>
  <drawNoJob>false</drawNoJob>
  <jobs>
    <li>
      <job>LayDown</job>
      <drawPostures>
        <li><key>LayingInBed</key><value>true</value></li>
      </drawPostures>
      <drawMoving>false</drawMoving>
      <drawUnmoving>true</drawUnmoving>
    </li>
    <li>
      <job>Arrest</job>
      <drawMoving>true</drawMoving>
      <drawUnmoving>false</drawUnmoving>
    </li>
  </jobs>
</jobs>
```
</td><td>
(None)
</td><td>
Allows you to specify whether this BodyAddon should be drawn when a pawn of your race is performing certain jobs.<br/><br/>
If <code>drawNoJob</code> is disabled (default <code>true</code>), then this BodyAddon will not be drawn if the pawn has no current job.<br/><br/>
If <code>drawMoving</code> is disabled (default <code>true</code>), then this BodyAddon will not be drawn if the pawn is performing a moving Toil for the specified job.<br/><br/>
If <code>drawUnmoving</code> is disabled (default <code>true</code>), then this BodyAddon will not be drawn if the pawn is performing a non-moving Toil for the specified job.
</td></tr>
<tr><td>

```xml
<hediffGraphics>
  <ProstheticBodyPart>
    Path/To/Texture
  </ProstheticBodyPart>
  <BionicBodyPart>
    Path/To/Texture
  </BionicBodyPart>
  <Frostbite>
    <path>Path/To/Base/Texture</path>
    <severity>
      <a0.8>Path/To/Extreme/Texture</a0.8>
      <a0.5>Path/To/Major/Texture</a0.5>
      <a0.2>Path/To/Minor/Texture</a0.2>
    </severity>
  </Frostbite>
</hediffGraphics>
```
</td><td>
(None)
</td><td>
Allows you to provide specific alternate textures for this BodyAddon if specific Hediffs are present. Typically used to provide alternate graphics for implants or bionics.<br/><br/>
You can also specify a list if you want different textures based on hediff severity.<br /><br/>
<strong>RimWorld 1.4 and later:</strong> This has been superseded by [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<backstoryGraphics>
  <CustomBackstory>
    Path/To/Backstory/Texture
  </CustomBackstory>
  <AnotherCustomBackstory>
    Path/To/Backstory/Texture
  </AnotherCustomBackstory>
</backstoryGraphics>
```
</td><td>
(None)
</td><td>
Allows you to provide specific alternate textures for this BodyAddon if the pawn has a specific backstory.<br /><br/>
<strong>RimWorld 1.4 and later:</strong> This has been superseded by [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<prioritization>
  <li>Hediff</li>
  <li>Backstory</li>
</prioritization>
```
</td><td>
<code>Backstory</code>
<code>Hediff</code>
</td><td>
By default, backstory overrides have priority over hediff-based overrides. You can use this to change that priority.<br /><br/>
<strong>RimWorld 1.4 and later:</strong> This has been superseded by [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<backstoryRequirement>
  CustomBackstory
</backstoryRequirement>
```
</td><td>
(None)
</td><td>
If set, this BodyAddon will only be drawn if the pawn has the specified backstory.
</td></tr>
<tr><td>

```xml
<hiddenUnderApparelTag>
  <li>CustomApparelTag</li>
</hiddenUnderApparelTag>
<hiddenUnderApparelFor>
<li>FullHead</li>
<li>UpperHead</li>
</hiddenUnderApparelFor>
```
</td><td>
(None)
</td><td>
Used to hide this BodyAddon if the pawn is wearing apparel with the specified apparelTags or that cover the specified BodyPartGroups.
</td></tr>
</tbody>
</table>

## Extension Graphics

In RimWorld 1.4 and later, [[Extension Graphics|Extension-Graphics]] can be used on Body Addons. This is an expansion of the <code>hediffGraphics</code> system.
