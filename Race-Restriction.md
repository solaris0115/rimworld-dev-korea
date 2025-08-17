Race Restrictions can be used to allow or prevent the usage of various game mechanics by your race, such as research projects, apparel, weapons, and more.

Race Restrictions can be added by placing a <code>raceRestriction</code> tag inside of <code>alienRace</code>.

```xml
<AlienRace.ThingDef_AlienRace>
  <alienRace>
    <raceRestriction>
      <!-- race restrictions are listed here -->
    </raceRestriction>
  </alienRace>
</AlienRace.ThingDef_AlienRace>
```

Unless otherwise noted, all Race Restrictions are optional.

## Apparel

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<apparelList>
  <li>Apparel_YourRaceArmor</li>
</apparelList>
```
</td><td>
Sets apparel that only your race can wear.<br/><br/>
Note that multiple races can share restricted apparel; any race with apparel listed in their list can wear it.
</td></tr>
<tr><td>

```xml
<whiteApparelList>
  <li>Apparel_Duster</li>
  <li>Apparel_AlienRaceGear</li>
</whiteApparelList>
```
</td><td>
Sets apparel that your race can wear without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyUseRaceRestrictedApparel</code>
</td></tr>
<tr><td>

```xml
<blackApparelList>
    <li>Apparel_Tuque</li>
    <li>Apparel_Parka</li>
</blackApparelList>
```
</td><td>
Sets apparel that your race is not allowed to wear.
</td></tr>
<tr><td>

```xml
<onlyUseRaceRestrictedApparel>
  true
</onlyUseRaceRestrictedApparel>
```
</td><td>
If set to true, then your race can only wear apparel that is on your <code>apparelList</code>
or <code>whiteApparelList</code>.
</td></tr>
</tbody>
</table>

## Weapons

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<weaponList>
  <li>Weapon_AlienRaceGun</li>
</weaponList>
```
</td><td>
Sets weapons that only your race can equip.<br/><br/>
Note that multiple races can share restricted weapons; any race with weapons listed in their list can equip it.
</td></tr>
<tr><td>

```xml
<whiteWeaponList>
  <li>MeleeWeapon_BreachAxe</li>
  <li>CustomAlienWeapon</li>
</whiteWeaponList>
```
</td><td>
Sets weapons that your race can equip without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyUseRaceRestrictedWeapons</code>
</td></tr>
<tr><td>

```xml
<blackWeaponList>
    <li>Gun_ChargeRifle</li>
    <li>MeleeWeapon_LongSword</li>
</blackWeaponList>
```
</td><td>
Sets weapons that your race is not allowed to equip.
</td></tr>
<tr><td>

```xml
<onlyUseRaceRestrictedWeapons>
  true
</onlyUseRaceRestrictedWeapons>
```
</td><td>
If set to true, then your race can only equip weapons in your <code>weaponList</code>
or <code>whiteWeaponList</code>.
</td></tr>
</tbody>
</table>

## Buildings

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<buildingList>
  <li>Building_AlienBuilding</li>
</buildingList>
```
</td><td>
Sets buildings that only your race can construct.<br/><br/>
Buildings restricted by a race will not be shown in the Architect Menu unless a member of that race
is in the player's colony. This list is cached and may take 2-3 in-game hours to show up
after a member of such a race joins the colony. 
</td></tr>
<tr><td>

```xml
<whiteBuildingList>
  <li>SculptureSmall</li>
</whiteBuildingList>
```
</td><td>
Sets buildings that your race can construct without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyBuildRaceRestrictedBuildings</code>
</td></tr>
<tr><td>

```xml
<blackBuildingList>
    <li>SculptureGrand</li>
</blackBuildingList>
```
</td><td>
Sets buildings that your race is not allowed to construct.
</td></tr>
<tr><td>

```xml
<onlyBuildRaceRestrictedBuildings>
  true
