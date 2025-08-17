*(This is a sub-page of [[Graphic Paths|Graphic-Paths]].)*

**This feature is only available in Humanoid Alien Races for RimWorld 1.4.** It is not available in earlier versions.

Apparel Graphics allow you to specify override and fallback graphics for apparel worn by your race.
They can be used to improve compatibility with apparel, such as:

1. Providing custom headwear textures for races with non-standard heads,
2. Providing alternate textures for races with override textures for vanilla body types, or
3. Providing fallback textures for races with custom body types for apparel without explicit textures.

Apparel Graphics can be specified inside [[Graphic Paths|Graphic-Paths]] like so:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <graphicPaths>
      <apparel>
        <!-- Apparel Graphics options go here -->
      </apparel>
    </graphicPaths>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

# Settings

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<individualPaths>
  <li>
    <key>Apparel_CowboyHat</key>
    <value>Path/To/Hat/Texture</value>
  </li>
  <li>
    <key>Apparel_Parka</key>
    <value>Path/To/Parka/Texture</value>
  </li>
  <li>
    <key>CustomApparelDef</key>
    <value>Path/To/Custom/Texture</value>
  </li>
</individualPaths>
```
</td><td>
If set, overrides the <code>wornGraphicPath</code> of the specified apparel for your race.
<code>pathPrefix</code> is not applied to these paths.
</td></tr>
<tr><td>

```xml
<pathPrefix>Path/Prefix/</pathPrefix>
```
</td><td>
If set, will attempt to find custom textures for worn apparel by prepend the given prefix to the
<code>wornGraphicPath</code> of all apparel (including headwear) worn by your race.
</td></tr>
<tr><td>

```xml
<fallbacks>
  <li>
    <!-- fallback options go here -->
  </li>
  <li>
    <!-- more options go here -->
  </li>
  <li>
    <!-- you can do this all day -->
  </li>
</fallbacks>
```
</td><td>
Specifies fallback textures based on a number of criteria. Fallback options are checked for suitability in list order and the first match for any given piece of apparel will be used. Please see the Fallback Options section below for more details.
</td></tr>
<tr><td>

```xml
<overrides>
  <li>
    <!-- override options go here -->
  </li>
  <li>
    <!-- more options go here -->
  </li>
  <li>
    <!-- you can do this all day -->
  </li>
</overrides>
```
</td><td>
Specifies override textures based on a number of criteria. Same options and logic as the fallbacks above, but checked before the original texture.
</td></tr>
<tr><td>

```xml
<bodyTypeFallback>Hulk</bodyTypeFallback>
```
</td><td>
Default value: (None)<br /><br />

If set, will attempt to use textures for the specified body type for your race if other override options do not yield
usable textures.
</td></tr>
<tr><td>

```xml
<femaleBodyTypeFallback>Thin</femaleBodyTypeFallback>
```
</td><td>
Default value: (None)<br /><br />

If set, will attempt to use textures for the specified body type for female members of your race if other
override options do not yield usable textures.
</td></tr>
</tbody>
</table>

## Fallback Options

The following options are usable inside `<fallbacks>` entries.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<wornGraphicPath>Path/To/Texture</wornGraphicPath>
```
or
```xml
<wornGraphicPaths>
  <li>Path/To/Texture</li>
  <li>Path/To/Another/Texture</li>
  <li>Path/To/Alternate/Texture</li>
</wornGraphicPaths>
```
</td><td>
The texture or textures to be used if this fallback is suitable for the given Apparel.<br/><br/>
If the plural <code>wornGraphicPaths</code> is used, then a semi-random entry from the list will be used
based on the apparel Def's <code>HashCode</code>.<br/><br/>
<em>Tip: You can also use a fully transparent texture to make apparel invisible.</em> 
</td></tr>
<tr><td>

```xml
<apparelTags>
  <li>IndustrialBasic</li>
  <li>MyApparelTag</li>
</apparelTags>
```
</td><td>
If set, then this fallback will only be used if the apparel has at least one of the specified apparel tags.
</td></tr>
<tr><td>

```xml
<bodyPartGroups>
  <li>Torso</li>
  <li>Legs</li>
</bodyPartGroups>
```
</td><td>
If set, then this fallback will only be used if the apparel covers at least one of the specified body part groups.
</td></tr>
<tr><td>

```xml
<layers>
  <li>Overhead</li>
  <li>Shell</li>
  <li>Middle</li>
  <li>OnSkin</li>
</layers>
```
</td><td>
If set, then this fallback will only be used if the apparel occupies at least one of the specified apparel layers.
</td></tr>
</tbody>
</table>

All path nodes also support [[Extension Graphics|Extension-Graphics]]. For example, you could set different `<pathPrefix>` values based on pawn gender:

```xml
<graphicPaths>
  <apparel>

    <pathPrefix>
      <path>MyRace/</path>
      <extendedGraphics>
        <Gender For="Male">MyRace/Male/</Gender>
        <Gender For="Female">MyRace/Female/</Gender>
      </extendedGraphics>
    </pathPrefix>

  </apparel>
</graphicPaths>
```

Note that if you use Extension Graphics for `<individualPaths>` or `<fallbacks>`, the pawn's BodyType will not be automatically appended to the path; you will need to specify it explicitly if needed:

