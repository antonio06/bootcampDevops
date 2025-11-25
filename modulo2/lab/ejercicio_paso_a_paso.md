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

- Crear imagen de mongo

```bash
  docker run -d --name LemoncodeCourseDb --network lemoncode-network -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=example -v mongo-data:/data/db mongo:8.2.1
```

## Reto 2: Dockerizar el Backend

- Crear imagen a traves del dockerfile de `./backend`

```bash
  docker build -t topics-api:v1 ./backend/.

  docker run -d --network lemoncode-network -p 5000:5000 topics-api:v1
```
