### Summary

The `Level` class represents a world/map that is loaded into memory

General guidelines:
- Keep in mind that some methods update level state without broadcasting the changes to the players currently in the level, while other methods will both update the level state and also broadcast the changes to players

## API

### Fields/Properties

#### `ushort Width` 

The width of this level (Number of blocks across in X dimension)

#### `ushort Height`

The height of this level (Number of blocks tall in Y dimension)

#### `ushort Length`

The length of this level (Number of blocks across in Z dimension)

### Static methods

### Examples

