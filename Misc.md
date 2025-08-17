These are some additional tools and options that can be useful for edge case scenarios when
creating humanoid alien races.

## ```AlienRace.Info``` DefModExtension

Humanoid Alien Races adds a custom DefModExtension that can be used on ```PawnKindDef```s.
This extension gives you a small subset of options that are available on [[General Settings]],
but will only apply to this specific PawnKind.

```xml
<PawnKindDef>
  <defName>MyRace_CustomPawnKind</defName>
  
  <!-- many fields omitted -->

  <modExtensions>
    <li Class="AlienRace.Info">
      <!-- mod extension settings go here -->
    </li>
  </modExtensions>
  
</PawnKindDef>
```

### Available Settings
<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>

<tr><td>

```xml
<allowHumanBios>false</allowHumanBios>
```
</td><td>
(Optional, default: <code>true</code>) If set to <code>false</code>, then disables the use of
human PawnBios for this PawnKind if human PawnBios are allowed at a race level. Setting this to
<code>true</code> does nothing if the race itself does not allow human PawnBios.
</td></tr>
<tr><td>

```xml
<maleGenderProbability>0.5</maleGenderProbability>
```
</td><td>
(Optional, default: <code>0.5</code>) Overrides the gender probability for this PawnKind.

**Warning**: If you use this mod extension, then its default value of <code>0.5</code> will
override your race's main setting even if you do not explicitly fill this field.
</td></tr>

</tbody>
</table>


## Custom Lifestages

Humanoid Alien Races also has a custom subclass for LifeStageAges, which can be used to
override various race settings for pawns of your race at those age ranges.

You can use this by specifying a ```Class``` attribute for a lifestage list item:

```xml
<AlienRace.ThingDef_AlienRace>
  <defName>MyMod_MyRace</defName>
  
  <!-- many fields omitted -->
  
  <race>
    <lifeStageAges>
      <li Class="AlienRace.LifeStageAgeAlien">
        <def>MyRace_Larva</def>
        <minAge>0</minAge>
        
        <!-- settings go here -->
        
      </li>
      <li>
        <def>HumanlikeTeenager</def>
        <minAge>13</minAge>
      </li>
      <li>
        <def>HumanlikeAdult</def>
        <minAge>18</minAge>
      </li>
    </lifeStageAges>
  </race>
  
</AlienRace.ThingDef_AlienRace>
```

### Available Settings
<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>

<tr><td>

```xml
<body>MyRace_LarvaBody</body>
```
</td><td>
(Optional) If set, overrides the BodyDef used by members of your race at this lifestage.
</td></tr>
<tr><td>

```xml
<headOffset />
<headOffsetSpecific />
<customDrawSize />
<customPortraitDrawSize />
<customHeadDrawSize />
<customPortraitHeadDrawSize />
<headFemaleOffset />
<headFemaleOffsetSpecific />
<customFemaleDrawSize />
<customFemalePortraitDrawSize />
<customFemaleHeadDrawSize />
<customFemalePortraitHeadDrawSize />
```
</td><td>
(Optional) Overrides the offset values for this life stage. Please see [[General Settings]]
for more details.
</td></tr>

</tbody>
</table>

## Custom BodyTypeDefs

If the vanilla BodyTypes do not suit your race and your race's custom body style does not fit
any vanilla silhouettes, you can create your own BodyTypeDefs. You can use the vanilla
```BodyTypeDefs``` as a reference, which can be found under ```Data/Core/Defs/Misc/BodyTypeDefs```.

Note that this can introduce a number of compatibility issues, as apparel without explicit textures
for your custom BodyTypes will render as error boxes unless you use [[Apparel Graphics]] fallbacks.

**(RimWorld 1.3 Only)**: All BodyTypeDefs must have `woundAnchors` defined - otherwise, when members of your race are injured, their body add-ons and hair may not render properly while they are lying in bed.
