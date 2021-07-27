# Archivo Docker Compose

Es una herramienta que ayuda a definir y compartir  aplicaciones de varios contenedores.
Con el archivo compose se pueden crear archivos en formato .yml para definir los servicios, a su vez estos archivos permiten que un tercero pueda contribuir en un proyecto y tener control de la versiones.

## Instalación de Docker Compose 
1. En un sistema Linux se debe instalar con el comando: 
-docker-compose version

## Creación del archivo de Compose
1. Se puede crear un directorio para luego allí crear al archivo .yml
-sebastian@ubuntutibaquira:~$ mkdir proxy

2. Crear el archivo .yml con vim
-sebastian@ubuntutibaquira:~/proxy$ vim docker-compose.yml

3. Con el archivo compose lo primero  que se debe definir la version. Donde por lo general es recomendable utilizar la ultima versión. y luego definir la lista de servicios o contenedores como lo conocemos que queremos ejecutar.

Como primera entrada definir el servicio y la imagen del contenedor. Se puede seleccionar cualquier nombre, el cual se convertira en un alisas.

lb: es el load balance que fucniona para balancear las peticones dle servicio.

Como ventaja los volúmenes en Docker compose pueden usar rutas de acceso relativas al directorio actual.

Tambien se debe migrar el dirctorio de trabajo y la asignación de volúmenes *(-v ${PWD}:/app).*

Para definir el elemento con -p, se definde el valor de puertos para el servicio.

version: '3'
services:
  web:
    image: dockercloud/hello-world
  lb:
    image: dockercloud/haproxy
    links:
      - web
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 80:80

Siempre tener en cuenta la identación ya que los espcios son fundamentales para un correcto funcionamiento     

4. Luego con el siguiento comando podemos poner y subir nuestro servicio
- sebastian@ubuntutibaquira:~/proxy$ docker-compose up -d

5. Con este comando podemos observar que servicios estan corriendo y ver si el de nostros ya esta levantado.
- docker-compose up.

6. Listo nuestro servicio puede ser observado en nuestro navegador con la ip y el puerto habilitado
- 192.168.1.27:8080


## Usa compose cuando se clona un archivo

Para esta práctica fue necesario usar un repositorio existente con el fin de poder a llegar alevantar el servicio de Jenkins.

1. Clonar y descargar el repositorio con el siguiente comando;
- sebastian@ubuntutibaquira:~/git clone https://github.com/jsgiraldoh/Jenkins.git

2. Con el repositorio ya descargado se puede ingresar a la carpeta que se genera y abrir el archivo .yml
-sebastian@ubuntutibaquira:~/Jenkins$ cat docker-compose-jenkins.yml

Asi se puede ver la informacion del archivo docker compose, su version, volumenes y puertos de uso.

3. Para levantar el servicio es necesario emplear el comando:
-sebastian@ubuntutibaquira:~/Jenkins$ docker-compose -f docker-compose-jenkins.yml up -d

*Donde:*
  -d es correr en backgorund.
  -f se puede asignar el nombre del servicio

4. Se puede revisar si  nuestro servicio ya se encuentra subido con el comando:
- sebastian@ubuntutibaquira:~/Jenkins$ docker ps

*_Nota:_*
En caso de presentar problemas de ejecución de levantar el servicio es necesario cambiar los permisos y propietario del archivo con los comandos:

- sebastian@ubuntutibaquira:~/Jenkins$ sudo chown sebastian:sebastian jenkins_home/

- sebastian@ubuntutibaquira:~/Jenkins$ sudo chmod 2777 jenkins_home/

5. El servico ya esta casi listo, solo es necesario hacerl el comando logs que me permitira obtener la contraseña con el fin de poder ingresar a la plataforma Jankins

- sebastian@ubuntutibaquira:~/Jenkins$ docker logs -f jenkins

*_Nota:_*
La contraseña siempre sera la que se encuentre entre las 3 filas de asteriscos

*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

7583af7c06b3466685eb9f7756d4582c

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

6. Listo ya puedes utilizar el servidor de automaizacion Jankins

### Tips
 1. Para detener los servicios levantados, ya bien sea por que no se van a usar o por que es necesario liberar memoria ya que esto consume memoria, se puede realizar con el comando:

 - docker-compose down

 2. Se pueden crear mas de un contenedor para evitar problemas si se llega a caer uno de ellos es por esta razón que se pueden usar varos a la vez sin que uno interfiera con el otro.

 - docker-compose up --scale web=5 -d 

 En este caso se crearan 5 contenedores, donde el mismo algoritmo creara un id distinto para cada uno de ellos.

 3. Para detenr un servico se utiliza el comando:
 - docker stop "Container ID"

 Entre comillas puede ir el ID Container paraidentificar cual es que se desea detener

 4. Para reestablecer un servicio se utiliza el comando
 - docker container restart "Container ID"