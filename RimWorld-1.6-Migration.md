This a guide to vanilla RimWorld changes and compatibility updates for Humanoid Alien Races for RimWorld 1.6 and the upcoming Odyssey DLC. This is a work in progress and will be updated as new information is available; please join the **[Alien Races Discord](http://discord.gg/XMCRj46)** for the latest information!

This document is primarily focused on game changes specific to Humanoid Alien Races; for a broader record of game changes as well as links to the official change log and modder primer, please also check out the [RimWorld 1.6 Mod Updates](https://rimworldwiki.com/wiki/Modding_Tutorials/RimWorld_1.6_Mod_Updates) page on the main RimWorld Wiki.

You can get the current development version of Humanoid Alien Races by downloading the Dev branch from GitHub or by using the Steam Workshop item here: **[Humanoid Alien Races - Dev](https://steamcommunity.com/sharedfiles/filedetails/?id=2640710953)** Note that since it has a different packageId from the live version of HAR, mods may throw an error about missing dependencies. This is normal and can safely be ignored; loading both at the same time will break your game.

# RimWorld 1.6 Core Changes

In general, RimWorld v1.6 seems to have had minimal impact on Humanoid Alien Races. If you find any additional changes that need to be made, please let us know on Discord so this document can be updated.

* `<forceGender>` is now a field in RaceProperties. This can be used to force an entire race to only generate as one gender, as opposed to setting `<fixedGender>` on all PawnKindDefs for a race.
* ScenarioDefs have several new fields to define which planet layer they start on and omitting these will cause your scenario to fail to load properly. If you have custom scenarios, consider inheriting from the new abstract `ScenarioBase`.

# Odyssey DLC Compatibility

At the time of writing (2025-06-17), the following has been gleaned from datamining alone and thus may not be comprehensive or representative of the final DLC contents.

## StatDefs

As with all DLC-locked StatDefs, if you use these without requiring Odyssey as a dependency then you should use `MayRequire="Ludeon.RimWorld.Odyssey"`.

* VacuumResistance - Appears to determine whether a Pawn takes vacuum burn damage, presumably while in space or other airless environments. The default value is 0 and a Pawn becomes fully immune at 1.0. Notably, vanilla apparel that have been upgraded with VacuumResistance such as recon and marine armor do *not* have full vacuum resistance, meaning a Pawn cannot stay in vacuum indefinitely.
* PilotingAbility
* FishingSpeed
* FishingYield
* GravshipRange - Most likely not a Pawn stat
* SubstructureSupport - Most likely not a Pawn stat

## FactionDefs

* There is a new `<arrivalLayerWhitelist>` entry that appears to only be on the vanilla Mechanoids faction, which explicitly lists the vanilla `Surface` layer as well as the Odyssey `Orbit` layer under a MayRequire. This potentially restricts which factions can raid which planet layers.