# Imagenes y contenedores

### Imagen
Una imagen se como una plantilla de lectura quue contiene las instrucciones para crear un contenedor en Docker, donde a su vez estas imagenes se basan en otras. se pueden crear imagenes propios o se pueden usar otras que ya fueron diseñadas por otros.

Para crear una imagen se debe usar Dockerfile y se emplean unos comandos básicos. No se puede modificar una imagen, crea imagen desde una imagen, ya que las imagenes son  estaticas.

### Contenedor
Un contenedor es una especie de prototipo ejecutable que se basa de una imagen. Un solo contenedor está relativamente bien asilado de otros y a su vez de la maquina host, donde se tiene control de dicha de red. Estos se definen por su imagen y las opciones de configuracíon. Al momento de elminar un contenedor si alguno de sus cambios no esta almacenado este tambien desaparecerá.

## Crear imagen y contenedor en Dockerfile
  Utilizaremos el MobaXterm para hacer uso de la máquina virtual del sistema Linux, donde se realizarán los siguientes pasos:
  1. Se va a crear un directorio llamado mi-primer-docker-file:
  >mkdir mi-primer-docker-file

  2. Avanzamos a nuestra nueva carpeta y se crea un archivo con el editor vim
  >vim Dockerfile
  dentro de este archivo debemos pegar el archivo RUN

  3. De nuevo en nuestra creamos otra nueva llamada tatic-html-directory
  >$mkdir static-html-directory

  4. dentro de esta nueva carpteta creamos nuestro arcivho que visualizaremos en este caso un html y colocaremos la información que deseamos desplegar
  >$ vim index.html
  Ya con estos dos archivos y directorios estamos listos para crear nuestro contenedor

  5. Basados en una imagen de la pagina de Docker Hub utilizaremos uno de la empresa _NGINX_ y ejecutamos el comando:
  >$docker image build -t some-content-nginx .

  6. Podemos listar nuestras imagenes actuales con el comando.
  >$ docker image ls
  Y allí visualizar la que creamos recientemente que debe llamarse *some-content-nginx*

  7. Ahora ponemos a correr nuestra imagen para poderla ver en un navegador web, haiblitandole un puerto con el siguiente comando
  >$docker run --name some-nginx -d -p 8080:80 some-content-nginx
  En este caso se habilitó el puerto 80 y se hace un mapeo del puerto 8080 del host al contenedor.
  *Donde:*
  - -d se corre en background
  - -p administrar nuestros puertos

  8. Para verificar la conectividad de la URL implementamos el comando:
  >curl -k localhost:8080
  *Donde:*
  - -k no me verifica la seguridad-
  9. Ya podemos visualizar nuestra imagen en nuestro navegador web con la ip:8080

  ## Subir un repositorio a Docker-Hub
  1. Se debe crear una cuenta en https://hub.docker.com/

  2. Crear un repositorio 

  3. Por consola en MobaXterm digitar el comando:
  > docker login

  4.  Ingresar el username y password con el que se registro en la pagina web

  5. Ingresar el comando  para crear el repositorio con el nombre que tenia en estte caso *some-content-nginx*
  > docker tag some-content-nginx johnsebas94/fedesoft-web

  6. Por ultimo hacer un push para subir nuestra imagen
  > docker push johnsebas94/fedesoft-web
  
  7. Listo la imagen ya esta en nuestro sitio Web, en mi caso mi  imagen esta en el link: *_https://hub.docker.com/repository/docker/johnsebas94/fedesoft-web_*

  8. Para ellminar una imagen se utiliza el siguiente comando, en este caso con el ejemplo seria:
  >docker image rm johnsebas94/fedesoft-web