</onlyBuildRaceRestrictedBuildings>
```
</td><td>
If set to true, then your race can only construct buildings from your <code>buildingList</code>
or <code>whiteBuildingList</code>.
</td></tr>
</tbody>
</table>

## Recipes

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<recipeList>
  <li>Refine_AlienMaterial</li>
</recipeList>
```
</td><td>
Sets recipes that only your race can work on.<br/><br/>
Note that any <code>RecipeDef</code> be specified, including surgery recipes.
</td></tr>
<tr><td>

```xml
<whiteRecipeList>
  <li>Make_StoneBlocksAny</li>
</whiteRecipeList>
```
</td><td>
Sets recipes that your race can work on without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyDoRaceRestrictedRecipes</code>
</td></tr>
<tr><td>

```xml
<blackRecipeList>
    <li>Make_Kibble</li>
</blackRecipeList>
```
</td><td>
Sets recipes that your race is not allowed to work on.
</td></tr>
<tr><td>

```xml
<onlyDoRaceRestrictedRecipes>
  true
</onlyDoRaceRestrictedRecipes>
```
</td><td>
If set to true, then your race can only work on recipes in your <code>recipeList</code>
or <code>whiteRecipeList</code>.
</td></tr>
</tbody>
</table>

## Plants

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<plantList>
  <li>Plant_AlienCrop</li>
</plantList>
```
</td><td>
Sets plants that only your race can sow or harvest.
</td></tr>
<tr><td>

```xml
<whitePlantList>
  <li>Plant_Potato</li>
</whitePlantList>
```
</td><td>
Sets plants that your race can sow or harvest without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyDoRaceRestrictedPlants</code>
</td></tr>
<tr><td>

```xml
<blackPlantList>
    <li>Plant_Smokeleaf</li>
</blackPlantList>
```
</td><td>
Sets plants that your race is not allowed to sow or harvest.
</td></tr>
<tr><td>

```xml
<onlyDoRaceRestrictedPlants>
  true
</onlyDoRaceRestrictedPlants>
```
</td><td>
If set to true, then your race can only sow or harvest plants in your <code>plantList</code>
or <code>whitePlantList</code>.
</td></tr>
</tbody>
</table>

## Traits

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<traitList>
  <li>Plant_AlienCrop</li>
</traitList>
```
</td><td>
Sets traits that only members of your race can generate with.
</td></tr>
<tr><td>

```xml
<whiteTraitList>
  <li>Plant_Potato</li>
</whiteTraitList>
```
</td><td>
Sets traits that members of your race can generate with without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyGetRaceRestrictedTraits</code>
</td></tr>
<tr><td>

```xml
<blackTraitList>
    <li>Plant_Smokeleaf</li>
</blackTraitList>
```
</td><td>
Sets traits that members of your race are not allowed to generate with.
</td></tr>
<tr><td>

```xml
<onlyGetRaceRestrictedTraits>
  true
</onlyGetRaceRestrictedTraits>
```
</td><td>
If set to true, then your race can only generate with traits in your <code>traitList</code>
or <code>whiteTraitList</code>.
</td></tr>
</tbody>
</table>

## Food

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<foodList>
  <li>MealAlienNutrientPack</li>
</foodList>
```
</td><td>
Sets food that only your race can eat.
</td></tr>
<tr><td>

```xml
<whiteFoodList>
  <li>MealLavish</li>
</whiteFoodList>
```
</td><td>
Sets food that your race can eat without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyEatRaceRestrictedFood</code>
</td></tr>
<tr><td>

```xml
<blackFoodList>
    <li>MealNutrientPaste</li>
</blackFoodList>
```
</td><td>
Sets food that your race is not allowed to eat.
</td></tr>
<tr><td>

```xml
<onlyEatRaceRestrictedFood>
  true
