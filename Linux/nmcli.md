---
tags:
  - linux
  - arch
  - network
  - nmcli
---
Programa para trabajar con redes des de tu ordenador o servidor
## radio wifi

Para verificar que el wifi de tu servidor/ordenador esta activo:

```bash
nmcli radio wifi
```
### *Imagen de ejemplo*
![[linux-nmcli-radio-wifi.png]]

En caso de devolver `disabled` al ejecutar el comando de `nmcli radio wifi`  ejecutar lo siguiente para activar el wifi:

```bash
nmcli radio wifi on
```

## wifi list

Para poder ver las redes wifi disponibles a las que connectarse:

```bash
nmcli device wifi list

nmcli -f ALL dev wifi list
```
### *Imagen de ejemplo*
![[nmcli-device-wifi-list.png]]
![[nmcli-dev-wifi-list.png]]
## wifi connect

Para poder conectarnos a alguna de las redes mostradas usando el comando `device wifi list`

```bash
nmcli device wifi connect "nombre-red" password "password-red"

# Si no tubiera password
nmcli device wifi connect "nombre-red"
```
### *Imagen de ejemplo*
![[nmcli-device-wifi-connect-password.png]]
![[nmcli-device-wifi-connect.png]]

## device status

Una vez conectados o si tenemos problemas de red podemos ejecutar lo siguiente para obtener información

```bash
mcli device status
```

### *Imagen de ejemplo*
![[nmcli-device-status.png]]
