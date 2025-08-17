StyleSettings are used to customize or disable hair styles, beards, or tattoos for your race. This replaces <code>hairSettings</code> for RimWorld 1.2 and earlier.

StyleSettings are used by adding a <code>styleSettings</code> tag inside of <code>alienRace</code>.

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <styleSettings>
      <!-- Style settings are listed here -->
    </styleSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

StyleSettings can have an entry for each non-abstract <code>StyleItemDef</code> subclass. In vanilla RimWorld, this includes <code>HairDef</code>, <code>BeardDef</code>, and <code>TattooDef</code> as follows:

```xml
<styleSettings>
  <li>
    <key>HairDef</key>
    <value>
      <!-- options for HairDef usage -->
    </value>
  </li>
  <li>
    <key>BeardDef</key>
    <value>
      <!-- options for BeardDef usage -->
    </value>
  </li>
  <li>
    <key>TattooDef</key>
    <value>
      <!-- options for TattooDef usage -->
    </value>
  </li>
</styleSettings>
```

These are all optional; ones that are omitted will allow all style items for that Def (as humans).

## Settings

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<hasStyle>true</hasStyle>
```
</td><td>
<code>true</code>
</td><td>
If set to false, disables the associated StyleItemDef for this race. Note that this is <em>not</em> the same as having Bald hair or NoBeard beards, this disables that entire system from your race.
</td></tr>
<tr><td>

```xml
<genderRespected>true</genderRespected>
```
</td><td>
<code>true</code>
</td><td>
<strong>RimWorld 1.4 and later only.</strong><br/><br/>

If set to false, members of your race will ignore gender tags for this style item.
</td></tr>
<tr><td>

```xml
<styleTags>
  <li>Urban</li>
  <li>Royal</li>
</styleTags>
```
</td><td>
(None)
</td><td>
If set, restricts the desired style variations for your race to the specified style tags. These are associated with <code>StyleItemCategoryDef</code> entries (under <code>Defs/Misc/HairDefs/StyleItemCategoryDefs.xml</code> in Core).
</td></tr>
<tr><td>

```xml
<styleTagsOverride>
  <li>Urban</li>
  <li>Royal</li>
</styleTagsOverride>
```
</td><td>
(None)
</td><td>
If set, restricts the desired style variations for your race to the specified style tags.<br /><br />

If overrides are used, then these are applied in a destructive prefix and the vanilla <code>WantsToUseStyle</code> code is not run.
</td></tr>
<tr><td>

```xml
<bannedTags>
  <li>Punk</li>
</bannedTags>
```
</td><td>
(None)
</td><td>
<strong>RimWorld 1.4 and later only.</strong><br/><br/>

If set, disallows the specified style tags for your race.
</td></tr>
<tr><td>

```xml
<shader>Transparent</shader>
```
</td><td>
(Varies)
</td><td>
Overrides the shader type used to draw this style item. For hair and beards, the default shader is <code>Transparent</code>. For tattos, the default shader is <code>CutoutSkinOverlay</code>.
</td></tr>

</tbody>
</table>
