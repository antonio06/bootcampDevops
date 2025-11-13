# Apuntes de Docker

- Ejecutar un contenedor (si no está la imagen la descarga): `docker run -d -p 8080:80 nginx`

-d => detach
-p => port (define un puerto)

OJO! al final siempre va el nombre de la imagen.

- Listar contenedores `docker ps` que están ejecutándose
- Parar un contendor `docker stop nombre_contedor`
- Listar todos los contenedores `docker ps -a`
- Renombrar un contenedor `docker rename antiguo_nombre nuevo_nombre`
- Contruir una imagen a través de un Dockerfile => `docker build -t mi-aplicacion-web:v1 .`
- Listar imágenes `docker images`
