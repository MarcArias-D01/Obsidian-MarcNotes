---
tags:
  - linux
  - linux/arch
  - linux/pacman
  - linux/clean
  - linux/update
  - linux/install
---
El gestor de paquetes oficial en Arch Linux.

## Instal

Para instalar una librería nueva:
```bash
sudo pacman -S <nombre-libreria>
```

## Update

Para hacer un Update del sistema. *Ojo si tienes yay instalado. Deberes recompilarlo*

```bash
sudo pacman -Syu
```

## Search

Para buscar si existe alguna librería disponible
```bash
pacman -Ss <text-busqueda>
```

## Clean

Para eliminar el cache de librerías antiguas instaladas:
```bash
sudo pacman -Sc # Limpiar todo excepto la version instalada
```

Para eliminar paquetes huérfanos (dependencias que actualmente no sirven de nada)
```bash
sudo pacman -Rs $(pacman -Qdtq) # Si devuelve que no se encontraron objetivos es que ya esta limpio
```
