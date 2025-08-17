PawnBioDefs can be used to create specific pre-made characters for your race,
similar to the "backer pawns" in vanilla RimWorld.

Individual characters are created using <code>AlienRace.PawnBioDef</code> Defs:

```xml
<AlienRace.PawnBioDef>
  <!-- pawn bio fields go here -->
</AlienRace.PawnBioDef>
```

## PawnBioDef Fields

<table>
<thead>
<tr><th align="left">Field</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<defName>MyRace_MyPawnBio</defName>
```
</td>
<td>
(Required) As with all Def types, a <code>defName</code> is required and must be globally
unique across all mods. However, this is not saved or referenced in any way by code and
is completely arbitrary for PawnBioDefs.
</td></tr>
<tr><td>

```xml
<childhood>MyRace_SpecificChildBackstory</childhood>
<adulthood>MyRace_SpecificAdultBackstory</adulthood>
```
</td>
<td>
(Required) Specifies the backstories that should be used for this character.
</td></tr>
<tr><td>

```xml
<gender>Male</gender>
```
</td>
<td>
(Optional, default: <code>Either</code>) Specifies a gender for this character.
Available values are: <code>Either</code> (default), <code>Male</code>, <code>Female</code>
</td></tr>
<tr><td>

```xml
<name>
  <first>John</first>
  <nick>Boogeyman</nick>
  <last>Wick</last>
</name>
```
</td>
<td>
(Required) Sets the name for this character.
</td></tr>
<tr><td>

```xml
<validRaces>
  <li>Human</li>
  <li>MyRaceDefName</li>
</validRaces>
```
</td>
<td>
(Required) Sets the race(s) that this character can spawn as.
</td></tr>
<tr><td>

```xml
<factionLeader>true</factionLeader>
```
</td>
<td>
(Optional) If set to <code>true</code>, then this character can only spawn
as a faction leader and has higher priority for use as a faction leader.
</td></tr>
<tr><td>

```xml
<forcedHediffs>
  <li>Malnutrition</li>
</forcedHediffs>
```
</td>
<td>
(Optional) Sets HediffDefs that this character should spawn with.
</td></tr>
<tr><td>

```xml
<forcedItems>
  <Gun_Autopistol>1</Gun_Autopistol>
</forcedItems>
```
</td>
<td>
(Optional) Adds items to this character's inventory when spawned.
Similar to <code>forcedItems</code> on backstories, will bypass possessions limits
and will be directly stored in the pawn's inventory rather than placed on the ground.
</td></tr>
</tbody>
</table>

## Complete Samples

```xml
<AlienRace.PawnBioDef>
  <defName>MyRace_NanomachinesSon</defName>
  <childhood>MyRace_FootballPlayer</childhood>
  <adulthood>MyRace_StateSenator</adulthood>
  <gender>Male</gender>
  <name>
    <first>Steven</first>
    <nick>Senator</nick>
    <last>Armstrong</last>
  </name>
  <validRaces>
    <li>MyRaceDefName</li>
  </validRaces>
  <factionLeader>true</factionLeader>
  <forcedHediffs>
    <li>LuciferiumHigh</li>
  </forcedHediffs>
</AlienRace.PawnBioDef>
```

```xml
<AlienRace.PawnBioDef>
  <defName>Custom_BabaYaga</defName>
  <childhood>Custom_OrphanRecruit</childhood>
  <adulthood>Custom_LegendaryHitman</adulthood>
  <gender>Male</gender>
  <name>
    <first>John</first>
    <nick>Boogeyman</nick>
    <last>Wick</last>
  </name>
  <validRaces>
    <li>Human</li>
  </validRaces>
  <forcedItems>
    <Gun_Autopistol>1</Gun_Autopistol>
  </forcedItems>
</AlienRace.PawnBioDef>
```
