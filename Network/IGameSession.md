### Summary

The `IGameSession` class abstracts a network session with a game (usually Minecraft Classic compatible) client

General guidelines:
- When possible, higher level methods in the [Player] class should be used instead

## API

### Fields

#### `byte ProtocolVersion`

The network protocol version supported by the game client

Remarks
- For Minecraft Classic 0.30, the protocol version is `7`

#### `BlockID MaxRawBlock`

The highest raw block ID supported by the game client

Remarks
- For vanilla Minecraft Classic client, highest supported raw ID is `49` (obsidian)
- For ClassiCube client, highest supported raw ID might be `49`, `65`, `255` or `767`

#### `int ID`

Temporary unique ID number for this network session

Remarks
- When a client logs out and then logs in again, the session `ID` will be different

### Methods


#### `string ClientName()`

Gets the name of the software the client is using

Remarks
- Software names **should not** be used to determine client feature support
