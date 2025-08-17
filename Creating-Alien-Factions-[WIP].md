**WARNING:** At time of writing, this page is 6 years old and unmaintained. If you managed to find your way here, please be wary of any information you find here, as it is likely obsolete and will eventually be replaced with a tutorial on the main RimWorld Wiki.

Instead of only having your aliens turn up randomly in character generation & as refugees/slaves, you can create alien exclusive factions with vanilla xml. In this tutorial I'll be using `PlayerAlienColony` for the defname of our custom player faction. Under `<PawnKindDef>` add:
```xml
<defaultFactionType>PlayerAlienColony</defaultFactionType>
```

### Player Faction Defs
Lets start writing up our own faction:
```xml
<FactionDef ParentName="PlayerFactionBase">
    <defName>PlayerAlienColony</defName>
    <label>Example Aliens</label>
    <description>Your community of your own alien race.</description>
    <isPlayer>true</isPlayer>
    <basicMemberKind>Alien</basicMemberKind>
    <pawnsPlural>aliens</pawnsPlural>
```
Next up is `<factionBaseNameMaker>NamerFactionBasePlayerColony</factionBaseNameMaker>` The default variable pulls from a name list for player factions. here are all the vanilla variables for this field:
```
NamerFactionBasePlayerColony
NamerFactionOutlander
NamerFactionPirate
NamerFactionTribal
NamerFactionSpacer
```
We will cover making custom name lists later on in this tutorial.
Alternatively you could choose to have a fixed name with `<fixedName></fixedName>`. Lets choose this option
```xml
<fixedName>Alien Colony</fixedName>
```
Next is tech level. Affects how slowly you research tech from a higher tier than your own. Here are all the vanilla variables for `<techLevel>`:
```
Undefined
Animal
Neolithic
Medieval
Industrial
Spacer
Ultra
Transcendent
```
I'm going to set our aliens to neolithic.
```xml
<techLevel>neolithic</techLevel>
```
Following this is backstory category. *Note: This will be overwritten by `<backstoryCategory>` under `<AlienRace.ThingDef_AlienRace>`.* For our example we will code this:
```xml
<backstoryCategory>ExampleAlienBackstory</backstoryCategory>
```
However here is the list of vanilla variables:
```
Civil
Raider
Slave
Tribal
```
`<pawnNameMaker>` works essentially the same as `<factionBaseNameMaker>`. Unlike the latter it is non-essential, and without it the game will just choose from the default name list. There is only one vanilla variable:
```xml
<pawnNameMaker>NamerPersonTribal</pawnNameMaker>
```
Next part we will leave alone for now. These choose the icons for the faction on the overworld/planetary map. Feel free to replace them if you have another icon/image in mind.
```xml
<expandingIconTexture>World/WorldObjects/Expanding/Town</expandingIconTexture>
<homeIconPath>World/WorldObjects/TribalFactionBase</homeIconPath>
```
Starting research defines designates what researches you start off with (e.g. neolithic tribes have to research *complex clothing* but start with *pemmican*). It comes in two variables: `ClassicStart` and `TribalStart`.
```xml
<startingResearchTags>
<li>TribalStart</li>
</startingResearchTags>
```
Hair tags define what hair set the faction uses. *Note: You can create your own custom hair set with hair defs, which are under misc. in the rimworld defs core.* Here is the list of vanilla variables:
```Punk
Rural
Tribal
Urban
```
You can also include multiple hair lists, for more variety.
```xml
<hairTags>
<li>Tribal</li>
<li>Urban</li>
</hairTags>
```
`<apparelStuffFilter>` is what material the factions clothes tend to be made out of. Here is a list:
```xml    
<apparelStuffFilter>
<thingDefs>
<li>Cloth</li>
<li>Synthread</li>
<li>DevilstrandCloth</li>
<li>Hyperweave</li>
</thingDefs>
</apparelStuffFilter>
```
Now we've finished! Let have a look at our code in full.
```xml
<FactionDef ParentName="PlayerFactionBase">
    <defName>PlayerAlienColony</defName>
    <label>Example Aliens</label>
    <description>Your community of your own alien race.</description>
    <isPlayer>true</isPlayer>
    <basicMemberKind>Alien</basicMemberKind>
    <pawnsPlural>aliens</pawnsPlural>
<fixedName>Alien Colony</fixedName>
<techLevel>neolithic</techLevel>
<backstoryCategory>ExampleAlienBackstory</backstoryCategory>
<pawnNameMaker>NamerPersonTribal</pawnNameMaker>
<expandingIconTexture>World/WorldObjects/Expanding/Town</expandingIconTexture>
<homeIconPath>World/WorldObjects/TribalFactionBase</homeIconPath>
<startingResearchTags>
<li>TribalStart</li>
</startingResearchTags>
<hairTags>
<li>Tribal</li>
<li>Urban</li>
</hairTags>
<apparelStuffFilter>
<thingDefs>
<li>Cloth</li>
<li>Synthread</li>
<li>DevilstrandCloth</li>
<li>Hyperweave</li>
</thingDefs>
</apparelStuffFilter>
</FactionDef>
```

