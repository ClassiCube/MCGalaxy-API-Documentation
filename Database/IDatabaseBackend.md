### Summary

The `IDatabaseBackend` class abstracts a particular Database System (RDBMS) implementation

There are three main functions of this class:
- Provide information about implementation specific limitations and SQL syntax
- Provide information about tables and table columns
- Generate strings representing SQL commands and queries

Remarks:
- Generally methods in the [Database](/Database/Database.md) class should be used instead

Examples
- SQLite, MySQL, etc

## Implementation API

### Database interaction

#### `ISqlConnection CreateConnection()`

Creates a new connection to the database for executing SQL commands and queries

Remarks:
- Generally it is preferrable to use the `Execute` and `Iterate` methods, rather than manually managing a connection to the database

#### `void Execute(string sql, object[] parameters, bool createDB)`

Executes an SQL command that does not return any results

Remarks:
- Generally the `Execute` method in the [Database](/Database/Database.md) class should be used instead
- `parameters` argument provides the values for SQL parameters
- The `createDB` argument should be `false` 99% of the time

#### `void Iterate(string sql, object[] parameters, ReaderCallback callback)`

Excecutes an SQL query, invoking a callback on the returned rows one by one

Remarks:
- Generally the `Iterate` method in the [Database](/Database/Database.md) class should be used instead
- `parameters` argument provides the values for SQL parameters

### Implementation specific information

#### `bool EnforcesTextLength { get; }`

Whether this database system implementation enforces the character length in VARCHAR columns

Examples:
- SQLite implementation does **not** enforce them
- MySQL implementation does enforce them

#### `bool EnforcesIntegerLimits { get; }`
		
Whether this database system implementation enforces integer limits based on column types

Examples:
- SQLite implementation does **not** enforce them
- MySQL implementation does enforce them

#### `string CaselessWhereSuffix { get; }`

Suffix required after a WHERE clause for caseless string comparison

Examples:
- SQLite requires a `COLLATE NOCASE` suffix

#### `string CaselessLikeSuffix { get; }`

Suffix required after a LIKE clause for caseless string comparison

Examples:
- SQLite requires a `COLLATE NOCASE` suffix

### Table Management Methods

#### `bool TableExists(string table)`

Whether a table with the given name exists

Remarks:
- The table name is **case sensitive**

#### `List<string> AllTables()`

Returns the names of all of the tables in the database

#### `List<string> ColumnNames(string table)`
		
Returns the names of all of the columns in the given table
	
#### `void PrintSchema(string table, TextWriter w)`
		
Prints/dumps the table schema of the given table

## SQL generation API

### Table management commands

#### `string RenameTableSql(string srcTable, string dstTable)`
		
Returns the SQL for renaming the source table to the given name

#### `string CreateTableSql(string table, ColumnDesc[] columns)`

Returns the SQL for creating a new table in the database

#### `string DeleteTableSql(string table)`
		
Returns the SQL for completely removing the given table
        
#### `string AddColumnSql(string table, ColumnDesc col, string colAfter)`
		
Returns the SQL for adding a new coloumn to the given table

### Data commands and queries

#### `string ReadRowsSql(string table, string column, string modifier)`
       
Returns SQL for reading rows from the given table

Remarks:
- `modifier` is SQL to filter which rows are read, return rows in a certain order, etc (can be `""` though)

#### `string CopyAllRowsSql(string srcTable, string dstTable)`

Returns SQL for copying all of the rows from the source table into the destination table

#### `string UpdateRowsSql(string table, string columns, string modifier)`

Returns SQL for updating rows in the given table

Remarks:
- `modifier` is SQL to filter which rows are updated (can be `""` though)

#### `string DeleteRowsSql(string table, string columns, string modifier)`

Returns SQL for deleting row in the given table

Remarks:
- `modifier` is SQL to filter which rows are deleted (can be `""` though)

#### `string AddRowSql(string table, string columns)`

Returns SQL for adding a row to the given table
        
#### `string AddOrReplaceRow(string table, string columns)`

Returns SQL for adding or replacing a row with the same primary key in the given table

## Examples

TODO