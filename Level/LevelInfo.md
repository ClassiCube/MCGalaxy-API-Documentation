### Summary

The `LevelInfo` class provides utility functionality for all maps and for maps currently loaded into memory as [Level](/Level/Level.md)s

TODO: reword this to be simpler

## API

### Loaded levels list
        
#### `static VolatileArray<Level> Loaded`

The list of levels currently loaded in memory

TODO: VolatileArray documentation

#### `static Level FindExact(string name)`

Returns the level currently loaded in memory whose name caselessly equals the given input

Return value:
	- A [Level](/Level/Level.md) instance if a match is found
	- `null` if no match is found
        
#### `static void Add(Level lvl)`

Adds the given [Level](/Level/Level.md) to the list of loaded levels

Remarks:
	- Raises OnLevelAddedEvent
        
#### `static void Remove(Level lvl)`

Removes the given [Level](/Level/Level.md) from the list of loaded levels

Remarks:
	- Raises OnLevelRemoved event

### All levels list
        
#### `static string[] AllMapFiles()`

Retrieves the list of all maps paths

Examples:
	- `[ "levels/abc.lvl", "levels/xyz.lvl" ]`
        
#### `static string[] AllMapNames()`

Retrieves the list of all maps paths

Examples:
	- `[ "abc", "xyz" ]`
        
#### `static bool MapExists(string name)`

Whether a map with the given name was found on disc in `levels` folder
        

### Map backups

#### `static int LatestBackup(string map)`

Returns the largest numerically named backup of the given map

Remarks:
	- Returns `0` if there are no numerically named backups for the given backup
        
#### `static string NextBackup(string map);`

Returns the ID to use for the next automatic backup of the given map
        
### Map information

#### `static LevelConfig GetConfig(string map)`

Returns a [[LevelConfig](/Level/LevelConfig.md) containing the properties/settings of the given map

#### `static bool IsRealmOwner(Level lvl, string name)`

Whether the given user is considered a realm owner of the given [Level](/Level/Level.md)

Remarks:
	- Realm owners are able to use `/Realm (/os)`
        
#### `static bool IsRealmOwner(string map, LevelConfig cfg, string name)`

Whether the given user is considered a realm owner of the given map

Remarks:
	- Realm owners are able to use `/Realm (/os)`