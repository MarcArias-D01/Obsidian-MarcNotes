#linux/command #dev

Docker es **una plataforma para desarrollar, enviar y ejecutar aplicaciones dentro de contenedores**. Dicho de forma más clara y práctica:
### Concepto básico

- Un **contenedor** es como una caja que incluye **todo lo que tu aplicación necesita**: código, librerías, dependencias y sistema operativo mínimo.
- Gracias a los contenedores, puedes ejecutar tu aplicación en cualquier máquina que tenga Docker, sin preocuparte por diferencias entre sistemas.

Para ejecutar un `compose.yml` con el archivo `.env` especifico:

```bash
docker compose --env-file .env.dev up
```

