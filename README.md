# XOHR Extraction

On September 10th 2024, LEET.cc (the host company for XOXO High RolePlay/Aurelia) shut down.

As part of the shutdown process, they provided copies of the worlds and player data to server owners.

Becca was kind enough to send me a copy of the XOXO/Aurelia data, so I could attempt to update it to modern Minecraft versions, as well as convert it to Java edition.

This repository holds all the different copies of the worlds, from the raw source files, to the fully converted Java edition maps.

## Gimme The Files, Nothing Else Matters
Okay, okay. The only two folders you need are "Bedrock" and "Java - Full"; Everything else is just for development and reference purposes only.

You can download them from the [Releases](releases/latest/) page; Use the [Directory](#directory) to understand what's in each folder, and [Worlds](#worlds) to understand what worlds are available.

## Worlds
The following table shows the worlds provided by LEET, their usability, platform and contents.

| World Name |                     Usable                     | Platform       | Notes                                                                                                     |
|------------|:----------------------------------------------:|----------------|-----------------------------------------------------------------------------------------------------------|
| desert     |                       ✅                        | Bedrock Only   | Has three copies of a build that also appears in "empty" and "flat"                                       |
| empty      |                       ✅                        | Bedrock Only   | Has a broken fragment of a build that also appears in "desert" and "flat"                                 |
| flat       |                       ✅                        | Bedrock + Java | Appears to also be known as "world", but is different from "world". Has Minigames and an unfinished city. |
| highschool |                       ✅                        | Bedrock Only   | Has a highschool called "Bullworth Academy", that was likely one of the purchasable maps in LEETs app.    |
| notch      | ❌<sup><a name="cite-1"></a>[[1]](#ref-1)</sup> | N/A            | World appears to be corrupted. Was likely one of the purchasable maps in LEETs app.                       |
| Plots      |                       ✅                        | Bedrock + Java | Has very little beyond a couple scattered builds, and lots of generated plots.                            |
| skyblock   |                       ✅                        | Bedrock + Java | Has the Skyblock Hub, and a variety of islands that players had claimed.                                  |
| standard   |                       ✅                        | Bedrock Only   | Has nothing bar two patches of generated overworld terrain                                                |
| world      |                       ✅                        | Bedrock + Java | The primary world of the server, has the majority of the builds.                                          |


## Directory:

- [Bedrock](Bedrock/)
  - These files are the maps in a format compatible with modern versions of Bedrock Edition.
- [Java - Full](Java%20-%20Full)
  - These files are the maps fully converted to Java Edition.

***

All files in the below folders are for upgrading or repairing the maps. They are not intended to be used as full releases.
- Dev
  - [Raw Source Files](Dev/Raw%20Source.zip)
    - Worlds
      - The files here are the raw maps as provided by LEET. They are not _directly_ compatible with any known version of Minecraft, though you can certainly use them as I did to create copies compatible with modern Bedrock.
    - Players
      - The files here are the player data for myself and Becca. No older player data was available, due to the common need for player data resets.
  - [Bedrock - Chunk Updated](Dev/Bedrock%20-%20Chunk%20Updated)
    - These files are functionally identical to the [Bedrock](Bedrock) files, but with the important addition of ~99% of the chunks being updated. _This only matters if you're converting them to Java Edition yourself._
  - [Java - Initial](Dev/Java%20-%20Initial)
    - These files are the [Bedrock](Bedrock) files converted to Java Edition. No chunk updates or repairs have been performed on them, and they should only be used for reference and testing.
  - [Java - Chunk Updated](Dev/Java%20-%20Chunk%20Updated)
    - These files are the [Bedrock - Chunk Updated](Dev/Bedrock%20-%20Chunk%20Updated) files converted to Java Edition. No repairs have been performed on them, and they should only be used for reference and testing.

## Update Process
The process of updating and converting the maps is as follows:
1. Load the raw worlds one at a time in a PocketMine-MP server.
2. Once PocketMine-MP has loaded and updated the worlds, close the server and copy the updated world files.
3. Open Minecraft Bedrock, and create a new singleplayer world. Name it the same as the updated world.
4. Open your Bedrock worlds directory. This is located at `games/com.mojang/minecraftWorlds` on mobile devices, and `C:\Users\{USER}}\AppData\Local\Packages\Microsoft.MinecraftUWP_8wekyb3d8bbwe\LocalState\games\com.mojang\minecraftWorlds` on Windows 10.
   1. I recommend pinning the directory to Quick Access if you're on Windows 10.
5. Locate the folder of the new world you just created, and paste in the updated world files from Step 2
6. Download [this](Dev/Utilities/level.dat) `level.dat`file, and place it in the world folder, replacing the existing one, and delete the `level.dat_old` file. Edit the `level.dat` file to change the `LevelName` as needed.
   1. You will need to use [nbt-studio](https://github.com/tryashtar/nbt-studio) to edit the `level.dat` file.
7. Open the world in Minecraft Bedrock to verify everything works. Once it has loaded, save and quit the world.
   1. Optional: Export the world at this stage as a `.mcworld` file, for backup purposes.

You have now completed an initial upgrade of the raw files to the latest Bedrock world format. All instructions after this point are for converting the maps to Java Edition.

8. Download and open the latest version of [Chunker](https://github.com/HiveGamesOSS/Chunker/releases/latest).
9. Select the Bedrock world to convert, choose the latest non-Beta version of Java Edition to convert to, then click "Advanced Mode"
10. Click on "World Settings", set "Generator" to "Void" and toggle "Map Features" off. Everything else should be pre-set if you used the `level.dat` file linked above in Step 6.
11. Click "Convert", wait for the conversion to complete, then save it as a `.zip` file.

You have now completed an initial conversion to Java Edition. 

It's important to note however that a variety of issues will exist in the world, notably that Block Entities (Chests, Item Frames, Flower Pots, etc.) do not have their contents on Java Edition. This seems to be caused by the fact that the world has very old chunk data that dates back to MCBE 1.8.<sup><a name="cite-2"></a>[[2]](#ref-2 "https://github.com/HiveGamesOSS/Chunker/issues/40#issuecomment-2348474314")</sup>.

Follow the next steps to fix these issues.

12. Open the world in Minecraft Bedrock, and locate any Block Entities. The easiest way to do this is to have the initial conversion Minecraft Java world open side-by-side, with a mod installed that can ESP/Highlight all Chests, Item Frames, and Flower Pots.
13. In the Bedrock world, place and break a block anywhere in the vicinity of a Block Entity. This will update the chunk you placed and broke the block in, as well as chunks in a 5 chunk radius around it.<sup>[citation needed]</sup> This means you do not need to manually update every single chunk that has Block Entities, and instead can just target clusters.
14. When you have completed chunk updates, save and quit the world.
    1. Optional: Export the world at this stage as a `.mcworld` file, for backup purposes.
15. Repeat steps 8-11 to convert the world to Java Edition.

You have now completed a full conversion to Java Edition.

It's important to note however that some issues with Signs may still exist. On Chunker 1.1.3 and below, some signs text was improperly split, resulting in all the text being on Line 1. Additionally, signs in chunks that were updated in steps 12-15 will have a glowing effect applied to their text.

Fixing these signs requires viewing both the Minecraft Bedrock and Minecraft Java worlds side-by-side, to compare each sign and repair it when needed. It is recommended to use the ESP/Highlight mod from Step 12 to locate all the signs.

## Known Issues
### Java Edition:
- Block Entities do not fully convert to Java Edition without Chunk Updates first being applied on Bedrock
  - This is not normally the case, but due to how LEET stored/saved the worlds, it is necessary.
- Signs do not properly convert to Java Edition regardless of Chunk Updates
  - When a Chunk Update is applied, the sign actually converts _less_ properly, by way of having glowing applied to the text.
  - All text is retained on signs, though it is not always visible due to sometimes being all on Line 1. The conditions for visibility seem to require intentional line breaks and/or colored text on the source sign. <sup>[citation needed]</sup>
  - The signs in the full release for Java Edition have been repaired with de-glowing and line-breaking where necessary.
    - Some line-breaks resulted in text being cut off, due to the abuse of unicode characters on Bedrock allowing for smaller text and thus more characters per line than Java Edition allows.
  - Some signs are invisible. Many of these were repaired in the full release, but some remain. This seems to be a side effect caused by whatever form of WorldEdit LEET used. <sup>[citation needed]</sup>
- A variety of blocks are replaced with air when converting to Java Edition, due to their being Bedrock-only<sup><a name="cite-3"></a>[[3]](#ref-3 "https://minecraft.wiki/w/Bedrock_Edition_exclusive_features#Blocks")</sup>
  - This applies to Nether Reactor Cores, Glowing Obsidian, Glowsticks, End Gateways, Cameras, and Update Blocks, just to name a few.
- Some Items and Books may not convert to Java Edition properly
  - Items with glitched/"illegal" enchants did not convert properly, and errors were printed regarding several books, though the books themselves were unable to be located for comparison and verification.

### Bedrock Edition:
- Some signs are invisible. Many of these were repaired in the full release, but some remain. This seems to be a side effect caused by whatever form of WorldEdit LEET used. <sup>[citation needed]</sup>
- End Gateways (the starry block inside an End Portal) were replaced with air when upgrading to modern Bedrock. This is  because they either no longer exist, or exist under a different ID/name.<sup>[citation needed]</sup>


## References
<a name="ref-1"></a>1. [↑](#cite-1) `2024-09-27 [18:11:52.332] [Server thread/ERROR]: Could not load world "notch": Corruption detected: Corrupted world data: Failed to decompress level.dat contents`

<a name="ref-2"></a>2. [↑](#cite-2) https://github.com/HiveGamesOSS/Chunker/issues/40#issuecomment-2348474314

<a name="ref-3"></a>3. [↑](#cite-3) https://minecraft.wiki/w/Bedrock_Edition_exclusive_features#Blocks