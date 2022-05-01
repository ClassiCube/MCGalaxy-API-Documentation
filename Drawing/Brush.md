### Summary

The `Brush` class is responsible for determining the output blocks from most [draw operations](/Drawing/DrawOp.md)

Some visual examples of brushes
[TODO sample image]

Remarks
- See also [BrushFactory](/Drawing/BrushFactory.md) class that parses player input to create a Brush

## API

### Properties

#### `abstract string Name { get; }`

Returns the name of this brush

### Methods

#### `virtual void Configure(DrawOp op, Player p)`

Performs additional configuration/calculations for the given draw operation

Remarks:
- Most brushes do not need to override this method

Examples:
- `ReplaceBrush` changes `op.Flags` to `BlockDBFlags.Replaced` (so that /b shows 'Replaced' instead of 'Drawn')
- `CloudyBrush` attempts to calculate appropriate noise thresholds based on the draw operation's boundaries

#### `abstract BlockID NextBlock(DrawOp op)`

Returns the output block based on the draw operation's current state (usually this just means the current coordinates)

Remarks:
- If no block should be output, return `Block.Invalid`

## Examples

```CSharp
public sealed class NeapolitanBrush : Brush
{
	public override string Name { get { return "Neapolitan"; } }
        
	public override BlockID NextBlock(DrawOp op) {
		int width     = op.Max.X - op.Min.X;
		int oneThirdX = op.Min.X + width / 3;
		int twoThirdX = op.Min.X + width * 2 / 3;
			
		if (op.Coords.X <= oneThirdX) {
			return Block.White;
		} else if (op.Coords.X <= twoThirdX) {
			return Block.Brown;
        } else {
			return Block.Pink;
		}
    }
}
```
[TODO output example image]