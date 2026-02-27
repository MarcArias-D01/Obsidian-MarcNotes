---
tags:
  - ubuntu
  - dns
  - dnsmask
---
Si el servidor ubuntu se actualiza automáticamente este puede degenerar y recrear el dnsmas.conf. Si lo hace cambia el nombre del archivo a dnsmask.conf.dpkg-old y crea uno nuevo vacía.

```conf
server=/privatelink.database.windows.net/168.63.129.16  
interface=eth0  
except-interface=lo  
listen-address=10.0.0.4  
bind-interfaces
```