</onlyEatRaceRestrictedFood>
```
</td><td>
If set to true, then your race can only eat food in your <code>foodList</code>
or <code>whiteFoodList</code>.
</td></tr>
</tbody>
</table>

## Animals

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<petList>
  <li>MealAlienNutrientPack</li>
</petList>
```
</td><td>
Sets animals that only your race can tame.
</td></tr>
<tr><td>

```xml
<whitePetList>
  <li>MealLavish</li>
</whitePetList>
```
</td><td>
Sets animals that your race can tame without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyTameRaceRestrictedPets</code>
</td></tr>
<tr><td>

```xml
<blackPetList>
    <li>MealNutrientPaste</li>
</blackPetList>
```
</td><td>
Sets animals that your race is not allowed to tame.
</td></tr>
<tr><td>

```xml
<onlyTameRaceRestrictedPets>
  true
</onlyTameRaceRestrictedPets>
```
</td><td>
If set to true, then your race can only tame animals in your <code>petList</code>
or <code>whitePetList</code>.
</td></tr>
</tbody>
</table>

## Xenotypes & Genes (Biotech DLC Only)

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<xenotypeList>
  <li>MyCustomXenotype</li>
  <li>AnotherXenotype</li>
</xenotypeList>
```
</td><td>
Sets xenotypes that only members of your race can have.
</td></tr>
<tr><td>

```xml
<whiteXenotypeList>
  <li>SharedXenotype</li>
  <li>AnotherSharedXenotype</li>
</whiteXenotypeList>
```
</td><td>
Sets xenotypes that your race can have without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyUseRaceRestrictedXenotypes</code>
</td></tr>
<tr><td>

```xml
<blackXenotypeList>
  <li>UnwantedXenotype</li>
  <li>IncompatibleXenotype</li>
</blackXenotypeList>
```
</td><td>
Sets xenotypes that your race cannot have.
</td></tr>
<tr><td>

```xml
<onlyUseRaceRestrictedXenotypes>
  true
</onlyUseRaceRestrictedXenotypes>
```
</td><td>
If set to true, then your race can only have xenotypes in your <code>xenotypeList</code>
or <code>whiteXenotypeList</code>.
</td></tr>
<tr><td>

```xml
<geneList>
  <li>MyCustomGene</li>
  <li>AnotherCustomGene</li>
</geneList>
```
</td><td>
Sets genes that only members of your race can have.
</td></tr>
<tr><td>

```xml
<whiteGeneList>
  <li>Hemogenic</li>
  <li>FacialRidges</li>
</whiteGeneList>
```
</td><td>
Sets genes that your race can have without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyHaveRaceRestrictedGenes</code>
</td></tr>
<tr><td>

```xml
<whiteGeneTags>
  <li>HairStyle</li>
  <li>BeardStyle</li>
  <li>Voice</li>
</whiteGeneTags>
```
</td><td>
Similar to <code>whiteGeneList</code>, but used to specify <code>exclusionTags</code>
instead of specific <code>GeneDef</code> entries.
</td></tr>
<tr><td>

```xml
<blackGeneList>
  <li>UnwantedGene</li>
  <li>AnotherUnwantedGene</li>
</blackGeneList>
```
</td><td>
Sets genes that your race cannot have.
</td></tr>
<tr><td>

```xml
<blackGeneTags>
  <li>Tail</li>
  <li>PsychicAbility</li>
</blackGeneTags>
```
</td><td>
Similar to <code>blackGeneList</code>, but used to specify <code>exclusionTags</code>
instead of specific <code>GeneDef</code> entries.
</td></tr>
<tr><td>

```xml
<blackEndoCategories>
  <li>HairColor</li>
  <li>BodyType</li>
</blackEndoCategories>
```
</td><td>
Sets endogene categories that your race cannot have.<br/><br/>
Valid options are: None, Melanin, HairColor, Ears, Nose, Jaw, Hands, Headbone, Head, BodyType, Voice
</td></tr>
<tr><td>

```xml
<onlyHaveRaceRestrictedGenes>
  true
