---
tags:
  - linux
  - network
  - ip
---

Comando par identificar las ips de tu servidor:

```bash
ip addr show
```

```
ip a
```

Resultado en walugi:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether bc:fc:e7:66:ea:fd brd ff:ff:ff:ff:ff:ff
    inet 136.243.37.107/32 scope global enp4s0
       valid_lft forever preferred_lft forever
    inet6 2a01:4f8:212:561::2/64 scope global 
       valid_lft forever preferred_lft forever
    inet6 fe80::befc:e7ff:fe66:eafd/64 scope link 
       valid_lft forever preferred_lft forever
5: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:19:f1:3e:51 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:19ff:fef1:3e51/64 scope link 
       valid_lft forever preferred_lft forever
147: br-0487d3135550: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:81:29:28:a4 brd ff:ff:ff:ff:ff:ff
    inet 172.19.0.1/16 brd 172.19.255.255 scope global br-0487d3135550
       valid_lft forever preferred_lft forever
    inet6 fe80::42:81ff:fe29:28a4/64 scope link 
       valid_lft forever preferred_lft forever
162: br-761674aeee7e: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:11:e1:df:db brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.1/16 brd 172.18.255.255 scope global br-761674aeee7e
       valid_lft forever preferred_lft forever
    inet6 fe80::42:11ff:fee1:dfdb/64 scope link 
       valid_lft forever preferred_lft forever
166: veth4db41fb@if165: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-761674aeee7e state UP group default 
    link/ether 6a:de:ae:81:29:41 brd ff:ff:ff:ff:ff:ff link-netnsid 1
    inet6 fe80::68de:aeff:fe81:2941/64 scope link 
       valid_lft forever preferred_lft forever
169: br-fb589d71479c: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:c8:00:d7:5b brd ff:ff:ff:ff:ff:ff
    inet 172.20.0.1/16 brd 172.20.255.255 scope global br-fb589d71479c
       valid_lft forever preferred_lft forever
    inet6 fe80::42:c8ff:fe00:d75b/64 scope link 
       valid_lft forever preferred_lft forever
183: veth7b63586@if182: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-fb589d71479c state UP group default 
    link/ether 92:3e:5f:7c:30:d6 brd ff:ff:ff:ff:ff:ff link-netnsid 3
    inet6 fe80::903e:5fff:fe7c:30d6/64 scope link 
       valid_lft forever preferred_lft forever
185: veth51088d3@if184: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-fb589d71479c state UP group default 
    link/ether 56:7b:75:a6:f7:01 brd ff:ff:ff:ff:ff:ff link-netnsid 4
    inet6 fe80::547b:75ff:fea6:f701/64 scope link 
       valid_lft forever preferred_lft forever
227: veth81473e5@if226: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-fb589d71479c state UP group default 
    link/ether 4e:4a:8a:d7:39:d1 brd ff:ff:ff:ff:ff:ff link-netnsid 5
    inet6 fe80::4c4a:8aff:fed7:39d1/64 scope link 
       valid_lft forever preferred_lft forever
229: veth6672fd4@if228: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-0487d3135550 state UP group default 
    link/ether 4a:4f:08:8e:53:b4 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::484f:8ff:fe8e:53b4/64 scope link 
       valid_lft forever preferred_lft forever
231: br-e9b2312db952: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:f7:d8:a3:a2 brd ff:ff:ff:ff:ff:ff
    inet 172.21.0.1/16 brd 172.21.255.255 scope global br-e9b2312db952
       valid_lft forever preferred_lft forever
    inet6 fe80::42:f7ff:fed8:a3a2/64 scope link 
       valid_lft forever preferred_lft forever
235: vethd1abbdd@if234: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-e9b2312db952 state UP group default 
    link/ether ca:ee:f8:4c:17:50 brd ff:ff:ff:ff:ff:ff link-netnsid 2
    inet6 fe80::c8ee:f8ff:fe4c:1750/64 scope link 
       valid_lft forever preferred_lft forever
```

### Interfaces principales

- **lo**
    
    - `127.0.0.1` → es **localhost**, no cuenta como privada ni pública.
        
- **enp4s0** (tu tarjeta de red física)
    
    - `inet 136.243.37.107/32` → **esta es tu IP pública** (te conecta directo a Internet).
        
    - `inet6 2a01:4f8:212:561::2/64` → tu IP pública en IPv6.
        
    - No aparece ninguna `192.168.x.x` o `10.x.x.x`, lo que indica que tu servidor tiene la IP pública directamente en la interfaz (esto suele pasar en VPS o servidores dedicados).
        
- **docker0, br-**_, veth_**
    
    - Direcciones como `172.17.0.1`, `172.19.0.1`, `172.18.0.1`, `172.20.0.1`, `172.21.0.1`.
        
    - Estas son **IPs privadas internas de Docker**, usadas solo por contenedores en tu máquina.
        
    - No son accesibles desde fuera.