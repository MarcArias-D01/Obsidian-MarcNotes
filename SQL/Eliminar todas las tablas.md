---
tags:
  - SQL
  - MSQL
---
OJO!!!
Elimina todas las tablas de la BBDD.

```SQL
DECLARE @TableName NVARCHAR(128)
DECLARE table_cursor CURSOR FOR
SELECT table_name
FROM information_schema.tables
WHERE table_type = 'BASE TABLE'

OPEN table_cursor
FETCH NEXT FROM table_cursor INTO @TableName

WHILE @@FETCH_STATUS = 0
BEGIN
    DECLARE @Sql NVARCHAR(500)
    SET @Sql = 'DROP TABLE ' + @TableName
    EXEC sp_executesql @Sql
    FETCH NEXT FROM table_cursor INTO @TableName
END

CLOSE table_cursor
DEALLOCATE table_cursor
```