---
tags:
  - SQL/MSQL
---
Si eliminas una BBDD en el que un usuario estaba agenciado ese usuario no va a poder loggearse nunca. Deberás agenciarle otra BBDD a ese usuario. Ejemplo de lo que paso en MEtarom.

```SQL

SELECT name, default_database_name  
FROM sys.server_principals  
WHERE name = 'driving01';

ALTER LOGIN driving01 WITH DEFAULT_DATABASE = [master]
```