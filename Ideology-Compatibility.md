The following are options and features for compatibility with the [Ideology DLC](https://store.steampowered.com/app/1392840/RimWorld__Ideology/).

## Races

No special compatibility is required at a race level for Ideology.

## PawnKinds

No special compatibility is required at a PawnKind level for Ideology.

## Factions and Cultures

NPC factions can be customized with required or disallowed memes and precepts:

```xml
<FactionDef>
  <defName>MyCustomFaction</defName>

  <!-- ideoligion customization fields go here -->

</FactionDef>
```

Note that all references to MemeDefs and PreceptDefs should use MayRequire, otherwise they will generate reference errors if the player does not have Ideology loaded:

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<requiredMemes>
  <li MayRequire="Ludeon.RimWorld.Ideology">Individualist</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">Loyalist</li>
</requiredMemes>
```
</td><td>
(Optional) Sets memes that are required for this faction.
</td></tr>
<tr><td>

```xml
<allowedMemes>
  <li MayRequire="Ludeon.RimWorld.Ideology">Transhumanist</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">Proselytizer</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">HumanPrimacy</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">NaturePrimacy</li>
</allowedMemes>
```
</td><td>
(Optional) If set, then only memes on this list can be randomly selected. Note that <code>requiredMemes</code> will bypass this list, so they do not have to be duplicated across both lists.
</td></tr>
<tr><td>

```xml
<disallowedMemes>
  <li MayRequire="Ludeon.RimWorld.Ideology">Supremacist</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">PainIsVirtue</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">Nudism</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">Raider</li>
</disallowedMemes>
```
</td><td>
(Optional) Sets memes that should not be used for this faction. Note that this list overrides both <code>requiredMemes</code> and <code>allowedMemes</code>; if you specify a meme here and in one of those two lists, then it will still be excluded.
</td></tr>
<tr><td>

```xml
<disallowedPrecepts>
  <li MayRequire="Ludeon.RimWorld.Ideology">ApparelDesired_Strong_Subordinate</li>
  <li MayRequire="Ludeon.RimWorld.Ideology">ApparelDesired_Soft_Subordinate</li>
</disallowedPrecepts>
```
</td><td>
(Optional) Sets precepts that should not be used for this faction.
</td></tr>
<tr><td>

```xml
<structureMemeWeights>
  <Structure_Animist MayRequire="Ludeon.RimWorld.Ideology">4</Structure_Animist>
  <Structure_TheistEmbodied MayRequire="Ludeon.RimWorld.Ideology">1</Structure_TheistEmbodied>
  <Structure_TheistAbstract MayRequire="Ludeon.RimWorld.Ideology">1</Structure_TheistAbstract>
  <Structure_Archist MayRequire="Ludeon.RimWorld.Ideology">1</Structure_Archist>
</structureMemeWeights>
```
</td><td>
(Optional) If set, only allows the specified structure memes and sets the relative weight of the structure meme. The given weight is multiplied into the MemeDef's <code>randomizationSelectionWeightFactor</code>, which defaults to <code>1.0</code>.
</td></tr>
</tbody>
</table>
