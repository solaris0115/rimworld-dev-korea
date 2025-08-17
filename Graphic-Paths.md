Graphic Paths are used to override various texture paths related to your race.
**Please note that this section has changed significantly in RimWorld v1.4.**

Graphic Paths should be placed inside the <code>alienRace</code> tag:

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <graphicPaths>
      <!-- Graphic Paths are listed here -->
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
<body>Alternate/Path/Prefix/</body>
```
or
```xml
<body>
  <path>Alternate/Path/Prefix/</path>
  <!-- Extension Graphics here -->
</body>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/Bodies/</code><br /><br />

Overrides body texture paths by replacing the path up to the file name as defined in <code>BodyTypeDef</code> objects.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<bodyMasks>Path/To/Textures</bodyMasks>
```
or
```xml
<bodyMasks>
  <path>Path/To/Textures</path>
  <!-- Extension Graphics here -->
</bodyMasks>
```
</td><td>
Default value: (None)<br /><br />

If set, applies the textures at the specified location as color masks on body textures.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<head>Alternate/Path/Prefix/</head>
```
or
```xml
<head>
  <path>Alternate/Path/Prefix/</path>
  <!-- Extension Graphics here -->
</head>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/Heads/</code><br /><br />

Overrides head texture paths by replacing the path up to the file name as defined in <code>HeadTypeDef</code> objects.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<headMasks>Path/To/Textures</headMasks>
```
or
```xml
<headMasks>
  <path>Path/To/Textures</path>
  <!-- Extension Graphics here -->
</headMasks>
```
</td><td>
Default value: (None)<br /><br />

If set, applies the textures at the specified location as color masks on head textures.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<skeleton>Alternate/Path</skeleton>
```
or
```xml
<skeleton>
  <path>Alternate/Path</path>
  <!-- Extension Graphics here -->
</skeleton>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/HumanoidDessicated</code><br /><br />

Overrides the Dessicated or "skeleton" texture used for human corpses.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<skull>Alternate/Path</skull>
```
or
```xml
<skull>
  <path>Alternate/Path</path>
  <!-- Extension Graphics here -->
</skull>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/Heads/None_Average_Skull</code><br /><br />

Overrides the skull texture used for dessicated human corpses.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<stump>Alternate/Path</stump>
```
or
```xml
<stump>
  <path>Alternate/Path</path>
  <!-- Extension Graphics here -->
</stump>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/Heads/None_Average_Stump</code><br /><br />

Overrides the stump texture used for decapitated human corpses.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<swaddle>Alternate/Path</swaddle>
```
or
```xml
<swaddle>
  <path>Alternate/Path</path>
  <!-- Extension Graphics here -->
</swaddle>
```
</td><td>
Default value: <code>Things/Pawn/Humanlike/Apparel/SwaddledBaby/Swaddled_Child</code><br /><br />

Overrides the swaddle texture used for babies.
Supports [[Extension Graphics|Extension-Graphics]].
</td></tr>
<tr><td>

```xml
<apparel>
  <!-- Apparel override settings here -->
</apparel>
```
</td><td>
Default value: (None)<br /><br />

Sets apparel texture overrides and fallbacks. See [[Apparel Graphics|Apparel-Graphics]] for more details.
</td></tr>
<tr><td>

```xml
<skinShader>CutoutSkin</skinShader>
```
</td><td>
Default value: <code>CutoutSkin</code><br /><br />

Overrides the default <code>ShaderType</code> used for rendering pawns of your race. Defaults to <code>CutoutSkin</code>, which by default adds a reddish hue to shading. If this looks bad, then you can either change this to <code>Cutout</code> or change the <code>skinColor</code> below.
</td></tr>
<tr><td>

```xml
<skinColor>(1,0,0,1)</skinColor>
```
</td><td>
Default value: <code>(1,0,0,1)</code><br /><br />

Overrides the default color used by <code>CutoutSkin</code> for pawns of your race.
</td></tr>
</tbody>
</table>

## RimWorld v1.4

As of RimWorld v1.4, GraphicPaths is no longer a list as lifeStage-based overrides are now done via [[Extension Graphics|Extension-Graphics]] instead of via list entries. Extension Graphics can be used in all fields that were previously simple paths.