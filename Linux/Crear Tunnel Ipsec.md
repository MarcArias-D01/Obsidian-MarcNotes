---
tags:
  - linux
---
## Instalar strongswan
```bash
sudo apt update
sudo apt install strongswan strongswan-pki libcharon-extra-plugins -y
```

- `strongswan`: El motor principal de la VPN.
- `strongswan-pki`: Herramientas para gestionar claves (por si en el futuro usas certificados).
- `libcharon-extra-plugins`: Plugins necesarios para que se entienda perfectamente con los algoritmos de encriptación que usa Azure.

