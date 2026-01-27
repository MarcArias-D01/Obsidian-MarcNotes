---
tags:
  - linux
  - clean
  - logs
  - ubuntu
  - arch
---
`journalctl` es una herramienta de Linux para **ver y gestionar los logs del sistema y servicios** que usan `systemd`.  
Permite **filtrar por unidad, fecha, nivel de severidad o procesos específicos**, facilitando el diagnóstico de problemas.  
Se puede usar en tiempo real (`-f`) o para **extraer información histórica**, funcionando como un “visor centralizado de logs”.

```bash
journalctl --disk-usage # Saber espacio ocupado en logs
```

```bash
sudo journalctl --vacuum-time=7d # Guardar últimos 7 días de logs
```


```bash
sudo journalctl --vacuum-size=100M # Limita Logs a !00Mb
```
