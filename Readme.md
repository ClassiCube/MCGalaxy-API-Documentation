This repository serves as a starting point for understanding MCGalaxy's API by documenting and providing examples for the essential classes

### Blocks
- [Block](/Block/Block.md)
- [BlockDefinition](/Block/BlockDefinition.md)
- [BlockProps](/Block/BlockProps.md)

### Commands
- [Command](/Scripting/Command.md) - Performs an action based on player input
- [CommandParser](/Scripting/CommandParser.md) - Helpers for parsing player input

### Drawing
- [Brush](/Drawing/Brush.md) - Determines the blocks output from most draw operations
- [BrushFactory](/Drawing/BrushFactory.md) - Parses player input to create a Brush
- [DrawOp](/Drawing/DrawOp.md) - Produces blocks from an array of coordinates (e.g. a box)
- [DrawOpPerformer](/Drawing/DrawOpPerformer.md)

### Events
TODO

### Level
- [Level](/Level/Level.md) - Array of blocks and associated data loaded in memory
- [LevelInfo](/Level/LevelInfo.md)
- [LevelActions](/Level/LevelActions.md)
- [LevelOperations](/Level/LevelOperations.md) - High level methods for manipulating levels

### Scripting
- [Plugin](/Scripting/Plugin.md)

### Player
- [Group](/Player/Group.md)
- [Player](/Player/Player.md) - Represents an online or virtual (e.g. console) player
- [PlayerInfo](/Player/PlayerInfo.md)
- [PlayerActions](/Player/PlayerActions.md)
- [PlayerOperations](/Player/PlayerOperations.md) - High level methods for manipulating players

### Player data
- [PlayerList](/Player/PlayerList.md) - List of names
- [PlayerExtList](/Player/PlayerExtList.md) - List of names and associated data
- PlayerMetaList

### Server
