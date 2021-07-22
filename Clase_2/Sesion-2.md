# Instalacion de Docker en terminal Linux

Para esta clase fue necesario usar la maquina herramienta virtual box  con ubuntu como sistema Linux para llevar acabo la instalacion de Docker.
* _Nota:_ Para mayor facilidad con el uso de la consola de la terminal Linux se utilizó el aplicativo MobaXterm en su version portable para permitir asi la opcion de copiado y pegado de comandos. * 

## Como unir el MobaXterm con el Terminal Linux

En la terminal linux se debe ejecutar el comando:
$ ip a s 

Con este comando es posible visualizar nuestra ip virtual que por lo general comienza en *192.168.x.x*

Ya con la ip nos dirigimos al MobaXterm e ingresamos el comando:
$ ssh #ip -l "nombre de usuario"

ya con esto podremos utilizar la consola de MobaXterm y dar inicio a la instalcion de Docker

## Instalación de Docker

1. Se ingresa el comando:
$  sudo apt-get update
2. Se ingresan  el comando que instala todos los paquetes para usar el repositorio
>sebastian@ubuntutibaquira:~$ sudo apt-get install \
>     apt-transport-https \
>     ca-certificates \
>     curl \
>     gnupg \
>     lsb-release
3. Se ingresa la llave GPG de docker para linux
$ url -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
4. Se ingresa el siguiente comando para configurar el repositorio dependiendo de la arquitectura que se tenga en el sistema
>sebastian@ubuntutibaquira:~$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
5. Ya con esto instalado podemos proceder con la instlacion de docker Engine
>sebastian@ubuntutibaquira:~$ sudo apt-get install docker-ce docker-ce-cli contain                           erd.io
6. Para verificar que nos quedo instalado correctamente el docker Engine ejecutamos:
>sebastian@ubuntutibaquira:~$ sudo docker run hello-world
Debe arrojar en consola  un mesaje que empieza por *Hello from Docker!* y se deplegara una gran cantidad de información.

## Descarga del Docker Compose
Para este caso nos asaremos en el repositorio que tiene Docker en Git Hub
1. Se ingresa a Git Hub y se ubica en el repositorio de Docker donde debemos copiar el HTTPS para obtener el Docker compose
>sebastian@ubuntutibaquira:~$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2. Necesitamos darle permisos de administrador por lo cual con el comando *chmod* podemos asignarselo 
>sebastian@ubuntutibaquira:~$ sudo chmod +x /usr/local/bin/docker-compose
3. Verificamos la verion que se instaló con el comando:
>sebastian@ubuntutibaquira:~$ docker-compose version.

## Ejemplo con Docker Compose
Para este ejemplo nos basamos en un repositorio del profesor Johan Giraldo de su Git Hub
1. Clonar el repositorio:
>git clone https://github.com/jsgiraldoh/Codimd.git
2. Verificamos que se encuentre en nuestro sistema el archivo e ingresamos al directorio que viene en la carpeta *Codimd*, y luego ingresamos el comando:
>sebastian@ubuntutibaquira:~/Codimd$ sudo docker-compose up -d
3. Ya luego de que se cree nuestro contenedor podemos observarlos con el siguiente comando
>sebastian@ubuntutibaquira:~/Codimd$ sudo docker container ls.

Se pudo observar por medio de nuestro navegador que al poner nuestra direccion ip:3000 estamos utilizando un contenedor que me permite editar y escribir archivos MarkDown

### Tips
Podemos utilizar el comando *docker help* para ver las opciones que tenemos en el manejo de Docker
*sudo usermod -aG docker "Nombre_de_usuario"* -> Para evitar que a todos los comandos le anteponga el sudo
*sudo systemctl status docker* -> Para ver el estado de nuestros contendedores ys i esta o no activos
*sudo systemctl enable docker* -> Para habiliar algun contenedor que este detenido

*_Nota:_* Siempre se hace un modulo por contenedor 