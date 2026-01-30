---
tags:
  - SQL
  - MSQL
---
Query para saber lo que ocupa cada tabla en una BBDD

```SQL
SELECT  
    s.name + '.' + t.name AS TableName,  
    SUM(p.rows) AS TotalRows,  
    SUM(a.total_pages) * 8 / 1024 AS TotalMB,  
    SUM(a.used_pages) * 8 / 1024 AS UsedMB,  
    SUM(a.data_pages) * 8 / 1024 AS DataMB,  
    CONVERT(DECIMAL(18,2), (SUM(a.used_pages) * 8.0 / 1024.0 / 1024.0)) AS UsedGB  
FROM sys.tables t  
INNER JOIN sys.schemas s ON t.schema_id = s.schema_id  
INNER JOIN sys.indexes i ON t.object_id = i.object_id  
INNER JOIN sys.partitions p ON i.object_id = p.object_id AND i.index_id = p.index_id  
INNER JOIN sys.allocation_units a ON p.partition_id = a.container_id  
GROUP BY s.name, t.name  
ORDER BY UsedGB DESC;
```