```xml
<graphicPaths>
  <apparel>

    <fallback>
      <li>
        <extendedGraphics>
          <Gender For="Male">MyRace/Apparel/CustomOutfit_Male</Gender>
          <Gender For="Female">MyRace/Apparel/CustomOutfit_Female</Gender>
        </extendedGraphics>
      </li>
    </pathPrefix>

  </apparel>
</graphicPaths>
```

## Override Priority

Apparel Graphics are resolved in the following order:

1. If an `individualPaths` entry for a given Apparel type is specified, the path given will be used. Further fallbacks will not be used if no usable textures are found at the specified path.
2. If a `prefixPath` is set, then an attempt to find custom textures for your race will be made. If textures are not found, then the next step will be attempted.
3. The standard `wornGraphicPath` will be searched for usable textures. If no textures are found, then fallback options will be tested.
4. Individual `fallbacks` options will be checked against the Apparel. If any matches are made, the specified graphic path will be used instead. If this fails to find usable textures, no further fallbacks will be used.
5. If the pawn is female and a `femaleBodyTypeFallback` is set, then textures for the specified body type will attempt to be used. If this fails to find usable textures, the next step will be attempted.
6. If a `bodyTypeFallback` is set, then textures for the specified body type will attempt to be used.
7. If all else fails, the standard `wornGraphicPath` will be used as per vanilla behavior. This will most likely cause an error if this point is reached.

# Examples

## Example 1: Custom BodyType Fallbacks

If you are using completely custom BodyTypes for your race, you often run into the issue of non-supported apparel not having textures for your custom BodyType. Previously this would typically mean whitelisting supported apparel and not allowing non-supported apparel to be worn, but now `<fallbacks>` can be used to specify textures to be used if a pawn of your race wears unsupported apparel:

```xml
<graphicPaths>
  <apparel>

    <fallbacks>
      <!-- Override all industrial military headwear with a helmet texture -->
      <li>
        <wornGraphicPath>MyRace/Things/Apparel/CustomHelmet</wornGraphicPath>
        <layers>
          <li>Overhead</li>
        </layers>
        <apparelTags>
          <li>IndustrialMilitaryBasic</li>
          <li>IndustrialMilitaryAdvanced</li>
        </apparelTags>
      </li>
      <!-- Override all industrial military chest armor with an armor texture -->
      <li>
        <wornGraphicPath>MyRace/Things/Apparel/CustomArmor</wornGraphicPath>
        <bodyPartGroups>
          <li>Torso</li>
        </bodyPartGroups>
        <apparelTags>
          <li>IndustrialMilitaryBasic</li>
          <li>IndustrialMilitaryAdvanced</li>
        </apparelTags>
      </li>
      <!-- Override all other chest apparel with a shirt texture -->
      <li>
        <wornGraphicPath>MyRace/Things/Apparel/CustomShirt</wornGraphicPath>
        <bodyPartGroups>
          <li>Torso</li>
        </bodyPartGroups>
      </li>
      <!-- Make all remaining non-supported apparel invisible -->
      <li>
        <wornGraphicPath>MyRace/Things/Apparel/TransparenTexture</wornGraphicPath>
      </li>
    </fallbacks>

  </apparel>
</graphicPaths>
```

Alternatively, if your race's custom body type is close enough to a vanilla body type that using the textures for the vanilla body type would be acceptable, you can specify such a fallback like so:

```xml
<graphicPaths>
  <apparel>

    <!-- Use Hulk textures for male and non-gendered pawns -->
    <bodyTypeFallback>Hulk</bodyTypeFallback>

    <!-- Use Thin textures for female pawns -->
    <femaleBodyTypeFallback>Thin</femaleBodyTypeFallback>

  </apparel>
</graphicPaths>
```

## Example 2: Race-Specific Overrides

Race-specific override textures can be used if you have:

1. Custom textures for vanilla BodyTypes (such as Kurin bodies, which override Female),
2. Custom head textures that normal human headwear doesn't fit well on, or
3. Otherwise just want to make normal apparel look differently on your race.

The recommended way to do this is with a Path Prefix:

```xml
<graphicPaths>
  <apparel>

    <!-- Prefix is added to all apparel texture requests for this race -->
    <pathPrefix>MyRace/</pathPrefix>

  </apparel>
</graphicPaths>
```

For example, these are the wornGraphicPaths for the vanilla cowboy hat and duster:

```
Things/Pawn/Humanlike/Apparel/CowboyHat/CowboyHat
Things/Pawn/Humanlike/Apparel/Duster/Duster
```

With the prefix active, Apparel Graphics will attempt to find textures at the following paths instead:

```
MyRace/Things/Pawn/Humanlike/Apparel/CowboyHat/CowboyHat
MyRace/Things/Pawn/Humanlike/Apparel/Duster/Duster
```

Alternatively, you can specify individual apparel Defs to override:

```xml
<graphicPaths>
  <apparel>

    <individualPaths>
      <li>
        <key>Apparel_Tuque</key>
        <value>MyCustomRace/Apparel/Headwear/AlienTuque</value>
      </li>
      <li>
        <key>Apparel_Parka</key>
        <value>MyCustomRace/Apparel/Body/AlienParka</value>
      </li>
    </individualPaths>

  </apparel>
</graphicPaths>
```
