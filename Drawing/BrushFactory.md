### Summary

The `BrushFactory` class is responsible for parsing input from a player to create a [Brush](/Drawing/Brush.md)

[TODO sample image]

Remarks
- The `BrushFactory` class is separate from the `Brush` class, because although rare,
  some `BrushFactory` types return different `Brush` types depending on the player input (See `CheckeredBrushFactory` for example)
- `BrushFactory` instances are essentially singletons, therefore you should not use any modifiable class level fields 
  (to avoid running into rare issues where two players both try to use the same `BrushFactory` instance at the exact same time)

## API

### Properties

#### `abstract string Name { get; }`

Returns the name of this brush factory

#### `abstract string Help { get; }`

Returns an array summarising the possible player input that can be provided

### Methods

#### `abstract Brush Construct(BrushArgs args)`

Parses input from the given player to return a new [Brush](/Drawing/Brush.md)

Remarks:
- Returns `null` when the input provided by the player is invalid
- `BrushArgs` is a class consisting of the following three fields:
	* Player - The [Player](/Player/Player.md) that is attempting to create a brush
	* Message - The raw arguments provided for input (including spaces)
	* Block - The block ID of the block the player is currently holding

## Examples

```CSharp
using MCGalaxy;
using MCGalaxy.Commands;
using MCGalaxy.Drawing.Brushes;
using MCGalaxy.Drawing.Ops;
using BlockID = System.UInt16;

public class FoodBrushFactory : BrushFactory
{
	public override string Name { get { return "Food"; } }
	public override string[] Help { get { return HelpString; } }
	
	static string[] HelpString = new string[] {
		"&TArguments: pumpkin",
		"&HDraws an alternating pattern of Orange and Black.",
		"&TArguments: candy",
		"&HDraws an alternating pattern of White and Red.",
	};
	
	public override Brush Construct(BrushArgs args) {
		BlockID block1, block2;
		
		if (args.Message == "pumpkin") {
			block1 = Block.Orange;
			block2 = Block.Black;
		} else if (args.Message == "candy") {
			block1 = Block.Red;
			block2 = Block.White;
		} else {
			args.Player.Message("Arguments must be either 'pumpkin' or 'candy'");
			return null;
		}

		// Check user is actually allowed to use the blocks
		if (!CommandParser.IsBlockAllowed(args.Player, "draw with", block1)) return null;
		if (!CommandParser.IsBlockAllowed(args.Player, "draw with", block2)) return null;
		
		return new CheckeredBrush(block1, block2);
	}
}

...

BrushFactory.Brushes.Add(new BrushFactory());
```

[TODO add remarks about how should use IsBlockAllowed/GetBlockIfAllowed]
[TODO add staic fields/methods]