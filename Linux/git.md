
Para añadir varios usuarios en el gitconf dependiendo de el repositorio que estes trabajando. Crea un gitconfig para ese usuario con 
```bash
git config user.name "Otro Nombre"
git config user.email "otro@email.com"

```

```bash
[includeIf "gitdir:/ruta/a/repositorio/"]
	path = /root/.gitconfig-usuario
```