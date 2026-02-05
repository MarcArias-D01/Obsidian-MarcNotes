---
tags:
  - linux
  - ubuntu
  - git
---
Para añadir varios usuarios en el gitconf dependiendo de el repositorio que estés trabajando. 

Crea un gitconfig para ese usuario en la ruta `~/.` que sea `~/.gitconfig-user`
```bash
[user]
        name = usuario-de-git
        email = usuario@driving01.com
```

Seguidamente en el `~/.gitconfig` añade lo siguiente al final de todo.  Lo usuarios se cargan de arriba a abajo.

```bash
[includeIf "gitdir:/ruta/a/repositorio/"]
	path = /root/.gitconfig-user
```