# Tips for New Race Modders

1. Custom humanlike races are complex and time-consuming to make! If you are new to RimWorld modding, it is strongly recommended that you cut your teeth on simpler content first, such as weapons, apparel, or animals. If you are unfamiliar with any of the following game systems, please check out the link to the general RimWorld tutorials further down the page: race Defs, race properties, PawnKindDefs, faction Defs (if you are making a custom faction for your face), and player factions (if you are making a starting scenario for your race).
2. Please read the whole wiki! The wiki has comprehensive documentation for all commonly used functions of the framework, so chances are whatever basic questions you have will be answered somewhere in it!
3. If you are having difficulty understanding how everything fits together or would otherwise like a working reference, try looking at a simple race mod to see it's made: [Rockmen by goudaQuiche](https://github.com/goudaQuiche/LTF_Rockmen), 
[Bun Race by Spanky-H](https://github.com/Spanky-H/BunRace) (Warning: out of date, has not been updated to 1.3)
4. If you are unsure about how something works, just try it out! A lot of the XML starts to make more sense once you play around with it. Feel free to reach out if you can't get it to work, often times there is no substitute for just trial by error.
5. Join the [RimWorld Alien Races Discord](http://discord.gg/XMCRj46). Be sure to search for keywords on things you're trying to figure out; often times people have already had a discussion about the thing you're trying to figure out and you can quickly find answers that way!
6. Often times, Google searches for those same keywords can yield useful results as well!
7. Use [Quicktest](https://steamcommunity.com/sharedfiles/filedetails/?id=767889064) for testing out your race (or any mod in development in general). It lets you test things much faster by launching Rimworld immediately onto a small map with pawns.
8. Be sure to check out the rest of the resources on this page as well!

## Useful File Locations:

Vanilla RimWorld content, including XML Defs and translation files for both the Core game and official DLCs, can be found in your Steam directory here:

    C:\Program Files (x86)\Steam\SteamApps\common\RimWorld\Data\

Your local mod folder where you should copy your mods to for test (and where Mod Manager and RimPy save mods to) is here:

    C:\Program Files (x86)\Steam\SteamApps\common\RimWorld\Mods

Some useful modding information directly provided by Tynan and Ludeon:

    C:\Program Files (x86)\Steam\SteamApps\common\RimWorld\ModUpdating.txt

RimWorld log location, useful for sharing or if your game crashes on load such that you never even reach the main menu:

    C:\Users\[YourUserName]\AppData\LocalLow\Ludeon Studios\RimWorld by Ludeon Studios\Player.log

## Templates

It is recommended that you instead start with a blank race and only add what you need, as using a template results in potentially hundreds of lines of unneeded settings. The [[Getting Started]] tutorial has a link to a blank race if you need help setting up a mod folder for the first time.

The following templates were provided by goudaQuiche. However, they are at the time of writing out of date and no longer useful in starting a new race project:

* ~~[Race Template](https://github.com/goudaQuiche/MoHARHediffsExamples/blob/master/1.4/Defs/ThingDefs_Races/HAR_Template.xml.dis)~~
* ~~[Backstories Template](https://github.com/goudaQuiche/MoHARHediffsExamples/blob/master/1.4/Defs/BackstoryDefs/Backstories_Template.xml)~~

## Art and Textures

* You can find a link to the official RimWorld Art Source [in this post on the official Ludeon forums](https://ludeon.com/forums/index.php?topic=2325.0). These are useful in finding body and apparel templates for your race, as the published game assets are packed into a Unity asset bundle and cannot be directly opened in an external graphics program.
* [Colouring In Images](https://github.com/seraphile/rimshare/wiki/Colouring-in-Images) - A useful guide on how RimWorld applies colors and color masks.
* [Officially Unofficial Guide to Rimworld's Artstyle](https://spdskatr.github.io/RWModdingResources/artstyle) - A guide on RimWorld's art style, based on a talk given by Tynan at Game Developer's Conference (GDC) 2017.

## Modding XML & C#

### General Modding Tutorials:

* [Modding Tutorials on the RimWorld Wiki](https://rimworldwiki.com/wiki/Modding_Tutorials) - The most reliable source of modding information, especially the basics such as mod folder layout and Def structures.
* [Mod Folder Structure](https://rimworldwiki.com/wiki/Modding_Tutorials/Mod_folder_structure) - A guide to how mod folders should be laid out.
* [PatchOperations Guide](https://gist.github.com/Zhentar/4a1b71cea45b9337f70b30a21d868782) - A guide on how to use PatchOperations to modify existing XML Defs. A [full reference for vanilla PatchOperations](https://rimworldwiki.com/wiki/Modding_Tutorials/PatchOperations) can also be found on the RimWorld wiki.
* [Plague Gun (1.1)](https://rimworldwiki.com/wiki/Modding_Tutorials/Plague_Gun_(1.1)) - The go-to comprehensive tutorial for RimWorld, which covers all the basics including XML Defs and custom C# assemblies. Includes a link to a working repository. Still relevant as of 1.3, not much to do with weapons has changed since 1.1.

* (Mostly outdated, has not been updated since 1.0) [spdskatr's RimWorld Modding Resources](https://spdskatr.github.io/RWModdingResources/) - Still has links to many useful resources, though.
* (Outdated, has not been updated since 2017) [Roxxploxx's Modding Guide](https://github.com/roxxploxx/RimWorldModGuide/wiki)

### Advanced Modding Topics:

* [Harmony 2 Documentation](https://harmony.pardeike.net/index.html) - Harmony is a library used by modders for RimWorld and many other Unity/C# based games. Based on Reflection, it is used to intercept (patch) method calls and access restricted fields in advanced mods.
* (Slightly Outdated) [Combat Extended Compatibility](https://steamcommunity.com/sharedfiles/filedetails/?id=1758482195) - A guide on how to make your race compatible with Combat Extended. Should also check the [up to date reference sheet](https://github.com/CombatExtended-Continued/CombatExtended/wiki/Stat-&-Balance-Spreadsheets) for the updated CE repository.

