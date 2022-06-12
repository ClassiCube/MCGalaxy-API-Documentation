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

Remarks:
- A [Player](/Player/Player.md) instance is required because block names can differ per-level
- Results from this function should never be cached

### Validation/Parsing Methods

#### `static BlockID Parse(Player p, string input)`



#### `static BlockID Convert(BlockID block)`

Converts special block IDs to the block IDs that clients see in the world

Remarks:
- Unrecognised special block IDs **are not converted**

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
