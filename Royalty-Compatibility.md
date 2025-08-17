The following are options and features for compatibility with the [Royalty DLC](https://store.steampowered.com/app/1149640/RimWorld__Royalty/).

## Races

If your race does not use the vanilla ```Brain``` BodyPartDef, then psylink neuroformers will not be usable on your race as they specifically target the Brain. Note that bestowing ceremonies and anima trees use ```hediffSet.GetBrain()``` which targets your pawns' ```ConsciousnessSource``` which will still work so long as you have an analogue organ.

## PawnKinds

Royalty can generate Guests and Mercenaries as part of quests. If you do not patch in explicit support (or use a mod such as Real Faction Guests), then this can result in humans with alien gear.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Patch>
  <Operation Class="PatchOperationFindMod">
    <mods>
      <li>Royalty</li>
    </mods>
    <match Class="PatchOperationSequence">
      <operations>
        <!-- Guests -->
        <li Class="PatchOperationAdd">
          <xpath>Defs/QuestScriptDef/root[@Class="QuestNode_Sequence"]/nodes/li[@Class="QuestNode_IsSet"]/node[@Class="QuestNode_GetRandomPawnKindForFaction"]/choices</xpath>
          <value>
            <li>
              <factionDef>MyRace_CustomFactionDefName</factionDef>
              <pawnKinds>
                <li>MyRace_FirstGuestPawnKind</li>
                <li>MyRace_SecondGuestPawnKind</li>
              </pawnKinds>
            </li>  
          </value>
        </li>
        <!-- Mercenaries -->
        <li Class="PatchOperationAdd">
          <xpath>/Defs/QuestScriptDef/root[@Class="QuestNode_Sequence"]/nodes/li[@Class="QuestNode_GetRandomPawnKindForFaction"]/choices</xpath>
          <value>
            <li>
              <factionDef>MyRace_CustomFactionDefName</factionDef>
              <pawnKinds>
                <li>MyRace_FirstMercPawnKind</li>
                <li>MyRace_SecondMercPawnKind</li>
                <li>MyRace_ThirdMercPawnKind</li>
              </pawnKinds>
            </li>  
          </value>
        </li>
      </operations>
    </match>
  </Operation>
</Patch>
```
Note that this example is using ```PatchOperationFindMod``` and ```PatchOperationSequence```; if you have other Royalty compatibility content, you may wish to use LoadFolders.xml instead. See [RimWorld Wiki](https://rimworldwiki.com/wiki/Modding_Tutorials/Mod_folder_structure) for more details.

## Factions and Cultures

Royalty's Empire faction is set to be a permanent enemy to all factions except vanilla player factions. Custom player factions will need to be patched into the Empire faction's exception list in order to be able to become friendly with the Empire and be eligible for titles:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Patch>
  <Operation Class="PatchOperationAdd">
    <xpath>Defs/FactionDef[defName="Empire"]/permanentEnemyToEveryoneExcept</xpath>
    <value>
      <li>MyRace_CustomFactionDefName</li>
    </value>
  </Operation>
</Patch>
```

If you are not using LoadFolders.xml, then you should also use a ```PatchOperationFindMod``` (see [RimWorld Wiki](https://rimworldwiki.com/wiki/Modding_Tutorials/PatchOperations#PatchOperationFindMod) for more details) to make it conditional on Royalty being loaded:

```xml
<Operation Class="PatchOperationFindMod">
  <mods>
    <li>Royalty</li>
  </mods>
  <match Class="PatchOperationAdd">
    <xpath>Defs/FactionDef[defName="Empire"]/permanentEnemyToEveryoneExcept</xpath>
    <value>
      <li>MyRace_CustomFactionDefName</li>
    </value>
  </match>
</Operation>
```

