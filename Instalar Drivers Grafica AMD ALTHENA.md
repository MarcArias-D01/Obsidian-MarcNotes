---
tags:
  - linux
  - AMD
  - gpu
date: 2026-05-12
---
### Primero hemos de saber que gráfica hay instalada si necesidad de driver ni nada. Al inicio no suele haber ningún driver instalado

```bash
lspci | grep -i vga
```

Resultado esperado:
> 0002:00:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Vega 10 [Instinct MI25 MxGPU/MI25x2 MxGPU/V340 MxGPU/V340L MxGPU]

En este ejemplo vemos uan gráfica AMD InstinctMI25 

El driver de AMD es el `rocm-smi`

```bash 
sudo apt install rocm-smi
```

Testeamos que funciona `rocm-smi`

En Azure, las máquinas con AMD (como las series NVv4) requieren pasos específicos porque el kernel estándar de Ubuntu a veces no trae el módulo `amdgpu` configurado para estas gráficas de servidor.

Prueba a forzar la carga del módulo:
```bash
sudo modprobe amdgpu
```

Fallo debido a que no puede acceder a donde esta la gráfico seguramente a que esta virtualizada. Se queda sin hacer nada. Realizamos un `rebot`


Ubuntu Noble tiene paquetes para ROCm directamente en sus repositorios oficiales. Prueba esto:
```bash
sudo apt install libamd-comgr2 librocm-smi64-1 rock-dkms-firmware -y
```

