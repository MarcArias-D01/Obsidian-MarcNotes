---
tags:
  - SQL/MSQL
---
Escribe como la creación de las columnas de una tabla de SQL. 

```SQL
SELECT column_name,
	data_type,
	character_maximum_length
FROM information_schema.columns
WHERE table_name = 'Articles';
```

```SQL
SELECT column_name,
	data_type,
	character_maximum_length,
	CONCAT (
		COLUMN_NAME,
		' ',
		DATA_TYPE,
		CASE 
			WHEN CHARACTER_MAXIMUM_LENGTH IS NULL
				THEN ''
			ELSE CONCAT (
					'(',
					CHARACTER_MAXIMUM_LENGTH,
					')'
					)
			END
		) AS query
FROM information_schema.columns
WHERE table_name = 'Articles';
```

Viene de la tabla que contiene toda la información de columnas:
```SQL
SELECT * FROM INFORMATION_SCHEMA.COLUMNS
```