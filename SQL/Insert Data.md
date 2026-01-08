---
tags:
  - SQL/MSQL
  - ETL
---
Este es un Ejemplo de una ETL en SQL. Creamos las tablas temporales transformadas en las que hay que hacer `JOIN` y se hace la carga por batches para no saturar la memoria del servidor.

```sql
SET NOCOUNT ON;

-- 1. Pre-limpiamos las dimensiones en tablas temporales indexadas
IF OBJECT_ID('tempdb..#CleanGeo') IS NOT NULL DROP TABLE #CleanGeo;
SELECT Id, TRIM(LEFT(MemberName, CHARINDEX(' - ', MemberName + ' - ') - 1)) AS CleanName 
INTO #CleanGeo FROM D01_SO_EroskiGeography;
CREATE INDEX IX_CleanGeo ON #CleanGeo(CleanName);

IF OBJECT_ID('tempdb..#CleanProd') IS NOT NULL DROP TABLE #CleanProd;
SELECT Id, TRIM(LEFT(MemberName, CHARINDEX(' - ', MemberName + ' - ') - 1)) AS CleanName 
INTO #CleanProd FROM D01_SO_EroskiProducts;
CREATE INDEX IX_CleanProd ON #CleanProd(CleanName);

DECLARE @BatchSize INT = 50000;
DECLARE @RowsAffected INT = 1;

-- 2. Bucle de inserción
WHILE @RowsAffected > 0
BEGIN
    INSERT INTO D01_SO_Eroski (Uuid, CreatedAt, UpdatedAt, TimeId, GeographyId, ProductId, ValueSales, UnitSales)
    SELECT TOP (@BatchSize)
        NEWID(), 
        GETDATE(), 
        NULL,
        T4.Id, 
        T2.Id, 
        T3.Id, 
        CAST(T1.Value AS DECIMAL(38,8)), 
        CAST(T1.Units AS INT)
    FROM SO_Eroski T1
    INNER JOIN #CleanGeo T2 ON T1.Client = T2.CleanName
    INNER JOIN #CleanProd T3 ON T1.Product = T3.CleanName
    INNER JOIN D01_SO_EroskiTime T4 ON T4.DateFromName = CAST(T1.Date AS DATE)
    LEFT JOIN D01_SO_Eroski T5 ON 
        T5.TimeId = T4.Id AND 
        T5.ProductId = T3.Id AND 
        T5.GeographyId = T2.Id
    WHERE 
        T1.Date >= '2023-01-01'
        AND T5.Id IS NULL; -- Filtro de exclusión

    SET @RowsAffected = @@ROWCOUNT;
    PRINT 'Insertadas ' + CAST(@RowsAffected AS VARCHAR) + ' filas...';
	WAITFOR DELAY '00:00:01'; 
END

-- Limpieza final
DROP TABLE #CleanGeo;
DROP TABLE #CleanProd;
```