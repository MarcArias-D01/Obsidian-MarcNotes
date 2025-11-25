#linux/command/systemctl 

`systemctl` es la herramienta de línea de comandos para interactuar con **systemd**, el sistema de inicio y gestor de servicios en Linux.

Se usa para:
- Iniciar, detener o reiniciar servicios (`systemctl start/stop/restart nombre_servicio`).
- Habilitarlos o deshabilitarlos en el arranque (`systemctl enable/disable`).
- Ver el estado de un servicio (`systemctl status nombre_servicio`).

#linux/location
Ubicación normal si se ejecuta como un usuario:
```bash
ls ~/.config/systemd/user/
```

Listar los servicio a los que tiene acceso el usuario
```bash
systemctl --user list-units
```

Si quieres filtrar por algún nombre especifico o palabra
```bash
systemctl list-units --user --type=service | grep exec
```

#linux/create  

Crear un procedimiento nuevo
```bash
vim ~/.config/systemd/user/exec-script.service
```

```ini
[Unit]
Description=Servicio que ejecuta exec.sh para el usuario
After=default.target

[Service]
Type=simple
ExecStart=/home/althena/exec.sh
WorkingDirectory=/home/althena
Restart=on-failure

[Install]
WantedBy=default.target
```

Otro ejemplo

```ini
[Unit]
Description=FastAPI/Uvicorn Service
After=network.target

[Service]
WorkingDirectory=/home/althena/ALTHENA-GTI-API-Labeler
ExecStart=/home/althena/ALTHENA-GTI-API-Labeler/.venv/bin/python /home/althena/ALTHENA-GTI-API-Labeler/main.py
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```

#linux/init 

Para ejecutar el procedure. Ejecutar uno a uno
```bash
systemctl --user daemon-reload

systemctl --user restart exec-script.service

systemctl --user enable exec-script.service

systemctl --user start exec-script.service

systemctl --user status exec-script.service
```

