RaceSettings are an option used to enable various additional compatibility functions for mod compatibility.

RaceSettings is a custom Def type. All of the following settings must be placed inside an ```AlienRace.RaceSettings``` Def object.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Defs>
  
  <AlienRace.RaceSettings>
    <defName>MyRace_RaceSettings</defName>
    
    <!-- options placed here -->
    
  </AlienRace.RaceSettings>

</Defs>
```

As with all Def types, your ```defName``` must be globally unique across all mod content, thus it is strongly recommended that you use a unique prefix to prevent mod collisions.

## PawnKind Settings

All of the following settings must be placed inside a ```pawnKindSettings``` tag inside of your RaceSettings Def:

```xml
<AlienRace.RaceSettings>
  <defName>MyRace_RaceSettings</defName>

  <pawnKindSettings>
    <!-- options placed here -->
  </pawnKindSettings>

</AlienRace.RaceSettings>
```

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>

<tr><td>

```xml
<startingColonists>
  <li>
    <pawnKindEntries>
      <li>
        <kindDefs>
          <li>MyRace_ColonistPawnKind</li>
        </kindDefs>
        <chance>100.0</chance>
      </li>
    </pawnKindEntries>
    <factionDefs>
      <li>PlayerColony</li> 
    </factionDefs>
  </li>
</startingColonists>
```
</td><td>
(Optional) Allows your race to be randomly generated as starting members for the specified
player FactionDef. Generally used to add your race to vanilla scenarios or scenarios from other
mods; if you only want your race to spawn as part of your NPC factions or your own custom
starting scenarios, then this is unnecessary.

Chance is a weight value, with the default value for that FactionDef being <code>100</code>.

```PlayerColony``` is the vanilla FactionDef used for Crashlanded, Rich Explorer,
and Naked Brutality. Lost Tribe uses ```PlayerTribe```.
</td></tr>
<tr><td>

```xml
<alienwandererkinds>
  <li>
    <pawnKindEntries>
      <li>
        <kindDefs>
          <li>ExampleAlienKind</li>
        </kindDefs>
        <chance>100.0</chance>
      </li>
    </pawnKindEntries>
    <factionDefs>
      <li>PlayerColony</li> 
    </factionDefs>
  </li>
</alienwandererkinds>
```
</td><td>
(Optional) Allows your race to be randomly generated in Wanderer Joins events
for the specified player FactionDef.

Formatting is otherwise the same as for <code>startingColonists</code> above.
</td></tr>
<tr><td>

```xml
<alienslavekinds>
  <li>
    <kindDefs>
      <li>MyRace_SlavePawnKind</li>
    </kindDefs>
    <chance>100.0</chance>
  </li>
</alienslavekinds>
```
</td><td>
(Optional) Allows your race to spawn as slaves in NPC faction caravans and settlements.

Chance is a weight value, with vanilla human slaves being <code>100</code>, thus having
a <code>chance</code> of <code>100</code> here will make the specified PawnKind(s)
the same commonality as vanilla human slaves.
</td></tr>
<tr><td>

```xml
<alienrefugeekinds>
  <li>
    <kindDefs>
      <li>MyRace_RefugeePawnKind</li>
    </kindDefs>
    <chance>100.0</chance>
  </li>
</alienrefugeekinds>
```
</td><td>
(Optional) Allows your race to spawn as refugees in quest events such as Space Refugee Pods.

Chance is a weight value, with vanilla human refugees being <code>100</code>, thus having
a <code>chance</code> of <code>100</code> here will make the specified PawnKind(s)
the same commonality as vanilla human refugees.
</td></tr>

</tbody>
</table>

## Universal BodyAddons

RaceSettings can be used to create BodyAddons that are attached to all humanlike races:

```xml
<AlienRace.RaceSettings>
  <defName>MyRace_RaceSettings</defName>

  <universalBodyAddons>
    <!-- options placed here -->
  </universalBodyAddons>

</AlienRace.RaceSettings>
```

This can be used to share BodyAddons between multiple races via Extension Graphics
and otherwise works identically to normal BodyAddons.

Please see the [[BodyAddons|Body-Addons]] page for more details.

## Backstory Tag Insertion

**(RimWorld v1.3 and earlier only)**: This feature was obsoleted by the vanilla game's migration
of backstories to ```BackstoryDef```s and is no longer available or necessary in RimWorld 1.4.
If you want to add custom ```spawnCategories``` to external backstories, you can use a regular
[PatchOperation](https://rimworldwiki.com/wiki/Modding_Tutorials/PatchOperations).

```xml
<AlienRace.RaceSettings>
  <defName>MyRace_RaceSettings</defName>
  
  <backstoryTagInsertion>
    <li>
      <backstories>
        <li>SpecificBackstoryName</li>
        <li>AnotherBackstoryName</li>
      </backstories>
      <spawnCategories>
        <li>MyRace_CustomSpawnCategory</li>
      </spawnCategories>
    </li>
  </backstoryTagInsertion>
  
</AlienRace.RaceSettings>
```