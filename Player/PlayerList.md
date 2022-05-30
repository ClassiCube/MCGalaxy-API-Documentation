### Summary

`PlayerList` class manages a **case-insensitive** list of names in a threadsafe manner

General guidelines:
- Use the return value from `Add` and `Remove` - don't write code like `if (list.Contains(name)) { list.Remove(name); ..`
- Although this class is intended for player names, it can also be used for level names etc

## API

### Data related methods

#### `bool Add(string name)`

Attempts to add the given name to the list

Return value
- `true` if the name was added to the list, `false` if the name was already case-insensitively in the list

#### `bool Remove(string name)`

Attempts to remove the given name from the list

Return value
- `true` if the name was case-insensitively removed from the list

#### `bool Contains(string name)`

Returns whether the given name is case-insensitively included in this list

### I/O methods

#### `void Save()`

Saves the list of names to disc

#### `static PlayerList Load(string path)`

Returns a `PlayerList` object initialised with the list of names loaded from the given path

Return value:
- A new `PlayerList` instance on success, throws an exception on failure

## Examples

```CSharp
PlayerList list = PlayerList.Load("text/mylist.txt");
list.Add("Player1");
list.Remove("Player2");
list.Save();
```
