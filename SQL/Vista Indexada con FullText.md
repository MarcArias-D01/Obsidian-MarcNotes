---
tags:
  - SQL
  - MSQL
---
Crear un vista con Indice y fulltext index

```sql
CREATE VIEW mf.VI_MotorbikesSearch WITH SCHEMABINDING AS
SELECT T1.Id As IdMotorbike, T1.IdMotorbikeSeries, T1.IdMotorbikeModel, T1.IdMotorbikeVersion, T1.IdMotorbikeSubversion, T6.Id As IdMotorbikeBrand,  CONCAT(T6.Name, ' ', T1.FullTextData/*, ' ', T1.Year, ' ', T1.Size*/) SearchPatterns  FROM mf.Motorbikes T1
INNER JOIN mf.MotorbikesSeries T2 ON T2.Id = T1.IdMotorbikeSeries
INNER JOIN mf.MotorbikesModels T3 ON T3.Id = T1.IdMotorbikeModel
INNER JOIN mf.MotorbikesVersions T4  ON T4.Id = T1.IdMotorbikeVersion
INNER JOIN mf.MotorbikesSubVersions T5 ON T5.Id = T1.IdMotorbikeSubversion
INNER JOIN mf.MotorbikesBrands T6 ON T6.Id = T3.IdMotorbikeBrand

GO

-- Primero el índice único obligatorio
CREATE UNIQUE CLUSTERED INDEX IX_mfVI_MotorbikesSearch_IdMotorbike ON mf.VI_MotorbikesSearch(IdMotorbike);
 
-- Ahora el Full-Text Index
CREATE FULLTEXT INDEX ON mf.VI_MotorbikesSearch(SearchPatterns) 
KEY INDEX IX_mfVI_MotorbikesSearch_IdMotorbike ON ReddFT WITH STOPLIST = OFF; 

```