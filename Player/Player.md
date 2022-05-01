### Summary

The `Player` class represents either an online player or a virtual player (e.g. console)

General guidelines:
- Keep in mind that virtual players have some restrictions 
- Prefer Set/Update methods instead of directly setting fields

### Virtual players

Virtual players refers to any players that aren't an online/human player

Some examples of virtual players
- The server console (accessible via `Player.Console`)
- Executing commands from a relay bot (e.g. a user ran `.x help me` from IRC)

[TODO level restrictions]
[TODO IsSuper]

## API

### Identification Fields

#### `int DatabaseID`

Unique and persistent ID number associated with the name of this player

Remarks
- This field is valid even for virtual players

### Network fields

#### `IGameSession Session`

The [IGameSession](/Network/IGameSession.md) object for this online player's current session

Remarks
- For virtual players **this field is null**
- Generally methods in this class should be used instead of using the `Session` field directly

#### `INetSocket Socket`

The `INetSocket` object for this online player's network socket

Remarks
- For virtual players **this field is null**
- Generally methods in this class should be used instead of using the `Socket` field directly.
- Be careful when using `Socket`, because it **allows you to send invalid data to the client**

### Drawing fields

#### `string BrushName`

The name of the [Brush](/Drawing/Brush.md) this player is currently using

Remarks
- Cannot be null, defaults to `"Normal"`


####`string DefaultBrushArgs`

The default arguments passed to the [Brush](/Drawing/Brush.md) when the player does not provide explicit arguments to a drawing command

Remarks
- Cannot be null, defaults to `""`


#### `Transform Transform`

The [Transform](/Drawing/Transform.md) instance this player is currently using

Remarks
- Cannot be null, defaults to `NoTransform.Instance`


### Instance methods

### Static methods

## Examples

