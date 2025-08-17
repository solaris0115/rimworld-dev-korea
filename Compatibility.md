These settings do not directly affect any vanilla game mechanics. Instead, they are used by other
mods for alien race compatibility. You do not need to provide compatibility flags if your race
does not differ from humans in any of these ways; the human defaults will be used for any
omitted fields.

**For C# modders**: These fields are private and are hidden behind virtual properties,
so you could make your own subclass of the Compatibility settings and override them.
Each of these fields also has a Pawn method variant that takes a Pawn as an argument,
that you can also override in case you need more logic to determine if the pawn actually
qualifies for the given flag.

Compatibility flags should be defined inside the <code>alienRace</code> tag of your <code>ThingDef.ThingDef_AlienRace</code>

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <compatibility>
      <!-- Compatibility flags go here -->
    </compatibility>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

## Compatibility Flags

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Human Default</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<isFlesh>true</isFlesh>
```
</td><td>
<code>true</code>
</td><td>
Should be true if your race has organic flesh.
</td></tr>
<tr><td>

```xml
<isSentient>true</isSentient> 
```
</td><td>
<code>true</code>
</td><td>
Should be true if your race is sentient and possesses free will.
</td></tr>
<tr><td>

```xml
<hasBlood>true</hasBlood>
```
</td><td>
<code>true</code>
</td><td>
Should be true if your race has organic blood.
</td></tr>
</tbody>
</table>
