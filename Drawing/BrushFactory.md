### Summary

The `BrushFactory` class is responsible for parsing input from a player to create a [brush](Drawing/Brush.md)

Some visual examples of brushes
[TODO sample image]

Remarks
- See also (BrushFactory.md)

## API

### Properties

#### `abstract string Name { get; }`

Returns the name of this brush factory


#### `abstract string Help { get; }`

Returns an array containing a summary of the possible player input that can be provided

### Methods

#### `abstract Brush Construct(BrushArgs args)`

Parses input from the given player to return a new [Brush](Drawing/Brush.md)

Remarks:
- Returns `null` when the input provided by the player is invalid
- BrushArgs is a class consisting of the following three fields:
	* Player
	* Block
	* Message

## Examples