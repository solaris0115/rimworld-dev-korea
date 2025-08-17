Thought Settings are used to restrict or alter Thoughts received by a race. This is most often used to prevent or
invert thoughts from situations and events that your race would react to differently from humans.

Thought Settings should be defined inside the <code>alienRace</code> tag of your <code>ThingDef.ThingDef_AlienRace</code>

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <thoughtSettings>
      <!-- Thought settings go here -->
    </thoughtSettings>
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
<replacerList>
  <li>
    <original>AttendedParty</original>
    <replacer>AlienAttendedParty</replacer> 
  </li>
  <li>
    <original>AteWithoutTable</original>
    <replacer>AlienHatesTables</replacer> 
  </li>
</replacerList>
```
</td><td>
Used to replace a specific <code>ThoughtDef</code> with another when applied to your race.<br/><br/>
A separate list item (<code>li</code>) should be used for each ThoughtDef you want to override.
</td></tr>
<tr><td>

```xml
<cannotReceiveThoughts>
  <li>SleptOnGround</li>
  <li>SoakingWet</li>
</cannotReceiveThoughts>
```
</td><td>
Used to complete negate specific <code>ThoughtDef</code> types from being received by your race.<br/><br/>
A separate list item (<code>li</code>) should be used for each ThoughtDef you want to negate.
</td></tr>
<tr><td>

```xml
<restrictedThoughts>
  <li>AlienPain</li>
  <li>AlienEnvironmentThought</li>
</restrictedThoughts>
```
</td><td>
Used to specify thoughts that should only apply to your race.<br/><br/>
A separate list item (<code>li</code>) should be used for each ThoughtDef you want to restrict.
</td></tr>
<tr><td>

```xml
<canStillReceiveThoughts>
  <li>Pain</li>
  <li>AteWithoutTable</li>
</canStillReceiveThoughts>
```
</td><td>
Used to specify thoughts that your race can use regardless of restrictions.<br/><br/>
A separate list item (<code>li</code>) should be used for each ThoughtDef you want to whitelist.
</td></tr>
<tr><td>

```xml
<cannotReceiveThoughtsAtAll>true</cannotReceiveThoughtsAtAll>
```
</td><td>
Stops your race from receiving any thoughts except for those whitelisted in <code>canStillReceiveThoughts</code>.
</td></tr>
</tbody>
</table>


## Specific Settings

The following settings have default values as shown, and should only be added if you want to
override said defaults. Note that "humanlikes" in RimWorld refer to
any race with Humanlike intelligence, which includes Humans as well as the vast majority of races
made with Humanoid Alien Races.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<ateThoughtGeneral>
  <thought>AteHumanlikeMeatDirect</thought>
  <ingredientThought>AteHumanlikeMeatAsIngredient</ingredientThought>
</ateThoughtGeneral>
```
</td><td>
Determines the thoughts received your race when eating humanlike meat. The thoughts are separated
by whether the meat is eaten directly as opposed to when it's eaten as an ingredient in a meal.
</td></tr>
<tr><td>

```xml
<butcherThoughtGeneral>
  <thought>ButcheredHumanlikeCorpse</thought>
  <knowThought>KnowButcheredHumanlikeCorpse</knowThought>
</butcherThoughtGeneral>
```
</td><td>
Determines the thoughts received by your race when butchering the corpse of a humanlike race.
The knowThought is received by members of your colony who didn't directly participate in the
butchering action.
</td></tr>
<tr><td>

```xml
<butcherThoughtSpecific>
  <li>
    <raceList>
      <li>Human</li>
    </raceList>
    <thought>ButcheredHuman</thought>
    <knowThought>KnowButcheredHuman</knowThought>
  </li>
</butcherThoughtSpecific>
<ateThoughtSpecific>
  <li>
    <raceList>
      <li>Human</li>
    </raceList>
    <thought>AteHumanlikeMeatDirect</thought>
    <ingredientThought>AteHumanIngredient</ingredientThought>
  </li>
</ateThoughtSpecific>
```
</td><td>
Specific tags can be used if you want different thoughts for butchering or consuming specific
races. This is often used to change thoughts towards butchering and eating one's own race as
opposed to others, such as a race that is only bothered by eating their own but doesn't mind
eating other humanlike races.
</td></tr>
</tbody>
</table>
