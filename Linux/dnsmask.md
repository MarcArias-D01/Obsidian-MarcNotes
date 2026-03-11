---
tags:
  - ubuntu
  - dns
  - dnsmask
  - network
---
Si el servidor ubuntu se actualiza automáticamente este puede degenerar y recrear el dnsmas.conf. Si lo hace cambia el nombre del archivo a dnsmask.conf.dpkg-old y crea uno nuevo vacía.

```conf
server=/privatelink.database.windows.net/168.63.129.16  
interface=eth0  
except-interface=lo  
listen-address=10.0.0.4  
bind-interfaces
```

PROBLEMA solucionado en D01:
Empezó a petar todo lo relacionado con DNS. Conseguimos depurar el problema hasta llegar al servidor que tiene la VPN funcionando i vimos que había un dnsmas.conf.dpkg-old este al hacer investigaciones en internet vimos que tenia configuración muy parecida a las que se proponían y la restauramos a como estaba antes y reseteamos el procedure  de dnsmask.