Git repo new ETL : 
- [Driving01/ChCh---SellOutTT](https://github.com/Driving01/ChCh---SellOutTT)



### TT
Se basa de momento en dos procesos. La carga de albaranesTT y TMPStocks. Los distribuidores nos haces llegar ficheros `.txt` via ftp al servidor sagitario de ChupaChups.

- Hay un proceso muy grande que hizo David en su tiempo todo en SQL para albaranesTT. LA idea es migrar-lo a algo que funcione mejor que PowerAutomate y SSIS
- en StocksTMP también hay un procso muy grande que hizo David en SQL. También se mirara de migrar a algo más manejable y modular.

Actualmente hay errores cuando se ejecutan algunos comandos. Las tablas estan mal formuladas creando problemas de rendimiento graves en SQL. También hace falta un proceso de comprobación de datos. Actualmente se pueden estar introduciendo datos duplicados o mal formateados. Se corrige todo a mano y a veces rehaciedno el proceso de ETL de algún archivo.

### OT

#### Belros
Nos pasan unos excels cada mes. Hay que cargarlos mediante el proceso de SSIS. Problema: crea errores el proceso de SSIS y la carga. mi python va bien.

Errores encontrados

- [ ] ⛔ 17-09-2025 el proveedor C3410000792 en el precio tiene errores de formato --> 1.056.00
- [ ] ⛔16-09-2025 en la tabla albaranesTT hay duplicados, tanto con clavePK o porque la clavePK es NULL o ''. Por suerte son valores del año 2023 o inferior.
- [ ] ⛔ 17-09-2025 EN SO_Belros el proceos de SSIS utilizado hasta la fecha originaba errores de varios ambitos como duplicados, fechas mal formateadas ,etc etc...