---
tags:
  - SQL
  - MSQL
---
Permesiso de ejecución a cualquier tabla de SQL con el schema 'x':
```SQL
DECLARE @SchemaName varchar(20)
DECLARE @UserName varchar(20)

SET @SchemaName = 'dbo'
SET @UserName = 'elena'

select 'GRANT EXECUTE ON OBJECT::' + @SchemaName + '.' + P.name  + ' to ' + @UserName
from sys.procedures P
inner join sys.schemas S on P.schema_id = S.schema_id
where S.name = @SchemaName
```

Esto genera los comandos GRANT SELECT para cada tabla base del esquema dbo. Luego, copia y ejecuta esas sentencias para asignar permisos.
```SQL
DECLARE @SchemaName varchar(20)
DECLARE @UserName varchar(20)

SET @SchemaName = 'dbo'
SET @UserName = 'elena'

SELECT 'GRANT SELECT ON OBJECT::' + @SchemaName + '.' + TABLE_NAME + ' TO ' + @UserName
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_SCHEMA = @SchemaName
AND TABLE_TYPE = 'BASE TABLE'

```

Dar Permisos de lectura a todas las BBDD de MSQL:

```SQL
USE master  
GO

  
DECLARE @DatabaseName NVARCHAR(100)     
DECLARE @SQL NVARCHAR(max)  
DECLARE @User VARCHAR(64)  
-- ##### AQUÍ S'HA DE CANVIAR EL NOM D'USUARI PEL LOGIN QUE S'HAGI CREAT PER DRIVING01 #####  
-- ##### AQUEST LOGIN HA D'HAVER ESTAT CREAT PRÈVIAMENT #####  
SET @User = '[User]'

PRINT 'The following user has been selected to have read-only access on all user databases except system databases and log shipped databases:  ' +@user

  
DECLARE Grant_Permission CURSOR LOCAL FOR  
SELECT name FROM sys.databases  
WHERE name NOT IN ('master','model','msdb','tempdb','distribution')    
and [state_desc]='ONLINE' and  [is_read_only] <> 1 order by name  
OPEN Grant_Permission    
FETCH NEXT FROM Grant_Permission INTO @DatabaseName    
WHILE @@FETCH_STATUS = 0  

BEGIN  

SELECT @SQL = 'USE '+ '[' + @DatabaseName + ']' +'; '+ 'CREATE USER ' + @User +   
    'FOR LOGIN ' + @User + '; EXEC sp_addrolemember N''db_datareader'',   
    ' + @User + '';  
PRINT @SQL  
EXEC sp_executesql @SQL

Print ''-- This is to give a line space between two databases execute prints.

FETCH NEXT FROM Grant_Permission INTO @DatabaseName    
  
END  

CLOSE Grant_Permission    
DEALLOCATE Grant_Permission
```