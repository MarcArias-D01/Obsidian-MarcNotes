---
tags:
  - SQL/MSQL
---
Obtener todas las queries de como se crean las vistas de la BBDD:

```sql
SELECT 
    OBJECT_SCHEMA_NAME(v.object_id) AS schema_name,
    v.name AS view_name,
    TRIM(m.definition) AS view_definition
FROM sys.views AS v
JOIN sys.sql_modules AS m
    ON v.object_id = m.object_id
ORDER BY schema_name, view_name;
```