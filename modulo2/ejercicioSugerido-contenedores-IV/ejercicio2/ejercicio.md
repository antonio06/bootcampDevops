## Creación del volumen

`docker volume create confetti-data`

## Listar los volúmenes

`docker volume ls`

## Creación de los contenedores y vincular el volumen

docker run -d --name nginx-con-volumen --mount source=confetti-data,target=/usr/share/nginx/html -p 8081:80 nginx

docker run -d --name httpd-con-volumen --mount source=confetti-data,target=/usr/local/apache2/htdocs/ -p 8082:80 httpd:trixie

## Asignar el volumen al contenedor

docker cp ejercicio2/. nginx-con-volumen:/usr/share/nginx/html

docker cp ejercicio2/. httpd-con-volumen:/usr/local/apache2/htdocs/
