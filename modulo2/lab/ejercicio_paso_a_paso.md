# Ejercicio Resuelto

## Imagen de mongo

- version => mongo:8.2.1

## Imagen node

- nodejs

## Reto 1: MongoDB en Contenedor

- Crear network

```bash
  docker network create lemoncode-network

  docker network ls
```

![Listado newtwork](./imagenes/listado-network.png)

- Crear contenedor de mongo

```bash
  docker volume create mongo-data

  docker run -d --name mongo-db --network lemoncode-network -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password -v mongo-data:/data/db mongo:8.2.1
```

## Reto 2: Dockerizar el Backend

- Crear contenedor a traves del dockerfile de `./backend`

```bash
  docker build -t calendar-api:v1 .

  docker run -d --network lemoncode-network -e DATABASE_URL="mongodb://admin:password@mongo-db:27017" -p 5000:5000 --name calendar-backend calendar-api:v1
```

Después de crear el contenedor:

Crear fichero `.env` con las siguientes variables de entorno.

```node
DATABASE_URL=mongodb://admin:password@localhost:27017
DATABASE_NAME=LemoncodeCourseDb
HOST=localhost
PORT=5000
```

Revisar de que el contenedor funciona correctamente con el comando `docker logs`

![Docker logs](./imagenes/docker-logs.png)

Ejecutado el comando `npm start`

![Conectando api](./imagenes/conectando-api.png)

Capturas de añadiendo objetos a la base de datos (postman)

![Postman](./imagenes/postman.png)

Listado de los datos:

![Listado elementos](./imagenes/listado-elementos.png)

## Reto 3: Dockerizar el Frontend

- Crear contenedor a traves del dockerfile de `./frontend`

```bash
docker build -t calendar-front:v1 .

docker run -d --network lemoncode-network -p 3000:3000 --name calendar-front calendar-front:v1
```

Ejecutamos el comando `npm start`

![Ejecutando app final](./imagenes/ejecutando-app-final.png)
