### Summary

The `Plugin` class provides the foundation for more advanced modifications/custom functionality

## API

### Required properties & methods

#### `abstract string name { get; }`

The full name of this plugin (e.g. `"DatExporter"`)

#### `abstract string MCGalaxy_version { get; }`

The minimum server software version this plugin is compatible with

Examples: `"1.9.3.8"`

#### `abstract void Load(bool auto)`

Where this plugin should hook into events, initalise states/resources, etc

Remarks:
- `auto` is `true` when the plugin is being automatically loaded (e.g. on server startup)
- `auto` is `false` when the plugin is being manually loaded (e.g. via `/plugin load`)

#### `abstract void Unload(bool auto)`

Where this plugin should unhook into events, dispose states/resources, etc

Remarks:
- `auto` is `true` when the plugin is being automatically unloaded (e.g. on server shutdown)
- `auto` is `false` when the plugin is being manually unloaded (e.g. via `/plugin unload`)

### Optional properties & methods

#### `virtual int build { get; }`

The version of this plugin (e.g. `200`)

Default: `0`

#### `virtual string welcome { get; }`

The message shown in server logs when this plugin is loaded

Default: `""`

#### `virtual string creator { get; }`

The name of the author of this plugin

Default: `""`

#### `virtual bool LoadAtStartup { get; }`

Whether this plugin's `Load` method is automatically called upon server startup

Default: `true`

#### `virtual void Help(Player p)`

Informs the given player what this plugin does

Default: Messages the given player `No help is available for this plugin.`

## Examples

TODO
