The following are new features added as of January 29, 2024.

# BodyAddon customization in styling stations

BodyAddons for alien races can now be customized in Ideology's styling station. This is done through a separate Racial Features tab in the styling station UI.

## XML configuration options

The following new options are available on BodyAddons to support this feature:

<table>
<thead>
<tr><th align="left">Setting</th><th align="left">Default</th><th align="left">Description</th></tr>
</thead>
<tbody>

<tr><td>

```xml
<userCustomizable>false</userCustomizable>
```
</td><td>
<code>true</code>
</td><td>
If set to <code>false</code>, then the specified BodyAddon will not be customizable by players. This should generally only be used for BodyAddons that have no variants or color options and thus cannot be customized anyways.
</td></tr>
<tr><td>

```xml
<allowColorOverride>true</allowColorOverride>
```
</td><td>
<code>true</code>
</td><td>
If set to true, then players will be able to color this BodyAddon separately from the normal color channel assigned to this BodyAddon.
</td></tr>
</table>

## Color generator options

The styling station will attempt to automatically pull exemplar colors from ColorGenerators with ranges, but you can specify additional color samples using the new IAlienChannelColorGenerator interface:

```cs
public interface IAlienChannelColorGenerator
{
  public List<Color> AvailableColors(Pawn pawn);

  public List<ColorGenerator> AvailableGenerators(Pawn pawn);
}
```

An example of an in-framework implementation of this interface can be seen [here](https://github.com/solaris0115/rimworld-dev-korea/blob/Dev/Source/AlienRace/AlienRace/ColorGenerators.cs#L41-L68)

# Race-specific overrides for StatPart_Age

Alien races can now have race-specific overrides for StatPart_Age. This is used for the following official content StatDefs:

```
WorkSpeedGlobal
ShootingAccuracyChildFactor
MarketValue
MeleeHitChance
AimingDelayFactor
ImmunityGainSpeed
ArrestSuccessChance
```

Overrides can be applied by adding <code>ageStatOverrides</code> to your <code>generalSettings</code> as follows:

```xml
<generalSettings>
  <ageStatOverrides>
    <WorkSpeedGlobal>
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(4,0.2)</li>
          <li>(12,0.8)</li>
          <li>(18,1)</li>
        </points>
      </curve>
    </WorkSpeedGlobal>
    <!-- This one requires a MayRequire because the stat itself is Biotech-specific -->
    <ShootingAccuracyChildFactor MayRequire="Ludeon.RimWorld.Biotech">
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(4,0.95)</li> 
          <li>(12,0.98)</li>
          <li>(13,1)</li>
        </points>
      </curve>
    </ShootingAccuracyChildFactor>
    <MarketValue>
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(3,0.5)</li>
          <li>(13,0.9)</li>
          <li>(18,1)</li>
        </points>
      </curve>
    </MarketValue>
    <MeleeHitChance>
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(4,0.05)</li>
          <li>(12,0.8)</li>
          <li>(13,1)</li>
        </points>
      </curve>
    </MeleeHitChance>
    <AimingDelayFactor>
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(4,1.8)</li>
          <li>(12,1.1)</li>
          <li>(13,1)</li>
        </points>
      </curve>
    </AimingDelayFactor>
    <!-- This is the only stat that doesn't use biological years by default because it's used for non-humanlike pawns -->
    <ImmunityGainSpeed>
      <curve>
        <points>
          <li>(0.65,1)</li>
          <li>(0.8,0.95)</li>
          <li>(1.0,0.9)</li>
          <li>(1.2,0.8)</li>
          <li>(1.5,0.5)</li>
        </points>
      </curve>
    </ImmunityGainSpeed>
    <ArrestSuccessChance>
      <useBiologicalYears>true</useBiologicalYears>
      <curve>
        <points>
          <li>(3, 0.05)</li>
          <li>(13, 0.8)</li>
          <li>(18, 1)</li>
        </points>
      </curve>
    </ArrestSuccessChance>
  </ageStatOverrides>
</generalSettings>
```

All overrides are optional; default behavior is to use the default curve specified in the StatPart. Overrides support any StatDef with StatPart_Age, even ones from mods, although you should use MayRequire for such StatDefs unless they are from mods that are hard dependencies for your mod.

Note that the value of <code>useBiologicalYears</code> does *not* need to match the vanilla StatPart's value. You can use whatever is more convenient for you. <code>humanlikeOnly</code> can technically be used in these overrides as well, but it will not do anything as the field is ignored and these overrides will only be triggered for your specific race anyways.

# Custom Growth Factors

You can now change the rate at which children of your race accumulate growth points by defining a custom curve where the left side value is the age in years and the right side value is the rate factor. The following example approximates the vanilla Human values:

```xml
<alienRace>
  <generalSettings>
    <growthFactorByAge>
      <points>
        <li>(0,1)</li>
        <li>(6,1)</li>
        <li>(7,0.75)</li>
        <li>(13,0.75)</li>
      </points>
    </growthFactorByAge>
  </generalSettings>
</alienRace>
```

# Favorite Color Channel

There is now a <code>favorite</code> color channel that can be used anywhere color channels are usable. The <code>first</code> color is the pawn's current favorite color, the <code>second</code> color will be the pawn's original favorite color if another mod has allowed it to be changed somehow.

# Racial Abilities

A new option has been added to <code>generalSettings</code> for adding vanilla-compatible <code>AbilityDef</code> entries to members of your race. There are a number of selection options available as well:

```xml
<alienRace>
  <generalSettings>
    <abilities>

      <!-- always added -->
      <li>FireSpew</li>

      <!-- 50% chance of being added to any given pawn -->
      <li>
        <defName>FoamSpray</defName>
        <chance>50</chance>
      </li>

      <!-- randomly select 2 distinct options -->
      <li>
        <options>
          <li>AcidSpray</li>
          <li>FireBurst</li>
          <li>AnimalWarcall</li>
        </options>
        <count>2</count>
      </li>

      <!-- always added for male pawns -->
      <li>
        <defName>MyRace_CustomMaleAbility</defName>
        <commonalityFemale>0</commonalityFemale>
      </li>

      <!-- 75% chance of adding both for female pawns -->
      <li>
        <options>
          <li>MyRace_CustomFemaleAbilityA</li>
          <li>MyRace_CustomFemaleAbilityB</li>
        </options>
        <commonalityFemale>75</commonalityFemale>
        <commonalityMale>0</commonalityMale>
      </li>

    </abilities>
  </generalSettings>
</alienRace>
```

Similar to extension graphics, entries for abilities can also be nested:

```xml
<alienRace>
  <generalSettings>
    <abilities>

      <li>
        <!-- always added -->
        <defName>FoamSpray</defName>
        <chance>100</chance>
        <options>
          <li>
            <!-- 50% chance that two of the following are added -->
            <chance>50</chance>
            <options>
              <li>AcidSpray</li>
              <li>FireBurst</li>
              <li>AnimalWarcall</li>
            </options>
            <count>2</count>
          </li>
          <!-- always added -->
          <li>FireSpew</li>
        </options>
        <count>2</count>
      </li>

    </abilities>
  </generalSettings>
</alienRace>
```
