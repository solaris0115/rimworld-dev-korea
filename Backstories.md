As of RimWorld 1.4, BackstoryDefs are now a vanilla Def type. AlienBackstoryDefs have additional
options on top of what vanilla BackstoryDefs provide, however alien races can use either.

**Note for modders updating to RimWorld 1.4**: HAR BackstoryDefs were renamed from
<code>AlienRace.BackstoryDef</code> to <code>AlienRace.AlienBackstoryDef</code>. If you do not
rename your old BackstoryDefs, then they will silently fail to be recognized by the RimWorld XML
loader and you will not know until your pawns fail to find valid backstories to generate with.
**In addition**, many fields were renamed due to overlaps or conflicts with the new vanilla
BackstoryDef, please check all of your fields to ensure they are correct.

## Using Custom Backstories

To make your race use your custom backstory categories, you must designate their tag(s) inside
your FactionDefs or PawnKindDefs.

Specifying backstory filters in a FactionDef enables them for all members of that faction,
even if they are not a member of your race:

```xml
<FactionDef>
  <defName>MyRace_CustomFaction</defName>
  <!-- many, many fields omitted -->
  
  <backstoryFilters>
    <li>
      <categories>
        <li>MyRace_BackstoryCategoryName</li>
        <li>MyRace_AlternateBackstories</li>
      </categories>
    </li>
  </backstoryFilters>
</FactionDef>
```

Specifying backstory filters in a PawnKindDef's <code>backstoryFilters</code> field will cause
them to be appended to their FactionDef's backstory filters.

```xml
<PawnKindDef>
  <defName>MyRace_ExampleKind</defName>
  <label>colonist</label>
  <race>MyRaceDefName</race>
  <defaultFactionType>MyRace_CustomFaction</defaultFactionType>
  <backstoryFilters>
    <li>
      <categories>
        <li>MyRace_SpecificBackstorySubset</li>
      </categories>
    </li>
  </backstoryFilters>
</PawnKindDef>
```

Specifying backstory filters in a PawnKindDef's <code>backstoryFiltersOverride</code> field
will cause them to completely replace any backstoryFilters inherited from its FactionDef.

This is recommended for player colonist PawnKinds if you are using [[Race Settings]]
to inject them into vanilla ScenarioDefs or if you have mixed-race factions and wish to keep your
backstories limited to specific members of your race.

```xml
<PawnKindDef>
  <defName>MyRace_ExampleKind</defName>
  <label>colonist</label>
  <race>MyRaceDefName</race>
  <defaultFactionType>MyRace_CustomFaction</defaultFactionType>
  <backstoryFiltersOverride>
    <li>
      <categories>
        <li>MyRace_BackstoryCategoryName</li>
      </categories>
    </li>
  </backstoryFiltersOverride>
</PawnKindDef>
```

**Note**: Since backstory category tags are arbitrary strings that are used in a global context,
it is strongly recommended that you prefix your category tags for uniqueness, just as you would
for defNames.

## Creating Custom Backstories

Individual backstories are created using individual <code>AlienRace.AlienBackstoryDef</code>
Defs. This is a subclass of the vanilla <code>BackstoryDef</code> and thus inherits many fields
from the vanilla class.

```xml
<AlienRace.AlienBackstoryDef>
  <!-- backstory fields go here -->
</AlienRace.AlienBackstoryDef>
```

### Vanilla <code>BackstoryDef</code> Fields

The following fields are inherited from the vanilla <code>BackstoryDef</code>.

<table>
<thead>
<tr><th align="left">Field</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

```xml
<identifier>DO_NOT_USE</identifier>
```
</td>
<td>
<strong>WARNING</strong>: This is a vanilla field used for pre-1.4 back-compatibility.
It is automatically filled with your <code>defName</code> by HAR
and should <strong>NOT</strong> be used directly for new backstories.
</td></tr>
<tr><td>

```xml
<defName>MyRace_MyCustomBackstory</defName>
```
</td>
<td>
The unique identifier for your backstory. As with all <code>defName</code> fields,
it must be globally unique across all mods, so prefixing your defNames with a unique
string such as your race or mod name is strongly recommended.
</td></tr>
<tr><td>

```xml
<slot>Adulthood</slot>
```
</td>
<td>
(Default: <code>Childhood</code>)
Determines whether your backstory is a <code>Childhood</code> or <code>Adulthood</code>
backstory. These are the only valid values for this field.
</td></tr>
<tr><td>

