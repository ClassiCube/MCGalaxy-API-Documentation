### Summary

The `PlayerExtList` class manages a **case-insensitive** list of names and simple associated data in a threadsafe manner

General guidelines:
- Use the return value from `Add` and `Remove` to detect whether a name was actually added or removed
(Don't write code like `if (list.Contains(name)) { list.Remove(name); ..`, just do `list.Remove(name);` )
- Although this class is intended for player names, it can also be used for level names etc

### Data related methods

#### `void Update(string name, string data)`

Updates (or creates) the data associated with the given name

#### `bool Contains(string name)`

Returns whether the given name is case-insensitively included in this list

#### `string FindData(string name)`

Retrieves the data associated with the given name in this list

Return value
- null if the name was not case-insensitively found in the list
- the associated data as a string otherwise

#### `bool Remove(string name)`

Attempts to remove the given name (and associated data) from the list

Return value
- true if the name was case-insensitively removed from the list

### I/O methods

####`void Save()`

Saves the list of names and associated data to disc

#### `static PlayerExtList Load(string path)`

Returns a `PlayerExtList` object initialised with the list of names and associated data loaded from the given path

Return value:
- A new `PlayerExtList` instance on success, throws an exception on failure

### Examples

```CSharp
PlayerExtList list = PlayerExtList.Load("text/mylist.txt");
list.Add("Player1", "A B C");
list.Remove("Player2");
list.Save();
```