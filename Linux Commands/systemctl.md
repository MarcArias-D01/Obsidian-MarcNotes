#linux/command 

#linux/location
Ubicación normal si se ejecuta como un usuario:
```bash
ls ~/.config/systemd/user/
```

Listar los servicio a los que tiene acceso el usuario
```bash
systemctl --user list-units
```

#linux/command/create  

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

#linux/command/start 

Para ejecutar el procedure. Ejecutar uno a uno
```bash
systemctl --user daemon-reload

systemctl --user restart exec-script.service

systemctl --user enable exec-script.service

systemctl --user start exec-script.service

systemctl --user status exec-script.service
```

