
#linux/command 

`journalctl` es una herramienta de Linux para **ver y gestionar los logs del sistema y servicios** que usan `systemd`.  
Permite **filtrar por unidad, fecha, nivel de severidad o procesos específicos**, facilitando el diagnóstico de problemas.  
Se puede usar en tiempo real (`-f`) o para **extraer información histórica**, funcionando como un “visor centralizado de logs”.

#clean

```bash
sudo journalctl --vacuum-time=7d
```

Comando perfecto para solo almacenar logs de los systemd de los último 'x' días