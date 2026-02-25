---
tags:
  - linux
  - systemctl
  - gui
  - xrdp
---


```bash
# Escritori remoto funciona con xrdp
sudo systemctl restart xrdp

# Matar sesion de GUI que tenga levantada para que devuelva la imagen por xrdp
sudo pkill -u admredd -9 xfce4-session
sudo pkill -u admredd -9 Xvnc
```