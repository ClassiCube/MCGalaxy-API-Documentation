### Summary

The `BrushFactory` class is responsible for parsing input from a player to create a [Brush](/Drawing/Brush.md)

Some visual examples of brushes
[TODO sample image]

Remarks
- The `BrushFactory` class is separate from the `Brush` class, because although rare,
  some `BrushFactory` types return different `Brush` types depending on the player input (See `CheckeredBrushFactory` for example)

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