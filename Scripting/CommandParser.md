### Summary

The `CommandParser` class provides helper methods for parsing player input

General guidelines:
- It is **highly recommended** that this class is used to parse player input over using `int.Parse` etc
- If the input failed to be parsed, all of the methods listed below will automatically message the player the reason why
- Methods only assign `result` when the input is successfully parsed

## API

### Methods

#### `static bool GetBool(Player p, string input, ref bool result)`

Attempts to parse the given input as a boolean

#### `static bool GetEnum<TEnum>(Player p, string input, string argName, ref TEnum result)`

Attempts to parse the given input as an `Enum` member


#### `static bool GetTimespan(Player p, string input, ref TimeSpan span, string action, string defUnit)`

Attempts to parse the given input as a `Timespan` using shorthand form

#### `static bool GetInt(Player p, string input, string argName, ref int result)`

Attempts to parse the given input as an int (32 bit integer)

#### `static bool GetInt(Player p, string input, string argName, ref int result, int min, int max)`

Attempts to parse the given input as an int that lies between `min` and `max`

#### `static bool GetReal(Player p, string input, string argName, ref float result)`

Attempts to parse the given input as a float (decimal number)

#### `static bool GetReal(Player p, string input, string argName, ref float result, float min, float max)`

Attempts to parse the given input as a float that lies between `min` and `max`

#### `static bool GetByte(Player p, string input, string argName, ref byte result)`

Attempts to parse the given input as a byte (8 bit unsigned integer)

#### `static bool GetByte(Player p, string input, string argName, ref byte result, byte min, byte max)`

Attempts to parse the given input as a byte that lies between `min` and `max`

#### `static bool GetUShort(Player p, string input, string argName, ref ushort result);`

Attempts to parse the given input as a ushort (16 bit unsigned integer)

#### `static bool GetUShort(Player p, string input, string argName, ref ushort result, ushort min, ushort max)`

Attempts to parse the given input as a ushort that lies between `min` and `max`

#### `static bool GetHex(Player p, string input, ref ColorDesc result)`

Attempts to parse the given input as a hex color

#### `static bool GetCoords(Player p, string[] args, int argsOffset, ref Vec3S32 coords)`

Attempts to parse the 3 given inputs as coordinates (`args[argsOffset]`, `args[argsOffset + 1]`, `args[argsOffset + 2]`)

Remarks:
- `coords` should be properly initialised (`GetCoords` supports specifying that input is relative to current value)

#### `static bool GetBlock(Player p, string input, out BlockID block)`

Attempts to parse the given argument as either a block name or a block ID

#### `static bool IsBlockAllowed(Player p, string action, BlockID block)`

Checks whether the given player is allowed to place/modify/delete the given block

#### `static bool GetBlockIfAllowed(Player p, string input, string action, out BlockID block)`

Attempts to parse the given argument as either a block name or a block ID

Also checks whether the given player is allowed to place/modify/delete the given block

## Examples

```CSharp
void BoolExample(Player p, string input) {
	bool value = false;
	if (!CommandParser.GetBool(p, input, ref value)) return;
	
	p.Message("Success:" + value);
}

// if input is 'true', messages the player "Success: true"
// if input is "ABCD", messages the player 
//		"'ABCD' is not a valid boolean." 
//		"Value must be either 1/yes/on or 0/no/off"
```

```CSharp
enum NameType { User, Email }
void EnumExample(Player p, string input) {
	NameType value = NameType.User;
	if (!CommandParser.GetEnum(p, input, "Name", ref value)) return;
	
	p.Message("Success: " + value);
}

// if input is "USER", messages the player "Success: User"
// if input is "ABCD", messages the player "Name must be one of the following: User, Email"

```

```CSharp
void IntExample(Player p, string input) {
	int value = 0;
	if (!CommandParser.GetInt(p, input, "Arg1", ref value, 1, 1024)) return;
	
	p.Message("Success: " + value);
}

// if input is '10', messages the player "Success: 10"
// if input is '-1', messages the player "Arg1 must be between 1 and 1024"
// if input is "AB", messages the player "'AB' is not a valid integer"
```

```CSharp
void BlockExample(Player p, string input) {
	BlockID block;
	if (!CommandParser.GetBlockIfAllowed(p, input, "draw with", out block)) return;
	
	p.Message("Success: " + value);
}

// if input is '3', messages the player "Success: 3"
// if input is 'dirt', messages the player "Success: 3"
// if input is 'abcd', messages the player "There is no block 'abcd'"
// if player can't use dirt, messages the player e.g. "Only Owner+ can draw with Dirt"
```