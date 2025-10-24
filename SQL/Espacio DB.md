#SQL/command/query

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