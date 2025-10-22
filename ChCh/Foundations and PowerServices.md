#powerautomate
#ssis
#python 
#client/chupachups/sellout
___

Git repo new ETL : 
- [Driving01/ChCh---SellOutTT](https://github.com/Driving01/ChCh---SellOutTT)

### TT 
Se basa de momento en dos procesos. La carga de albaranesTT y TMPStocks. Los distribuidores nos haces llegar ficheros `.txt` vía ftp al servidor sagitario de ChupaChups.

- Hay un proceso muy grande que hizo David en su tiempo todo en SQL para albaranesTT. LA idea es migrar-lo a algo que funcione mejor que PowerAutomate y SSIS
- en StocksTMP también hay un proceso muy grande que hizo David en SQL. También se mirara de migrar a algo más manejable y modular.

Actualmente hay errores cuando se ejecutan algunos comandos. Las tablas están mal formuladas creando problemas de rendimiento graves en SQL. También hace falta un proceso de comprobación de datos. Actualmente se pueden estar introduciendo datos duplicados o mal formateados. Se corrige todo a mano y a veces rehaciendo el proceso de ETL de algún archivo.

### OT

___
## Primera Semana de Mes
### Belros
Nos pasan unos excels cada mes. Hay que cargarlos mediante el proceso de SSIS. Problema: crea errores el proceso de SSIS y la carga. mi python va bien.
- [x] 🔺 Ejecutado Python 10-2025 ✅ 2025-10-17
### Conway
Archivos llegan por correo. // Envios Conway
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-17
### Logista
Llegan por mail. // Lucia o Cristina
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-17
______

## Tercera Semana de Mes
### Alcampo 
Llegan por mail Rosa o Miquel
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-17

### Eroski
Entrar al FTP de Eroski y descargar los archivos
Seleccionamos Eroski IRI y se cargan dos carpetas: Up y Down. La información se encuentra en la carpeta Down. Se descargan los ficheros y estos se guardan en Temp/Nielsen. Se copian y se pegan en SelloutOT/Eroski/Ficheros (2).
Se borra el fichero FINAL.txt (3) y se renombra el fichero Extract Chupa Chups E3C_Star Schema_Mensual_aaaa-mm-12-00-dd-mm_FINAL.txt como FINAL.txt (4). El fichero Productos.txt se borra (5) y Extract Chupa Chups E3C_Star Schema_Mensual_aaaa-mm-12-00-dd-mm_Product_Meta.txt se renombra como Productos.txt (6). Se borra el fichero Clientes.txt (7) y Extract Chupa Chups E3C_Star Schema_Mensual_aaaa-mm-12-00-dd-mm_Geographi_Meta.txt se renombra como Clientes.txt (8). Borramos el fichero Extract Chupa Chups E3C_Star Schema_Mensual_aaaa-mm-12-00-dd-mm_Time_Meta.txt (9)

- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-17

### ECI
Se reciben en el FTP de Sagitario EDI_ECI/Files. Hay un proce que se ejcuta todos los dias alas 3 - 4 am descubrir que es el PwoerAutoamte no va
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-20

### Dia
Follón gordo...
- [x] 🔺 Ejecutado 10-2025 Mirar de ejecutar next week ✅ 2025-10-20

### Carrefour
Entrar en su portal y descargar
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-17
___
## Cada Semana
### Carreforu weekly
Ejecutar cada semana
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-09
- [x] 🔺 Ejecutado 10-2025 ✅ 2025-10-16
___

# ToDo

Errores encontrados: #client/chupachups/error

- [x] ⛔ 17-09-2025 el proveedor C3410000792 en el precio tiene errores de formato --> 1.056.00 ✅ 2025-09-19
- [ ] ⛔16-09-2025 en la tabla albaranesTT hay duplicados, tanto con clavePK o porque la clavePK es NULL o ''. Por suerte son valores del año 2023 o inferior.
- [x] ⛔ 17-09-2025 EN SO_Belros el proceso de SSIS utilizado hasta la fecha originaba errores de varios ámbitos como duplicados, fechas mal formateadas ,etc etc... ✅ 2025-09-19
- [x] ⛔ 18-09-2025 En SO_ECI puede haber algunos errores debido al cruce que se hace con `PRD_Product`. Cuando esta Categoría tiene el valor de **Chupa Chups PVM Mixed Categories**, **Mentos PVM Mixed Categories** o **Smint PVM Mixed Categories** la categoría aparece como `Categories` Esta mal debería ser siempre GUM o CANDY. 23-09-2025 Rosa quiere una lista para que nos diga cuales sustituir por Candy o Gum. ✅ 2025-10-17
- [x] ⛔ 19-09-2025 En SO_ECI_POS no se actualiza automáticamente. Por ende faltan puntos de venta de el corte ingles tendríamos que ver como se esta haciendo la ETL para poder hacer algún proceso para añadirlos automáticamente. Actualmente no pasa esto y aparecen registros en SO_ECI sin un match con SO_ECI_POS. ✅ 2025-10-14
- [x] ⛔ 22-09-2025 En Alcampo algo ha pasado con la ETL no se ha actualizado correctamente. ✅ 2025-10-06
- [x] ⏬ 25-09-2025 Lucia quiere machacar valores de SKU por unos que hay en un excel que ha pasado a la tabla de Logista_PRD ✅ 2025-09-25
- [x] ⛔ 22-09-2025 En Alcampo algo ha pasado con la ETL no se ha actualizado correctamente. ✅ 2025-10-02
- [x] ⏬ 25-09-2025 Lucia quiere machacar valores de SKU por unos que hay en un excel que ha pasado a la tabla de Logista_PRD ✅ 2025-10-02
- [x] ⛔ 01-10-2025 En Conway el Adri destruyo una columna y el proceso fallaba. ✅ 2025-10-02
- [x] 🔁 Mirar de reducir los datos en cada columna mediante FK (conversar con Adri). ✅ 2025-10-06
- [x] 🔼 03-10-2025 Añadir la tabla de Logs que se usa actualmente en la ETL platform. ✅ 2025-10-06
- [x] 2025-10-06 ⏫ Testear en Server Sagitario. ✅ 2025-10-14
- [x] 🔺 2025-10-06 Ejecución SSI Octubre ✅ 2025-10-06
- [x] 2025-10-06 Faltan datos de clintes SSIS. ✅ 2025-10-21
- [x] 🔺2025-10-06 Altimiras los datos que sube al FTP siempre son de junio... ✅ 2025-10-17
- [x] 🔼 2025-10-07 Lucia necesita ayuda, quiere una tabla con datos agregados de conway. logista y belros. ✅ 2025-10-21
- [x] 🔺 Control Nuevos CodTipologias en cada carga. Informar. ✅ 2025-10-14
- [x] 🔺 Mirar Txt vacios ✅ 2025-10-21
- [x] 🔼  Rosa quire añadir en la vista Eroski ✅ 2025-10-21
- [x] 🔺 ChCh cargar todos los csv son diarios. ✅ 2025-10-21
- [ ] 🔼 Mirar que paso en Agosto de 2024 ECI
- [ ] Proceso Carrefour importar datos antiguos
- [ ] Proceso Eorski importar datos antiguos
- [ ] Proceso Alcampo importat datos antiguos
