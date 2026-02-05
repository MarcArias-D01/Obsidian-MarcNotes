---
tags:
  - docker
  - linux
  - gpu
---
- [GPU]
Docker es **una plataforma para desarrollar, enviar y ejecutar aplicaciones dentro de contenedores**. Dicho de forma más clara y práctica:
### Concepto básico

- Un **contenedor** es como una caja que incluye **todo lo que tu aplicación necesita**: código, librerías, dependencias y sistema operativo mínimo.
- Gracias a los contenedores, puedes ejecutar tu aplicación en cualquier máquina que tenga Docker, sin preocuparte por diferencias entre sistemas.


Para ejecutar un `compose.yml` con el archivo `.env` especifico: 
```bash
docker compose --env-file .env.dev up
```


Para copiar archivos dentro de un docker:
```bash
docker cp CertificadoSharepointConnector.pfx airflow_airflow-webserver_1:/opt/airflow/
```


Para crear una Network:
```bash
docker network create my_network --driver bridge
```

Importante si **bindeas volumnes**
```bash
mkdir -p tu_volumen
sudo chown -R 1000:1000 tu_volumen  # UID/GID típicos contenedores
```

# GPU
Si quieres que tus contenedores utilicen **GPU**

```bash
# 1. Añadir repositorio NVIDIA
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# 2. Instalar
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit

# 3. Configurar Docker runtime
sudo nvidia-ctk runtime configure --runtime=docker

# 4. Reiniciar Docker
sudo systemctl restart docker
```

Para verificar:
```bash
nvidia-smi
# Debe mostrar tu GPU


docker run --rm --gpus all nvidia/cuda:12.6.2-base-ubuntu24.04 nvidia-smi # TEST


docker run --rm --gpus all ubuntu nvidia-smi # TEST simple


# Verificar runtime configurado
docker info | grep -i nvidia
# Debe mostrar: Runtimes: nvidia runc ...
```
