---
tags:
  - SQL
  - MSQL
---
Procedimiento creado para eliminar los logs del systema de todas las BBDD.

```SQL
USE [master]
GO
/****** Object:  StoredProcedure [dbo].[usp_CleanLogs]    Script Date: 22/10/2025 16:29:03 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author:		Marc Arias
-- Create date: 02-10-2024
-- Description:	Stored Procedure dedicado a la limpieza de logs de las bases de datos.
-- =============================================
ALTER PROCEDURE [dbo].[usp_CleanLogs] 
AS
BEGIN
	-- SET NOCOUNT ON added to prevent extra result sets from
	-- interfering with SELECT statements.
	SET NOCOUNT ON;
 
		DECLARE @DatabaseName NVARCHAR(128)
		DECLARE @sqlCommand NVARCHAR(MAX)
		DECLARE db_cursor CURSOR FOR
		SELECT name
		FROM sys.databases
		WHERE name NOT IN ('master', 'model', 'msdb', 'tempdb')  -- System DB cuidado con etas BBDD la tempdb puede modificarse un poco pero mejor que no
		AND state_desc = 'ONLINE'  
		OPEN db_cursor
		FETCH NEXT FROM db_cursor INTO @DatabaseName
		WHILE @@FETCH_STATUS = 0
		BEGIN
		    -- Construccion de la query
		    SET @sqlCommand = 'USE [' + @DatabaseName + ']; ' + CHAR(13) + CHAR(10) +
		                      'ALTER DATABASE [' + @DatabaseName + '] SET RECOVERY SIMPLE; ' + CHAR(13) + CHAR(10) +
		                      'DBCC SHRINKFILE (' + QUOTENAME(@DatabaseName + '_log') + ', 1);'
		    -- Ejecución
		    EXEC sp_executesql @sqlCommand
		    -- pasar al siguiente valor del cursor
		    FETCH NEXT FROM db_cursor INTO @DatabaseName
		END
		CLOSE db_cursor
		DEALLOCATE db_cursor
 
END
```