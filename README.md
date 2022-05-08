# Docker-Course
### Componentes DENTRO del circulo de Docker:

* Docker daemon: Es el centro de docker, el corazón que gracias a el, podemos comunicarnos con los servicios de docker.
* REST API: Esta simplemente expone la interfaz necesaria para poder comunicarse con el docker daemon.
* Cliente de docker: Gracias a este componente, podemos comunicarnos con el corazón de docker (Docker Daemon) que por defecto es la línea de comandos.
Dentro de la arquitectura de Docker encontramos:

* Contenedores: Es la razón de ser de Docker, es donde podemos encapsular nuestras imagenes para llevarlas a otra computadora, o servidor, etc.
* Imagenes: Son las encapsulaciones de x contenedor. Podemos correr nuestra aplicación en Java por medio de una imagen, podemos utilizar Ubuntu para correr nuestro proyecto, etc.
* Volumenes de datos: Podemos acceder con seguridad al sistema de archivos de nuestra máquina.
Redes: Son las que permiten la comunicación entre contenedores.

![image](https://user-images.githubusercontent.com/72711545/167314824-93f7b4e3-eec9-4da5-b5e4-ba337fd331d0.png)

### Primeros Pasos - Hello World
* Es importante tener una cuenta en Docker Hub
* Correr el primer componente: ``` docker run hello-world ```
![image](https://user-images.githubusercontent.com/72711545/167314943-0ccf4064-7e30-44d7-a1c2-23fc2f34cfc5.png)

### Conceptos Fundamentales
#### ¿Qué es un contenedor?
* Es una agrupación de n procesos que corren de forma nativa en la maquina, peor están aislados del resto del sistema. 
* El contenedor es una unidad lógica, no como la maquina virtual es que es una agrupación fisica y virtualizada, que tiene las abstracciones de memoria, cpu, etc.
* Un contenedor es una agrupación de procesos, entidad lógica. 
* Los procesos que se ejecutan en los contenedores sólo tienen rango de acción dentro del espacio del contenedor que se ejecutan. 
* Los contenedores son versátiles, ya que son ligeras y contienen todas las dependencias para su ejecución, garantizando su ejecución en todos lados. 
* Los contenedores son más eficientes, ya que comparten los archivos del sistema base con otros contenedores de manera inmutable. No ejecutan todo el OS, sino sólo procesos.

### Comprendiendo el estado de Docker
- ``` docker run hello-world``` (corro el contenedor hello-world)
- ``` docker ps ``` (muestra los contenedores activos)
- ``` docker ps -a ```(muestra todos los contenedores)
- ``` docker inspect  <containe ID>``` (muestra el detalle completo de un contenedor)
- ``` docker inspect  <name>``` (igual que el anterior pero invocado con el nombre)
- ``` docker run –-name hello-gabriela hello-world``` (le asigno un nombre custom “hello-gabriela”)
- ``` docker rename hello-gabriela hola-vasti``` (cambio el nombre de hello-gabriela a hola-vasti)
- ``` docker rm <ID o nombre>``` (borro un contenedor)
- ``` docker container prune``` (borro todos lo contenedores que esten parados)

### El modo interactivo
- ```docker run ubuntu ``` (corre un ubuntu pero lo deja apagado)
- ```docker ps -a ``` (lista todos los contenedores)
- ```docker run -it ubuntu ``` (lo corre y entro al shell de ubuntu)
* -i: interactivo
* -t: abre la consola
- ```cat /etc/lsb-release``` (veo la versión de Linux)
- ``` exit ```

### Ciclo de vida de un contenedor
- ```docker ps -a ``` (veo todos los contenedores)
- ```docker --name <nombre> -d ubuntu -f <comando>```
- ```docker --name alwaysup -d ubuntu tail -f /dev/null ```(mantiene el contenedor activo)
- ```docker exec -it alwaysup bash ```(entro al contenedor)
- ```docker inspect --format ‘{{.State.Pid}}’ alwaysup ```(veo el main process del ubuntu)
- desde Linux si ejecuto ``` kill -9 <PID> `` `mata el proceso dentro del contenedor de ubuntu pero desde MAC y windows no funciona
- Para ejecutar un contenedor activando el modo interactivo pero dejándolo en background (con el fin de acceder a él después) usamos los parámetros “d”, “i” y “t” el -d flag significa detached: ```docker run --name [nameContainer] -dit ubuntu ```
- Para detener un contenedor en windows: ``` docker stop <container_id or container_name>```

### Exponiendo contenedores
- ``` docker run -d --name proxy nginx``` (corro un nginx)
- ```docker stop proxy``` (apaga el contenedor)
- ```docker rm proxy``` (borro el contenedor)
- ```docker rm -f <contenedor> ```(lo para y lo borra)
- ```docker run -d --name proxy -p 8080:80 nginx ```(corro un nginx y expongo el puerto 80 del contenedor en el puerto 8080 de mi máquina)
- localhost:8080 (desde mi navegador compruebo que funcione)
- ```docker logs proxy ```(veo los logs)
- ```docker logs -f proxy ``` (hago un follow del log)
- ```docker logs --tail 10 -f proxy ```(veo y sigo solo las 10 últimas entradas del log)

