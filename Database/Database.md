### Summary

The `Database` class abstracts executing SQL commands/queries in the underlying Database System (RMDBS) via both a low level and high level interface

todo: move via LL/HL to second line?

TODO: stuff should return true/false failure or throw exceptions?

todo: link to IDatabaseBackend and ColumnDesc
Remarks
- Generally the high level interface should be used if possible (that way you do not need to worry about SQL differences betweeen Database System implementations)
- Parameterised queries using SQL parameters should always be used whenever possible

#### Parameterised queries / Prepared statements

The `Database` class is designed to easily support parameterised SQL queries and commands

Therefore the majority of methods take an additional `args` argument that specifiy the values of one or more SQL parameters

NOTE: For simplicity, only the `@[arg index]` format is supported for SQL parameter names

Examples:
```CSharp
Database.AddRow("Example", "name,count", "John", 400);

Database.GetRows("Example", "name,count", "WHERE count >= @0 && count < @1", 50, 9000);
```

## High level API

### Table Management Methods

#### `static bool TableExists(string table)`

Whether a table with the given name exists

Remarks:
- The table name is **case sensitive**

#### `static void CreateTable(string table, ColumnDesc[] columns)`

Creates a new table in the database

Remarks:
- Does nothing if a table with the same name already exists

#### `static void RenameTable(string srcTable, string dstTable)`
		
Renames the source table to the given name
		
Remarks
- Source table must exist and destination table must not exist

#### `static void static void DeleteTable(string table)`
		
Completely removes the given table

Remarks:
	Does nothing if the given table does not actually exist
        
#### `static void AddColumn(string table, ColumnDesc col, string colAfter)`
		
Adds a new coloumn to the given table
		
Remarks:
- Note `colAfter` is only a hint - some database systems ignore it

### Data retrieval (Query) methods

#### `static int CountRows(string table, [optional] string modifier, params object[] args)`

Counts rows in the given table.

Remarks:
- `modifier` is an optional argument that does not have to be provided
- If `modifier` is provided, then it is treated as SQL to filter which rows are counted

#### `static string ReadString(string table, string column, [optional] string modifier, params object[] args)`
       
Returns value of first column in last row read from the given table

Remarks:
- `modifier` is an optional argument that does not have to be provided
- If `modifier` is provided, then it is treated as SQL to filter which rows are read
									 
#### `static List<string[]> GetRows(string table, string column, [optional] string modifier, params object[] args)`
       
Returns all columns of all rows read from the given table

Remarks:
- `modifier` is an optional argument that does not have to be provided
- If `modifier` is provided, then it is treated as SQL to filter which rows are read, return rows in a certain order, etc
							
#### `static List<string[]> ReadRows(string table, string column, ReaderCallback callback, [optional] string modifier, params object[] args)`
       
Iterates over read rows for the given table

Remarks:
- `modifier` is an optional argument that does not have to be provided
- If `modifier` is provided, then it is treated as SQL to filter which rows are read, return rows in a certain order, etc

#### Data modifying (Command) methods

TODO FINISH

/// <summary> Inserts/Copies all the rows from the source table into the destination table. </summary>
        /// <remarks> May NOT work correctly if the tables have different schema. </remarks>
        public static void CopyAllRows(string srcTable, string dstTable);
        
        /// <summary> Updates rows for the given table. </summary>
        /// <param name="modifier"> Optional SQL to filter which rows are updated. </param>
        public static void UpdateRows(string table, string columns,
                                       string modifier = "", params object[] args);
        
        /// <summary> Deletes rows for the given table. </summary>
        /// <param name="modifier"> Optional SQL to filter which rows are deleted. </param>
        public static void DeleteRows(string table, string modifier = "", params object[] args);

        /// <summary> Adds a row to the given table. </summary>
        public static void AddRow(string table, string columns, params object[] args);
        
        /// <summary> Adds or replaces a row (same primary key) in the given table. </summary>
        public static void AddOrReplaceRow(string table, string columns, params object[] args);

## Examples

TODO