</onlyHaveRaceRestrictedGenes>
```
</td><td>
If set to true, then your race can only have genes in your <code>geneList</code>
or <code>whiteGeneList</code>.
</td></tr>
</tbody>
</table>

## Reproduction (Biotech DLC Only)

Unless otherwise specified, all reproduction restrictions are from the perspective of the mother.

See also [[General Settings|General-Settings]] for additional reproduction and children-related settings.

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<reproductionList>
  <li>UniqueSubRace</li>
  <li>AnotherSubRace</li>
</reproductionList>
```
</td><td>
Sets races that only members of your race can reproduce with.
</td></tr>
<tr><td>

```xml
<whiteReproductionList>
  <li>AnotherRace</li>
  <li>YetAnotherRace</li>
</whiteReproductionList>
```
</td><td>
Sets races that your race can reproduce with without restricting it to only your race.<br/><br/>
Usually used in conjunction with <code>onlyReproduceWithRestrictedRaces</code>
</td></tr>
<tr><td>

```xml
<blackReproductionList>
  <li>UnwantedXenotype</li>
  <li>IncompatibleXenotype</li>
</blackReproductionList>
```
</td><td>
Sets races that your race cannot reproduce with.
</td></tr>
<tr><td>

```xml
<canReproduce>true</canReproduce>
```
</td><td>
If set to false, then your race cannot become pregnant.<br/><br/>
Generally used for races that do not give live birth but still have reproductive fertility,
such as those that lay eggs.<br/><br/>
Note: This was changed from <code>canGetPregnant</code> in an early dev version of HAR for RimWorld 1.4.
</td></tr>
<tr><td>

```xml
<canReproduceWithSelf>true</canReproduceWithSelf>
```
</td><td>
If set to false, then female members of your race cannot be impregnated by male members of your race.<br/><br/>
Can be used for races that can only crossbreed with other races.
</td></tr>
<tr><td>

```xml
<onlyReproduceWithRestrictedRaces>
  true
</onlyReproduceWithRestrictedRaces>
```
</td><td>
If set to false, then your race can only reproduce with races in your <code>reproductionList</code>
or <code>whiteReproductionList</code>.<br/><br/>
By default, all humanlike races can crossbreed.
</td></tr>
</tbody>
</table>

## Additional Settings

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<researchList>
  <li>
    <projects>
      <li>CustomResearchDef</li>
      <li>AnotherResearchDef</li>
    </projects>
  </li>
</researchList>
```
or
```xml
<researchList>
  <li>
    <projects>
      <li>RestrictedResearch</li>
    </projects>
    <apparelList>
       <li>Apparel_AlienGoggles</li>
       <li>Apparel_AlienLabCoat</li>
    </apparelList>
  </li>
</researchList>

```
</td><td>
Can be used to restrict research projects so that they can only be researched by your race.<br/><br/>
You can optionally set apparel that must be worn in order to research those projects, and separate list items
can be used to set different apparel requirements for different research projects.
</td></tr>
<tr><td>

```xml
<conceptList>
  <li>AlienRace_Abilities</li>
  <li>AlienRace_SpecialFood</li>
</conceptList>
```
</td><td>
Sets <code>ConceptDef</code> entries that are automatically triggered
when a member of your race joins the player's colony.<br/><br/>
These populate the Learning Helper in the top-right corner of the game UI
and can be used provide helpful information or tutorials for your race.
</td></tr>
<tr><td>

```xml
<workGiverList>
  <li>WorkGiver_AlienRaceWork</li>
  <li>WorkGiver_AlienRaceMaintenance</li>
</workGiverList>

```
</td><td>
Sets <code>WorkGiverDef</code> entries that only members of your race can be assigned to.<br/><br/>
This can be used to restrict work options, such as being able to use specific workbenches.
</td></tr>
</tbody>
</table>
