---
tags:
  - SQL/MSQL
---
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
SELECT DISTINCT T1.*, T2.physical_name, T2.file_logical_name
FROM Databases_size T1
LEFT JOIN (SELECT db.name AS database_name,
	mf.name AS file_logical_name,
	mf.physical_name,
	mf.type_desc AS file_type
FROM sys.master_files mf
JOIN sys.databases db ON db.database_id = mf.database_id) T2 ON T1.DatabaseName = T2.database_name
ORDER BY SizeMB DESC
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