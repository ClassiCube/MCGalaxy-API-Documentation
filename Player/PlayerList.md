### Summary

`PlayerList` is a class that manages a **case-insensitive** list of names in a threadsafe manner

General guidelines:
- Use the return value from `Add` and `Remove` - don't write code like `if (list.Contains(name)) { list.Remove(name); ..`
- Although this class is intended for player names, it can also be used for level names etc

### Instance methods

#### Add

`bool Add(string name)`

Attempts to add the given name to the list

Return value
- true if the name was added to the list, false if the name was already case-insensitively in the list

#### Remove

`bool Remove(string name)`

Attempts to remove the given name from the list

Return value
- true if the name was case-insensitively removed from the list

#### Contains

`bool Contains(string name)`

Returns whether the given name is case-insensitively included in this list

#### Save

`void Save()`

Saves the list of names to disc

(Each name is written on a separate line)

### Examples

