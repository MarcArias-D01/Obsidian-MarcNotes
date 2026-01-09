---
tags:
  - SQL/MSQL
---
Devuelve una lista de todas las Foreing keys que hay en la BBDD con el nombre, tabla destino y tabla origen.

```SQL
SELECT T1.name AS ForeingKey,
	T2.name AS TableName,
	T3.name AS MainTable
FROM sys.foreign_keys T1
LEFT JOIN sys.objects T2 ON T1.referenced_object_id = T2.object_id
LEFT JOIN sys.objects T3 ON T1.parent_object_id = T3.object_id
```