```xml
<title>alien hero</title>
```
</td>
<td>
(Required) The full name of this backstory. Unless it is a proper name, it should be left
lowercase so that the game's grammar resolver can capitalized it as needed.
</td></tr>
<tr><td>

```xml
<titleShort>hero</titleShort>
```
</td>
<td>
(Required) The short name of this backstory. Used in places such as inspect panes where there
is insufficient space for longer backstory names. Does not actually have to be different from the
regular <code>title</code> if it is short enough to fit in compact places.
</td></tr>
<tr><td>

```xml
<titleFemale>alien heroine</titleFemale>
```
</td>
<td>
(Optional) If provided, then this alternate title will be used for female pawns
with this backstory. 
</td></tr>
<tr><td>

```xml
<titleShortFemale>heroine</titleShortFemale>
```
</td>
<td>
(Optional) If provided, then this alternate short title will be used for female pawns
with this backstory.
</td></tr>
<tr><td>

```xml
<description>[PAWN_nameDef] was a hero to [PAWN_possessive] people.
[PAWN_pronoun] carried [PAWN_objective]self with dignity and
confidence but often let [PAWN_possessive] accomplishments
get to [PAWN_possessive] head.</description>
```
</td>
<td>
<strong>RimWorld 1.5+</strong> - In 1.5, BackstoryDef now uses the standard <code>description</code> field. In RimWorld 1.4 and earlier, you should use <code>baseDesc</code> instead.<br/><br/>

Sets the full description of your backstory. Specific string tokens can be used to customize
the description for specific pawns:

<code>[PAWN_nameDef]</code> - The short name of the pawn, i.e. its first name.<br/>
<code>[PAWN_pronoun]</code> - he/she<br/>
<code>[PAWN_possessive]</code> - his/her<br/>
<code>[PAWN_objective]</code> - him/her

These strings will be automatically capitalized by the grammar resolver as necessary.
</td></tr>
<tr><td>

**RimWorld 1.5+**:
```xml
<skillGains>
  <Social>4</Social>
  <Shooting>3</Shooting>
  <Melee>2</Melee>
  <Plants>-2</Plants>
</skillGains>
```

**RimWorld 1.4 and earlier**:
```xml
<skillGains>
  <li><key>Social</key><value>4</value></li>
  <li><key>Shooting</key><value>3</value></li>
  <li><key>Melee</key><value>2</value></li>
  <li><key>Plants</key><value>-2</value></li>
</skillGains>
```
</td>
<td>
(Optional) Sets skill bonuses and penalties for this backstory. Please see the [[RimWorld 1.5 Migration Guide|RimWorld-1.5-Migration]] for information on how to easily convert between the legacy syntax and the new syntax.
</td></tr>
<tr><td>

```xml
<workDisables>ManualDumb,PlantWork</workDisables>
```
</td>
<td>
(Optional, default: <code>None</code>) Determines the work types that are disabled (incapable of)
for pawns with this backstory.

The available values for this field are:
<code>None</code> (Default),
<code>ManualDumb</code>,
<code>ManualSkilled</code>,
<code>Violent</code>,
<code>Caring</code>,
<code>Social</code>,
<code>Commoner</code>,
<code>Intellectual</code>,
<code>Animals</code>,
<code>Artistic</code>,
<code>Crafting</code>,
<code>Firefighting</code>,
<code>Cleaning</code>,
<code>Hauling</code>,
<code>PlantWork</code>,
<code>Mining</code>,
<code>Hunting</code>,
<code>Constructing</code>,
<code>Shooting</code>,
<code>AllWork</code>
</td></tr>
<tr><td>

```xml
<requiredWorkTags>Violent</requiredWorkTags>
```
</td>
<td>
(Optional, default: <code>None</code>) Sets work tags that are required for this backstory.
When applied to <code>Adulthood</code> backstories, will cause this backstory to only
be paired with <code>Childhood</code> backstories whose disabled work types do not
include the specified work types.
</td></tr>
<tr><td>

```xml
<spawnCategories>
  <li>MyRace_GeneralBackstories</li>
  <li>MyRace_EliteBackstories</li>
</spawnCategories>
```
</td>
<td>
(Optional) Sets the spawn category tags for your backstory.
See the "Using Custom Backstories" section for details on how these are used.

