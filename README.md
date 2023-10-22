# Wordpress_docker

## Instalacion de docker mediante un docker compose
Una vez se tiene el docker compose es muy sencillo creamos el archivo 'docker-compose.yml' y luego inicializamos el contenedor.

<img width="200" alt="image" src="https://github.com/FranciscoFerreiraT/Wordpress_docker/assets/92456485/06c65a4d-25f6-4088-b798-59f8e8e58762">

Como podemos ver los contenedores ya estarian creados e iniciados

## Explicacion de los parametros del docker-compose

```bash 
version: '3.3' #Esto indica la versión de Docker Compose que se está utilizando

services: #Aqui comienza la seccion de la definicion de los servicios
   db: #Esto define el servicio que tendra la base de datos SQL
     image: mysql:5.7 #Especifica la imagen que utilizaremos
     ports: #Puertos del contenedor host
       - "3307:3306"
     volumes: #Aqui se crean los volumenes de la base de datos
       - db_data:/var/lib/mysql
     environment: #Aqui configuramos el entorno de la base de datos y le indicamos la contraseña,nombre,usuario y root
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress: #Esto define el servicio de wordpress
     depends_on:
       - db #Esto hace que el servicio wordpress utilice la base de datos creada anteriormente
     image: wordpress:latest #Esto especifica la imagen de docker
     ports: #Aqui se mapea el puerto 80 del contenedor al puerto 8000 del host
       - "8000:80"
     volumes: #Se asocia el directorio local 
       - ./html:/var/www/html
     environment: #Aqui se crea las variables de entorno
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes: # y finalmente se define un volumen para la base de datos MYSQL
    db_data: {}

```


## Demostracion funcionamiento de Wordpress

<img width="941" alt="image" src="https://github.com/FranciscoFerreiraT/Wordpress_docker/assets/92456485/af9a43b6-6be3-48cd-982c-113ad2230436">

<img width="871" alt="image" src="https://github.com/FranciscoFerreiraT/Wordpress_docker/assets/92456485/d023a29e-dc71-47fc-9d8f-b66288214a69">

<img width="1229" alt="image" src="https://github.com/FranciscoFerreiraT/Wordpress_docker/assets/92456485/ed4665c8-a802-45b6-9603-f749f6f57e76">



