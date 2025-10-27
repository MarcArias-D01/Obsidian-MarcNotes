#SQL/command/query 
#SQL/MSQL 

Encontrar un valor en una tabla de SQL. Saber en que columna se haya el valor.

```SQL
DECLARE @TableName NVARCHAR(255) = 'Articles';
DECLARE @SearchValue NVARCHAR(50) = '0009';
DECLARE @ColumnName NVARCHAR(255);
DECLARE @SqlCmd NVARCHAR(1000);

DECLARE column_cursor CURSOR
FOR
SELECT COLUMN_NAME
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = @TableName;

OPEN column_cursor;

FETCH NEXT
FROM column_cursor
INTO @ColumnName;

WHILE @@FETCH_STATUS = 0
BEGIN
	BEGIN TRY
		SET @SqlCmd = '
            IF EXISTS (SELECT 1 FROM ' + QUOTENAME(@TableName) + ' WHERE ' + QUOTENAME(@ColumnName) + ' = ''' + @SearchValue + ''')
            BEGIN
                PRINT ''Value found in column: ' + @ColumnName + ''';
            END
        ';

		EXEC sp_executesql @SqlCmd;
	END TRY

	BEGIN CATCH
		PRINT 'Error in column: ' + @ColumnName + ' - ' + ERROR_MESSAGE();
			-- Continúa con la siguiente columna
	END CATCH;

	FETCH NEXT
	FROM column_cursor
	INTO @ColumnName;
END

CLOSE column_cursor;

DEALLOCATE column_cursor;

```