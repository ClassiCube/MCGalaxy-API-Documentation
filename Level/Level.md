### Summary

The `Level` class represents a world/map that is loaded into memory

General guidelines:
- Keep in mind that some methods update level state without broadcasting the changes to the players currently in the level, 
  while other methods will both update the level state and also broadcast the changes to players

## API

### Fields/Properties

#### `ushort Width` 

The width of this level (Number of blocks across in X dimension)

#### `ushort Height`

The height of this level (Number of blocks tall in Y dimension)

#### `ushort Length`

The length of this level (Number of blocks across in Z dimension)

### Block methods

#### `int PosToInt(ushort x, ushort y, ushort z)`
Converts the given x,y,z coordinates to a coordinates index

Remarks:
- Returns -1 if coordinates outside this level's boundaries are given

#### `void IntToPos(int pos, out ushort x, out ushort y, out ushort z)`
Converts the given coordinates index to x,y,z coordinates

Remarks:
- **Undefined behaviour** if given coordinates index is invalid

#### `bool IsValidPos(int x, int y, int z)`
Whether the given coordinates lie within this level's boundaries

#### `BlockID FastGetBlock(int index)`
Gets the block at the given coordinates index

Remarks:
- **Undefined behaviour** if the coordinates are outside the level boundaries

#### `BlockID FastGetBlock(ushort x, ushort y, ushort z)`
Gets the block at the given x,y,z coordinates

Remarks:
- **Undefined behaviour** if the coordinates are outside the level boundaries

#### `BlockID GetBlock(ushort x, ushort y, ushort z)`
Gets the block at the given x,y,z coordinates

Remarks:
- Returns `Block.Invalid` if the coordinates are outside the level boundaries

#### `BlockID GetBlock(ushort x, ushort y, ushort z, out int index)`
Gets the block at the given x,y,z coordinates, and additionally returns the corresponding coordinates index

Remarks:
- Returns `Block.Invalid` if the coordinates are outside the level boundaries

#### `void SetBlock(ushort x, ushort y, ushort z, BlockID block)`
Sets the block at the given x,y,z coordinates

Remarks:
- Does nothing if the coordinates are outside the level boundaries


### Examples

