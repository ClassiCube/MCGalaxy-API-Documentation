### Summary

The `DrawOp` class is responsible for taking one or more input coordinates/marks and producing output blocks

Remarks
- Draw operations do not only have to draw shapes (ReplaceDrawOp, RestoreSelectionDrawOp TODO)

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

#### `abstract string Name { get; }`

Returns the name of this draw operations

#### `abstract long BlocksAffected(Level lvl, Vec3S32[] marks)`

Estimates the total number of blocks that this draw operation may affect

Remarks:
- This should be implemented as a simple estimate (shouldn't perform any complex calculations)
- This is an upper bound/worst case estimate (assumes that all potentially affected blocks will actually be changed)

#### `abstract void Perform(Vec3S32[] marks, Brush brush, DrawOpOutput output)`

Performs the draw operation (actually outputs the block using `output`)

#### `void Setup(Player p, Level lvl, Vec3S32[] marks)`

Initialises/Prepares the state of this draw operation from the given arguments

Remarks:
- Initialises `Player`, `Level`, `Min`, `Max` etc fields

##### `protected DrawOpBlock Place(ushort x, ushort y, ushort z, Brush brush)`

Returns a `DrawOpBlock` with the given x,y,z and block calculated by the given brush
        
#### `protected DrawOpBlock Place(ushort x, ushort y, ushort z, BlockID block)`

Returns a `DrawOpBlock` with the given x,y,z and the given block type
        
#### `protected Vec3U16 Clamp(Vec3S32 pos)`

Constrains/Clamps the given coordinates to lie within the Level's boundaries

## Fields

#### Vec3S32 Min

The minimum coordinates of the bounds of this draw operation

Remarks:
- This is the smallest X/Y/Z from all of the input coordinates/marks

#### Vec3S32 Max

The maximum coordinates of the bounds of this draw operation

Remarks:
- This is the largest X/Y/Z from all of the input coordinates/marks

#### DrawOpBlock Coords

The coordinates of the current block being processed by this draw operation

Remarks:
- This field is mainly intended for use by [Brushes](/Drawing/Brush.md)

#### Player Player

The player that is executing this draw operation

#### Level Level

The Level that this draw operation is being performed on

#### ushort Flags

The BlockDB change type for blocks affected by this draw operation

[TODO /b example image]

Remarks:
- This field should be set in the constructor of the draw operation class
- The supported flag values from the `BlockDBFlags` class are
-	* Drawn, Replaced, Pasted, Cut, Filled, Restored, UndoOther, UndoSelf, RedoSelf, FixGrass

##### bool AffectedByTransform

Whether the output of this draw operation can potentially be transformed (e.g. scaled or rotated) by a [Transform](/Drawing/Transform.md)

- Draw operations whose output must not be transformed (e.g. Replace, Restore, UndoPlayer) should set this field to false

## Examples

```CSharp
using MCGalaxy;
using MCGalaxy.Drawing;
using MCGalaxy.Drawing.Brushes;
using MCGalaxy.Drawing.Ops;
using MCGalaxy.Maths;

public class OddBoxDrawOp : DrawOp
{
	public override string Name { get { return "OddBox"; } }
	
	public override long BlocksAffected(Level lvl, Vec3S32[] marks) {
		long width  = Max.X - Min.X + 1;
		long height = Max.Y - Min.Y + 1;
		long length = Max.Z - Min.Z + 1;
		
		// NOTE: strictly speaking, the marks should be examined to calculate the number of rows
		// that will actually get drawn - but it's simpler to just always assume the worst case
		return (width / 2 + 1) * height * length;
	}
	
	public override void Perform(Vec3S32[] marks, Brush brush, DrawOpOutput output) {
		//  Min contains the smallest X,Y,Z of the marks, so can be used as lower left corner of the box
		//  Max contains the largest X,Y,Z of the marks, so can be used as upper right corner of the box
		// Both coordinates are then constrained/clamped to lie within the boundaries of the level
		Vec3U16 min = Clamp(Min), max = Clamp(Max);
		
		for (ushort y = min.Y; y <= max.Y; y++)
			for (ushort z = min.Z; z <= max.Z; z++)
				for (ushort x = min.X; x <= max.X; x++)
		{
			// skip even coordinates on X axis
			if ((x % 2) == 0) continue;
			
			// use the given brush to determine the type of block to place at x,y,z
			// then actually output the block by invoking 'output' callback function
			output(Place(x, y, z, brush));
		}
	}
}

```
[TODO output example image]
