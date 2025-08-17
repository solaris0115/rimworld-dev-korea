Relation Settings are used to alter the names or generation commonality of specific PawnRelations between members of your race.

Relation Settings should be defined inside the <code>alienRace</code> tag of your <code>ThingDef.ThingDef_AlienRace</code>

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <relationSettings>
      <!-- Relation settings go here -->
    </relationSettings>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

## General Settings

All of these settings are optional unless otherwise specified.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<relationChanceModifierLover>1</relationChanceModifierLover>
<relationChanceModifierExLover>1</relationChanceModifierExLover>

<relationChanceModifierFiance>1</relationChanceModifierFiance>
<relationChanceModifierSpouse>1</relationChanceModifierSpouse>
<relationChanceModifierExSpouse>1</relationChanceModifierExSpouse>

<relationChanceModifierParent>1</relationChanceModifierParent>
<relationChanceModifierChild>1</relationChanceModifierChild>
<relationChanceModifierSibling>1</relationChanceModifierSibling>
```
</td><td>
These are the eight basic PawnRelationDefs that are used for randomly generated relationships.
All values default to 1 and any override provided here will be multiplied by the PawnRelationDef's
base <code>generationChanceFactor</code>. For example, using 2.0 will cause that relationship
to generate twice as often as it does for humans, and using 0 will cause it to never randomly
generate.
</td></tr>
<tr><td>

```xml
<renamer>
   <li>
      <relation>Parent</relation>
      <label>Patron</label>
      <femaleLabel>Matron</femaleLabel>
   </li>
</renamer>
```
</td><td>
This can be used to rename vanilla relationships when shown for members of your race. 
</td></tr>
</tbody>
</table>
