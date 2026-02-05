---
tags:
  - linux
  - ubuntu
  - lsof
  - port
---
Abreviatura de *list open files* sirve para **listar todos los archivos que están abiertos actualmente por los procesos del sistema**. En Linux, _todo es un archivo_ (archivos, sockets, tuberías, dispositivos y conexiones de red), por lo que `lsof` es una herramienta muy potente para monitorear qué procesos están usando recursos del sistema.

___
## Ejemplos útiles

- 1  **Ver qué usa un puerto específico (como el 8089):**
```bash
sudo lsof -i:8089
```

- 2  **Listar archivos abiertos por un usuario:**
```bash
lsof -u nombre_usuario
```

  - 3  **Mostrar archivos abiertos de un proceso conocido:**
```bash
lsof -p 1234
```

 - 4 **Filtrar por tipo de red o protocolo:**
```bash
lsof -p 1234
```

- 5 **Ver qué archivos están abiertos en un directorio:**
```bash
sudo lsof +D /var/log/
```

- 6  **Solo el PID del proceso que usa un puerto (útil para matar procesos):**
```bash
sudo lsof -t -i:8089
```
 
