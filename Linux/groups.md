---
tags:
  - linux
  - groups
  - user
  - security
---
Cuando quieres ejecutar algún comando sin que te pida usarlo --> `sudo comando`

Añadir el usuario con el que estas por ejemplo al grupo docker
```bash
sudo usermod -aG docker $USER
```

```bash
groups
# Verás "docker" al final, pero aún necesitarás recargar la sesión
```

Para aplicar cambios sin resetear la sesión:
```bash
newgrp docker
```

Ahora verificar usando cualquier comando de docker sin añadir `sudo docker`


