---
tags:
  - SQL/MSQL
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