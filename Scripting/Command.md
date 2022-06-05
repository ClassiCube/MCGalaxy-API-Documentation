### Summary

The `Command` class performs action(s) based on player input

Remarks:
- For simple commands derive from `Command`
- For more advanced commands that require knowing how the command is being executed 
(e.g. from a Message Block) or with what permissions the command is being executed (to behave properly with `/SendCmd`), derive from `Command2`

## API

### Required properties & methods

#### `abstract string name { get; }`

The full name of this command (e.g. `"Copy"`)

#### `abstract string type { get; }`

The type/group of this command (see `CommandTypes` class)

Remarks:
- The available types/groups in the `CommandTypes` class are
- * Building, Chat, Economy, Games, Information, Moderation, Other, World

#### `abstract void Help(Player p)`

Informs the given player what this command does and how to use it

#### `abstract void Use(Player p, string message)`
       
Performs the action(s) of this command using the given arguments

### Common properties & methods

#### `virtual string shortcut { get; }`

The shortcut/short name of this command (e.g. `"c"`)

Default: `""`

#### `virtual bool museumUsable { get; }`

Whether this comand can be used in museums (private readonly [Levels](/Level/Level.md))

Default: `true`

Remarks:
- Level altering (e.g. places a block) commands should return false

#### `virtual LevelPermission defaultRank`

The default minimum rank that is required to use this command

Default: `LevelPermission.Guest`

Remarks:
- You can use one of the default rank permission levels from the `LevelPermission` class:
	- Guest, Builder, AdvBuilder, Operator, Admin, Owner
- Alternatively you can use an explicit permission level (e.g. `(LevelPermission)15;`)
        
### Additional properties & methods

#### `virtual void Help(Player p, string message) { Help(p); Formatter.PrintCommandInfo(p, this); }`
        
#### `virtual CommandPerm[] ExtraPerms { get { return null; } }`
#### `virtual CommandAlias[] Aliases { get { return null; } }`
        
#### `virtual bool SuperUseable { get { return true; } }`
#### `virtual bool MessageBlockRestricted { get { return false; } }`
#### `virtual bool UseableWhenFrozen { get { return false; } }`
#### `virtual bool LogUsage { get { return true; } }`
#### `virtual bool UpdatesLastCmd { get { return true; } }`

## Examples

```CSharp
// simple example of a command
using System;

namespace MCGalaxy 
{
	public class CmdSimple : Command
	{
		public override string name { get { return "Simple"; } }
		public override string type { get { return "other"; } }
		public override LevelPermission defaultRank { get { return LevelPermission.Guest; } }

		// A simple command that messages you 'Hello World!' when you type '/Simple'
		public override void Use(Player p, string message) {
			p.Message("Hello World!");
		}

		public override void Help(Player p) {
			p.Message("/Simple - Messages you 'Hello World!'");
		}
	}
}
```

```