### Scenarios
To be able to play our custom faction, we need a scenario to select them with. Thankfully Scenarios can be both edited in game as well as xml. When you start a new game: click on the scenario editor button, enable edit mode and then set the `player faction` section to your custom faction. Scenarios will also allow you to choose what research your faction starts off with, and can ban certain researches all together. You can also disable activities like hunting or harvesting, forcing your race to depend only on agriculture or hunting.


***

### NPC Faction Defs
What if you want your aliens to be NPCs, that can raid or trade with your colony. Here is an example vanilla faction:
```xml
  <FactionDef>
		<defName>Outlander</defName>
		<label>outlander union</label>
    <description>These people have lived here for decades or centuries, and have lost most of the technology that brought them to this world. They usually work with simple mechanical tools and defend themselves with advanced gunpowder weapons.\n\nThey are concerned with the practical matters of trade, trust, and survival.</description>
    <pawnsPlural>outlanders</pawnsPlural>
    <factionBaseSelectionWeight>1</factionBaseSelectionWeight>
    <requiredCountAtGameStart>1</requiredCountAtGameStart>
    <canMakeRandomly>true</canMakeRandomly>
    <raidCommonality>100</raidCommonality>
    <canSiege>true</canSiege>
    <canStageAttacks>true</canStageAttacks>
    <leaderTitle>mayor</leaderTitle>
    <expandingIconTexture>World/WorldObjects/Expanding/Town</expandingIconTexture>
    <colorSpectrum>
      <li>(0.64, 0.42, 0.36)</li>
      <li>(0.47, 0.5, 0.91)</li>
    </colorSpectrum>
    <startingGoodwill>
      <min>10</min>
      <max>40</max>
    </startingGoodwill>
		<factionNameMaker>NamerFactionOutlander</factionNameMaker>
		<factionBaseNameMaker>NamerFactionBaseOutlander</factionBaseNameMaker>
		<techLevel>Industrial</techLevel>
		<backstoryCategory>Civil</backstoryCategory>
		<hairTags>
			<li>Rural</li>
		</hairTags>
    <naturalColonyGoodwill>
      <min>-60</min>
      <max>0</max>
    </naturalColonyGoodwill>
    <caravanTraderKinds>
      <li>Caravan_Outlander_BulkGoods</li>
      <li>Caravan_Outlander_CombatSupplier</li>
      <li>Caravan_Outlander_Exotic</li>
      <li>Caravan_Outlander_PirateMerchant</li>
    </caravanTraderKinds>
    <visitorTraderKinds>
      <li>Visitor_Outlander_Standard</li>
    </visitorTraderKinds>
    <factionBaseTraderKinds>
      <li>FactionBase_Outlander_Standard</li>
    </factionBaseTraderKinds>
    <allowedArrivalTemperatureRange>
      <min>-40</min>
      <max>45</max>
    </allowedArrivalTemperatureRange>
    <pawnGroupMakers>
      <li>
        <kindDef>Normal</kindDef>
        <options>
          <Villager>50</Villager>
          <TownGuard>250</TownGuard>
          <TownCouncilman>250</TownCouncilman>
          <GrenadierDestructive>50</GrenadierDestructive>
          <MercenaryGunner>100</MercenaryGunner>
          <MercenarySlasher>100</MercenarySlasher>
        </options>
      </li>
      <li>
        <kindDef>Trader</kindDef>
        <traders>
          <TownTrader>1</TownTrader>
        </traders>
        <carriers>
          <Muffalo>1</Muffalo>
          <Dromedary>1</Dromedary>
        </carriers>
        <guards>
          <TownGuard>250</TownGuard>
          <GrenadierDestructive>50</GrenadierDestructive>
          <MercenaryGunner>100</MercenaryGunner>
          <MercenarySlasher>100</MercenarySlasher>
        </guards>
      </li>
      <li>
        <kindDef>FactionBase</kindDef>
        <options>
          <Villager>50</Villager>
          <TownGuard>250</TownGuard>
          <TownCouncilman>250</TownCouncilman>
          <GrenadierDestructive>50</GrenadierDestructive>
          <MercenaryGunner>100</MercenaryGunner>
          <MercenarySlasher>100</MercenarySlasher>
        </options>
      </li>
    </pawnGroupMakers>
    <homeIconPath>World/WorldObjects/DefaultFactionBase</homeIconPath>
  </FactionDef>
```
As you can see it shares a lot in common with the player based factions, but has some completely new areas.
**\[WIP\]**


### Custom Name Makers Defs
Create custom name lists for your pawns and factions.
**\[TBA\]**