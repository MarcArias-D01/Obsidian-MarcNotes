---
tags:
  - SQL
  - MSQL
---
Devuelve una lista de todas las relaciones que tiene con otra tabla una tabla de SQL

```SQL
SELECT 
    fk.name AS FK_Name,
    tp.name AS Parent_Table,
    cp.name AS Parent_Column,
    tr.name AS Referenced_Table,
    cr.name AS Referenced_Column,
	Query = 'ALTER TABLE ' + tp.name + ' ADD CONSTRAINT fk_' + cp.name + ' FOREIGN KEY (' + cp.name + ') REFERENCES Master' + tr.name + '(' + cr.name + ');'  
FROM 
    sys.foreign_keys AS fk
INNER JOIN 
    sys.foreign_key_columns AS fkc ON fk.object_id = fkc.constraint_object_id
INNER JOIN 
    sys.tables AS tp ON fk.parent_object_id = tp.object_id
INNER JOIN 
    sys.columns AS cp ON fkc.parent_object_id = cp.object_id AND fkc.parent_column_id = cp.column_id
INNER JOIN 
    sys.tables AS tr ON fk.referenced_object_id = tr.object_id
INNER JOIN 
    sys.columns AS cr ON fkc.referenced_object_id = cr.object_id AND fkc.referenced_column_id = cr.column_id

WHERE tp.name = 'BARTICLES'
ORDER BY
    Parent_Table, tr.name,FK_Name;
```