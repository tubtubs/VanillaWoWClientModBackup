### 12/04/2024 : 1.0.0
- First release

### 14/04/2024 : 1.1.0
- Fixed bug causing crash with SetMouseoverUnit
- CastSpellByName is now reverse compatible & can once again accept 1, 0, true, or false as OnSelf flags, in addition to the custom targeting by unit string.
- Added SelectionCircleStyle CVar.
- - "1" == [default classic style](https://github.com/balakethelock/SuperWoW/assets/111737968/5086467b-eb63-40aa-aec9-05d9848e8140)
- - "2" == [full circle style](https://github.com/balakethelock/SuperWoW/assets/111737968/6d6db191-bc61-44b0-81ac-54d614bf4db9)
- - "3" == [pointed circle style](https://github.com/balakethelock/SuperWoW/assets/111737968/be99853f-1754-47df-a6fa-818a52da2e71)
- - "4" == [facing classic style](https://github.com/balakethelock/SuperWoW/assets/111737968/550a443e-ea17-43b9-9d51-238672953b62)
- - If you want to use styles 2 or 3 you have to download the textures [here](https://github.com/balakethelock/SuperWoW/releases/tag/Patch)

### 02/05/2024 : 1.1.1
- Fixed bug with strings being turned to lowercase
- Added UncapSounds CVar. Set to "1" to remove the hardcoded soundchannels limit (you still have to set software sound channels to a high number if you want the max number of soundeffects played by the game)
- added new unit "mark1" to "mark8" that selects the corresponding target marker. explanation: UnitName("mark8") returns the name of the unit marked skull

### 05/09/2024 : 1.1.2
- Fixed UnitExists function (the invisible target bug)
- Fixed UnitBuff and UnitDebuff returning negative spell id.

### 09/10/2024 : 1.1.3
- Fixed some crashes with custom spells

### 07/11/2024 : 1.2
- Better compatibility with spell links of various addons. Now all spells use "enchant:" syntax for their hyperlinks. Update to latest SuperAPI for better support.
- New global variables SUPERWOW_STRING and SUPERWOW_VERSION give version info for addons.

### 22/11/2024 : 1.3
- Autoloot now works on enchanting & pick pocket.
- Added ImportFile and ExportFile functions to both FrameXML and GlueXML.

### 31/01/2025 : 1.4
- Fixed some unit signal events not always firing.
- Added LootSparkle CVar to show sparkles on lootable treasure.
- Reworked Raw GUID log. Raw Combat Log entries are now **always** accessible through the event RAW_COMBATLOG (arg1 = original event name, arg2 = text with GUID). This comes with removing the option to turn raw GUID mode on/off through LoggingCombat("RAW").
- Raw Combat Log also comes with its own separate txt file.
- lua function CombatLogAdd("text") now can accept a flag as 2nd argument to instead add the message to the raw log like so:
/run CombatLogAdd("hi world") --add the text to WoWCombatLog.txt
/run CombatLogAdd("hi world", 1) --add the text to WoWRawCombatLog.txt

### 10/07/2026: 2.0
- Code refactoring and performance boost.
- Split TrackUnit function to two separate functions, TrackUnit and UntrackUnit. UntrackUnit("all") can be used remove tracking from all units.
- Second Argument of function CastSpellByName can now accept "CLICK" to instantly cast reticle spells on mouseover location (bypassing targeting circle mode)
- Added UnitNameplate("unit") function that returns Nameplate frame.
- Added CanLootUnit("unit") function that returns whether a unit has loot inside.
- New ChatBubbleCvars: ChatBubbleRange (10-200 yards), ChatBubblesRaid, ChatBubblesBattleground, ChatBubblesWhisper, ChatBubblesCreatures
- Added NameplateRange CVar (10-80 yards). This takes precedance over all client modifications for Nameplate range.
- Added NameplateMotion CVar: 0 = Overlap. 1 = Default spread. 2 = Smart spread.
- Added HealingText CVar to toggle Floating Healing Text.
- Added CREATE_CHATBUBBLE event. arg1 = chatbubble frame, arg2 = unit GUID.
- Added CursorPosition() function that returns world XYZ coordinates of mouseover.
- Added GetWorldLocMapPosition(continent, x, y) that returns map XY coordinates from a world XYZ coordinate and continent index.
- Added GetMapPositionWorldLoc(continentIndex, zoneIndex, mapX, mapY) that returns world XYZ coordinates from map XY coordinates.
- Added GetMapBoundaries(continentIndex, zoneIndex) that returns left, right, top and bottom boundaries of a map.
- Added IsSwimming(), IsMounted(), isIndoors() functions to return the status of the player.
- Added GetSpeed() function to return runSpeed, swimSpeed of the player in yards per second (7 yards = 100% movement speed)

### 15/07/2026: 2.1
- Improvements to NameplateMotion Smart Spread mode.
- Added GetWeaponEnchantID(unit). Returns mainhand and offhand temporary enchant ID.
- Added GetSendMailItemLink(). Returns Hyperlink for the item in Sending Mail slot.
- Added GetInboxItemLink(itemIndex). Returns Hyperlink for the item in Mailbox slot.
- Added GetQuestID(questIndex). Returns ID of the quest in the questlog slot.
- Added GetQuestLink(questID). Returns Hyperlink for the quest ID from client cache. If no entry in cache, returns nil and fills the cache from server (fires event QUEST_LOG_UPDATE)
- Tooltip SetHyperlink now supports quest hyperlinks with information from client cache. If no entry in cache, fills the cache from server.
Generate Hyperlinks with GetQuestLink or get them directly from Wowhead.

### 16/07/2026: 2.2
- More Improvements to NameplateMotion Smart Spread mode, added Compact Spread mode.
- Refactored Quest ID & link functions to three distinct functions with more descriptive & less generic names, should solve most addon compatibility:
GetQuestIDForLogIndex(questIndex); GetQuestLinkForLogIndex(questIndex); GetQuestLinkForID(questID)

### XX/XX/XXXX: 3.0 **COMING SOON, [join Premium supporters](https://ko-fi.com/balakesuperwow) for early access & behind the scenes info**
- More code refactoring & performance boosts.
- Full HD Text support. Requires DXVK (comes bundled with VanillaFixes). The module can be turned off by adding the line "superwow.disableHDText = True" to dxvk.conf in game directory.
- With HD Text comes the new CVars: OutlineNamesText, OutlineWorldText, ShadowWorldText.
- Function Change: GetPlayerBuff by default **NO LONGER** shows hidden buffs. The function's filter argument (in addition to HELPFUL | HARMFUL | CANCELABLE | NOT_CANCELABLE ) now also accepts SHOWALL as a conditional argument. It re-introduces hidden buffs to the function. If you want selective hidden buffs search, use this function.
- New CVar: ForceShowAuras, this makes GetPlayerBuff's filter argument ALWAYS treat SHOWALL as true. If you want hidden buffs back, turn this on.
- New Function: GetQuestgiverQuestID() Returns questID of the questgiver NPC (or questgiver item) you are currently interacting with.
- New Function: AppendText("filename", "textToAppend"), much more efficient than ImportText for small edits (Still recommend caching things and only appending them to file in batches)
- New Events: SUPERWOW_KEY_DOWN, SUPERWOW_KEY_UP, SUPERWOW_MOUSE_DOWN, SUPERWOW_MOUSE_UP, SUPERWOW_MOUSE_WHEEL. Arg1: Key or button.

- New Functions: GetNumSoundDrivers() returns number of Sound Drivers, GetLoadedSoundDriver() returns index of the currently used Sound Driver, GetSoundDriverName(index) returns name of the Sound Driver index, GetSoundDevices() returns everything at once.
- New CVar: SoundDriver, used at game start to load a specific SoundDriver. Requires full Game Restart to change.

- New Function: PingLocation(x, y, z [, PingVisual]). PingVisual : 0 to 4, default is 0. Draws one of 5 different ping visuals in your world. Share information with other players through Addon messages to create a complete Pinging communication system.

- Complete rework of coordinates functions:
The game uses three different types of coordinates
- - World coordinates { worldX, worldY, worldZ, worldID} refer to the raw coordinates of a point and which world it belongs to. Worlds are "instances", open world included. This means open world Kalimdor is a world, open world Eastern Kingdoms is a world, Blackrock Depths is a world, Molten Core is a world.
- - Map coordinates { ContinentIndex, ZoneIndex, mapX, mapY } refers to 0-1.0 coordinates of a point in a specific map.
- - Screen Coordinates { ScreenX, ScreenY } refers to coordinates of a point on your screen. The same coordinates used by the lua API and its frames.
- - These different coordinates can be converted between each other with the new functions: 
- - - worldX, worldY, worldZ, worldID = GetScreenToWorldCoords(screenX, screenY)
- - - screenX, screenY = GetWorldToScreenCoords(worldX, worldY, worldZ)
- - - worldX, worldY, worldZ, worldID = GetMapToWorldCoords(continentIndex, zoneIndex, mapX, mapY)
- - - mapX, mapY (of the currently selected map) = GetWorldToMapCoords(x, y [, worldID]) -- if no worldID, assumes the player's current worldID.

- New Function: IsKeyDown("KeyName") returns 1 if the key is currently being held (example args: "SHIFT", "D", "ENTER")

- Combat Logging now additionally logs to individual Session Files. Can be turned off with CVar "CombatLogSessions"

- New Functions: GetFullLocalTime() and GetFullServerTime() both return year, month, day, weekday, hour, minute, second, millisecond.

- New Functions: FocusUnit("unit") and ClearFocus(), as well as event PLAYER_FOCUS_CHANGED that fires on Focus change. Focus is now accepted as a unit identifier for lua Functions, and can appended with suffixes "target", "pet", "owner" like all other unit identifiers.

- New Event: [SUPERWOW_COMBAT_LOG_EVENT](https://github.com/balakethelock/SuperWoW/wiki/SUPERWOW_COMBAT_LOG_EVENT-wip)

- New CVar: "XPText" Toggles off world XP Text.

- New CVar: "ForceTimeOfDay" Sets world to a specific daytime (Visual change only)

- New CVar: "SkyOffset" Enables [immersive sky mode](https://www.youtube.com/watch?v=die4OURQ6e8).

- New SuperAPI setting: Extended Horizons uncaps Fog, Farclip and HorizonFarClip.

- New CVar: "ModernSwimming" Enables modern wow swimming motions (Jump to go up, sit to go down)

- New CVar: "NameplateVerticalSpacing" changes height of unit Nameplates for custom nameplate Motion algorithms

- Fixed client glitch where it thinks keyboard turning counts as moving & cancels player channels.