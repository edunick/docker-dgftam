# docker-dgftam
<h3>Pasos para despligue de sistemas DGFTAM</h3>

<strong>Levantando nginx, php-fpm, certbot</strong>
1) Instalar docker para ubuntu 18.04 https://phoenixnap.com/kb/how-to-install-docker-on-ubuntu-18-04
2) Instalar docker-compose para ubuntu 18.04 https://linuxize.com/post/how-to-install-and-use-docker-compose-on-ubuntu-18-04/
3) Crear la red fortalecimiento #docker network create fortalecimiento
4) Crear la carpeta <strong>release/</strong> en la raiz del sistema operativo root@sigm-dgft:/# ls
5) Clonar este repositorio para eso entrar a: #cd /release y luego #git clone https://github.com/edunick/docker-dgftam.git nginx-cerbot
6) Entrar a #cd /release/nginx-cerbot
7) Dentro de data/nginx dejar todos los archivos .conf que vamos a usar segun los dominios que tengamos
8) Volver a #cd /release/nginx-cerbot y editar #nano init-letsencrypt.sh alli en domains=(midominio.com) ponemos el dominio o sub-dominio que necesitamos agregar, ctrol-x guardar y salir.
9) Levantar los contenedores con #docker-compose up -d
10) Si queremos agregar otro sub-dominio volver al paso 6)-8)

<strong>Levantando PostgresSQL y PGAdmin</strong>

1) Entrar a release/nginx-certbot/data/postgres ahi esta el Dockerfile para el postgres

  Construimos la imagen con el siguiente comando #docker build -t eg_postgresql .
  Esto va a crear por defecto
  usr: docker
  database: docker
  pass: docker

  Si quisieramos cambiar los valores hay que editar el Dockerfile y reconstruir la imagen
  Luego instanciamos el contenedor
  #docker run -d -p 5432:5432 --network="fortalecimiento" --name serverdb eg_postgresql
  
2) Ejecutar lo siguiente para el PgAdmin
  Traemos la imagen #docker pull dpage/pgadmin4
  Luego instanciamos el contenedor
  docker run -p 8080:80 --name pgadmin --network="fortalecimiento" -e "PGADMIN_DEFAULT_EMAIL=edunick@gmail.com" -e "PGADMIN_DEFAULT_PASSWORD=docker" -d dpage/pgadmin4

