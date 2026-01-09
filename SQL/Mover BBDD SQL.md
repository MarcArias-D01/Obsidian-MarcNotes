---
tags:
  - SQL/MSQL
---
Mover la ubicación de una BBDD. Primero tienes que ejecutar la parte hasta el ROLBACKIMMEDIATE.
Mover la ubicación del archivo de path_old a path_new. Seguidamente ejecutar las siguientes lineas.

```SQL
USE CadastreEspanya;
GO

ALTER DATABASE CadastreEspanya MODIFY FILE (
	NAME = CadastreEspanya,
	FILENAME = '/mnt/HC_Volume_38100564/mssql_data/CadastreEspanya.mdf'
	)
GO

ALTER DATABASE CadastreEspanya MODIFY FILE (
	NAME = CadastreEspanya_log,
	FILENAME = '/mnt/HC_Volume_38100564/mssql_data/CadastreEspanya_log.ldf'
	)
GO

ALTER DATABASE CadastreEspanya

SET OFFLINE
GO

ALTER DATABASE CadastreEspanya

SET OFFLINE
WITH

ROLLBACK IMMEDIATE;

----
ALTER DATABASE CadastreEspanya

SET ONLINE;
GO

SELECT name,
	physical_name AS CurrentLocation,
	state_desc
FROM sys.master_files
WHERE database_id = DB_ID(N'CadastreEspanya');
```