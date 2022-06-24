### Summary

The `Block` class provides utility functionality relating to Block IDs and Block names

Remarks
- Block IDs in MCGalaxy are unsigned 16 bit integers. 
To distinguish these from other unsigned 16 bit integers, typically `using BlockID = System.UInt16;` is inserted at the top of files

## Block IDs

Because of historical reasons, not all block IDs that you see in the client have the same block ID in MCGalaxy.
(Because Block IDs 66-255 were already used for special blocks such as physics blocks, portals, etc)

| Server Block ID | Group | Raw Block ID
|-----------------|-------|-------------
| 0-65  | Classic & CPE blocks | 0-65
| 66-255 | Special blocks | (none)
| 256-321 | (unused) | 0-65
| 322-511 | Custom blocks #1 | 66-255
| 512-767 | Custom blocks #2 | 256-511
| 768-1023 | Custom blocks #3 | 512-767

---

### Raw block IDs -> Server block IDs
- It is recommended to use `Block.FromRaw()` to convert from raw Block IDs to server Block IDs for clarity
- Manual conversion is relatively straightforward though - just add 256 if the raw block ID is over 65

### Server block IDs -> Raw block IDs
- It is recommended to use `Block.ToRaw()`
- Note however that you **must** ensure that the block ID is not a special block - use `Block.Convert` first if necessary

## API

### Fields

#### `const byte CLASSIC_MAX_BLOCK`

Highest block ID supported in Classic (Obsidian)

#### `const byte CPE_MAX_BLOCK`

Highest block ID supported in Classic + CPE custom blocks (Stone Bricks)

#### `static readonly int ExtendedCount`

Total number of blocks supported by the current server

Remarks
- For standard/normal MCGalaxy this is 512
- For TEN_BIT_BLOCKS MCGalaxy this is 1024

### Conversion Methods

- Because level only blocks can be defined, results from this function can change depending on the player's level and should never be cached

#### `static string GetName(Player p, BlockID block)`

Returns the name of the given block

Remarks:
- A [Player](/Player/Player.md) instance is required because block names can differ per-level
- Results from this function should never be cached (as it can change per-level)
- Blocks IDs that are not defined in the current level will return raw block ID instead

### Validation/Parsing Methods

#### `static BlockID Parse(Player p, string input)`

Parses the given input containing either a block ID, block name, or block alias

Remarks:
- Returns `Block.Invalid` if the input could not be parsed
- A [Player](/Player/Player.md) instance is required because defined blocks can differ per-level
- Results from this function should not be cached (as it can change per-level)

#### `static BlockID Convert(BlockID block)`

Converts special block IDs to the block IDs that clients would see in the world

Remarks:
- Unrecognised special block IDs **are not converted**

Examples:
- `Door_Wood` is converted to `Wood`

## Examples

TODO