<strong>Warning</strong>: as spawn categories are arbitrary strings with global scope,
it is strongly recommended that you use a unique prefix for your spawn categories just
as you would for <code>defName</code> fields.
</td></tr>
<tr><td>

```xml
<bodyTypeMale>Male</bodyTypeMale>
<bodyTypeFemale>Female</bodyTypeFemale>
<bodyTypeGlobal>Thin</bodyTypeGlobal>
```
</td>
<td>
(Optional) Sets a BodyTypeDef override for this backstory, with <code>bodyTypeMale</code>
and <code>bodyTypeFemale</code> taking precedence over <code>bodyTypeGlobal</code>
if appropriate. Only works when used on <code>Adulthood</code> backstories.
</td></tr>
<tr><td>

```xml
<forcedTraits>
  <Tough>0</Tough>
  <NaturalMood>1</NaturalMood>
</forcedTraits>
```
</td>
<td>
(Optional) Sets forced traits for pawns with this backstory. Spectrum traits should have the
degree value specified, while non-spectrum traits should use a value of <code>0</code>.

<strong>Note</strong>: Forced traits can bypass the trait limit of a given pawn's race,
the game will simply not add any more randomly generated traits if forced traits push
that pawn to or past its limit.
</td></tr>
<tr><td>

```xml
<disallowedTraits>
  <Psychopath>0</Psychopath>
  <Nerves>-1</Nerves>
  <Nerves>-2</Nerves>
</disallowedTraits>
```
</td>
<td>
(Optional) Sets traits that cannot be randomly generated for a pawn with this backstory.
Spectrum traits should have the degree value specified, while non-spectrum traits
should use a value of <code>0</code>.
</td></tr>
<tr><td>

```xml
<nameMaker>MyRace_CustomHeroNameMaker</nameMaker>
```
</td>
<td>
(Optional) Sets a RulePackDef that will be used for pawns with this backstory.
<code>Childhood</code> overrides will override <code>Adulthood</code> overrides.
Backstory overrides will override race and culture namers, but will be overridden
by pawnKind and xenotype namers.
</td></tr>
<tr><td>

```xml
<possessions>
  <li>
    <key>Gun_Autopistol</key>
    <value>1</value>
  </li>
</possessions>
```
</td>
<td>
(Optional) Sets one or more additional possessions that belong to this pawn.
If playing on a non-Naked Brutality scenario, up to two additional possessions
can be generated alongside the standard starting resources and equipment.
This can be ignored if there are higher-priority additional starting items,
such as baby food for baby pawns, hemogen packs for sanguophage pawns,
or starting drug stashes for pawns with addictions.
</td></tr>
<tr><td>

```xml
<shuffleable>true</shuffleable>
```
</td>
<td>
(Optional) If set to <code>false</code>, then this backstory cannot be randomly generated.
This is used for [[PawnBios|PawnBioDef]].
</td></tr>
</tbody>
</table>

### <code>AlienRace.AlienBackstoryDef</code> Additional Fields

The following fields are only available in HAR's AlienBackstoryDef class and thus cannot be
used in vanilla BackstoryDefs.

<table>
<thead>
<tr><th align="left">Field</th><th align="left">Description</th></tr>
</thead>
<tbody>
<tr><td>

**RimWorld 1.5+**:
```xml
<forcedTraitsChance>
  <li>
    <defName Degree="1">NaturalMood</defName>
    <chance>50</chance>
  </li>
  <li>
    <defName Degree="2">NaturalMood</defName>
  </li>
  <li>
    <defName>Nimble</defName>
    <chance>50</chance>
  </li>
</forcedTraitsChance>
```

**RimWorld 1.4 and earlier**:
```xml
<forcedTraitsChance>
  <li>
    <defName>NaturalMood</defName>
    <degree>1</degree>
    <chance>50</chance>
  </li>
  <li>
    <defName>NaturalMood</defName>
    <degree>2</degree>
  </li>
  <li>
    <defName>Nimble</defName>
    <chance>50</chance>
  </li>
</forcedTraitsChance>
```
</td>
<td>
(Optional) Sets forced traits with a random chance factor. Chance values should be from
<code>0</code> to <code>100</code>, inclusive. Note that entries are resolved
from top to bottom, thus utilizing multiple degrees of a spectrum trait will only use the
first entry to be resolved. In the given example, there is a 50% chance for this pawn to
have Optimist, and if it does not have Optimist then it will have Steadfast.

