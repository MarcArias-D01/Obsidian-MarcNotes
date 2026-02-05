---
tags:
  - SQL
  - MSQL
---
Ver todos los procesos que se estanejecutando en una BBDD.

Puedes hacer `kill <num_proceso>`

```SQL
SELECT session_id,
	login_time,
	host_name,
	program_name,
	STATUS,
	cpu_time,
	memory_usage
FROM sys.dm_exec_sessions
ORDER BY cpu_time
```

Descubrir queries ejecutándose:
```sql
SELECT t.*
FROM sys.dm_exec_requests AS r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
WHERE session_id = <tu_session>
```