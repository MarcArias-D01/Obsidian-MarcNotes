#SQL/command/query
#SQL/MSQL 

Saber el espacio que ocupan las bases de datos

```SQL
WITH Databases_size  
AS (  
    SELECT DB_NAME(database_id) AS DatabaseName,  
        SUM(size * 8 / 1024) AS SizeMB  
    FROM sys.master_files  
    WHERE type = 0  
    GROUP BY DB_NAME(database_id)  
    )  
SELECT *  
FROM Databases_size  
ORDER BY SizeMB;
```

Espacio de logs en DB
```SQL
SELECT
    DB_NAME(database_id) AS DatabaseName,
    name AS LogicalFileName,
    physical_name AS PhysicalFileName,
    size / 128.0 AS CurrentSizeMB,
    size / 128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS float) / 128.0 AS FreeSpaceMB
FROM sys.master_files
WHERE type_desc = 'LOG';
```