**Note**: This was renamed from <code>forcedTraits</code> to avoid conflicting with the new
vanilla BackstoryDef's forcedTraits field. This field retains the original HAR syntax
for backwards compatibility.
</td></tr>
<tr><td>

```xml
<disallowedTraitsChance>
  <!-- same syntax as above -->
</disallowedTraitsChance>
```
</td>
<td>
(Optional) Sets disallowed traits. This was renamed from <code>disallowedTraits</code>
to avoid conflicting with the vanilla BackstoryDef's disallowedTraits field.
</td></tr>
<tr><td>

```xml
<workAllows>AllWork</workAllows>
```
</td>
<td>
(Optional, default: <code>AllWork</code>) Sets work types allowed by this backstory.
If set to a value other than <code>AllWork</code>, the inverse of this field is used
to overwrite the vanilla <code>workDisables</code> field. This field is retained for
backwards compatibility with backstories written for older versions of HAR or if writing
allowed work types is easier than disallowed types, but is otherwise obsolete.
</td></tr>
<tr><td>

```xml
<maleCommonality>100</maleCommonality>
<femaleCommonality>100</femaleCommonality>
```
</td>
<td>
(Optional, default: <code>100</code>) Sets the commonality of this backstory for
the given genders. Values should be between <code>0</code> to <code>100</code> (inclusive).
Usually used to completely disable a backstory for a given gender.
</td></tr>
<tr><td>

```xml
<linkedBackstory>MyRace_LinkedBackstory</linkedBackstory>
```
</td>
<td>
(Optional) If set on a <code>Childhood</code> backstory, then the specified backstory
will be forced as this pawn's adult backstory, if applicable.

If set on an <code>Adulthood</code> backstory, then this backstory will only be generated
for a pawn with the specified backstory as its childhood backstory. Furthermore, only
backstories linked in this way can be chosen, allowing you to specify a subset of valid
adulthoods for a given childhood.
</td></tr>
<tr><td>

```xml
<relationSettings>
  <!-- see description -->
</relationSettings>
```
</td>
<td>
(Optional) Backstories can be used to alter the chance of generating a pawn with an existing
relationship to this pawn. See [[Relation-Settings|Relation-Settings]] for more details.
</td></tr>
<tr><td>

```xml
<forcedHediffs>
  <li>WakeUpTolerance</li>
</forcedHediffs>
```
</td>
<td>
(Optional) If set, applies the specified HediffDefs to a pawn that generates with this
backstory. Can only be used to apply a whole-body hediff, and said hediff will be applied
at its default <code>initialSeverity</code>.
</td></tr>
<tr><td>

**RimWorld 1.5+**:
```xml
<passions>
  <Shooting>2</Shooting>
  <Melee>1</Melee>
</passions>
```

**RimWorld 1.4 and earlier**:
```xml
<passions>
  <li><skill>Shooting</skill><xp>2</xp></li>
  <li><skill>Melee</skill><xp>1</xp></li>
</passions>
```
</td>
<td>
(Optional) Forces a skill passion level for the specified skills. 0 results in no passion,
1 results in a single-flame passion, and 2 results in a double-flame passion.

<strong>Note</strong>: This value is a specific override, not a minimum level.
</td></tr>
<tr><td>

```xml
<bioAgeRange>21~34</bioAgeRange>
```
</td>
<td>
(Optional) Sets the allowed biological age range for this backstory.

<strong>Note</strong>:
This is only used to validate the backstory against a pawn being generated;
if this range falls outside the range allowed by the pawn's PawnKindDef or race,
then this backstory will never be chosen.
</td></tr>
<tr><td>

```xml
<chronoAgeRange>21~85</chronoAgeRange>
```
</td>
<td>
(Optional) Sets the allows chronological age range for this backstory.

<strong>Note</strong>:
This is only used to validate the backstory against a pawn being generated;
if this range falls outside the range allowed by the pawn's PawnKindDef or race,
then this backstory will never be chosen.
</td></tr>
<tr><td>

```xml
<forcedItems>
  <MedicineIndustrial>1</MedicineIndustrial>
</forcedItems>
```
</td>
<td>
(Optional) If set, then the specified items will be added to the inventory of pawns
with this backstory. Unlike the vanilla <code>possessions</code> field,
items specified here will bypass additional possession limits and be placed directly
into the pawn's inventory rather than on the ground with the rest of your starting supplies.
</td></tr>
</tbody>
</table>
