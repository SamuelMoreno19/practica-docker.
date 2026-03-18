# Practica-docker.
- Bienvenido aqui daremos los primeros pasos prácticos con Docker. En estas lecciones, aprenderemos a ejecutar nuestro primer contenedor, gestionar contenedores en ejecución y trabajar con imágenes de Docker.Incluye laboratorios prácticos para el aprendizaje efectivo de los conceptos y temas.

# Lab-Docker extrae una imagen del repositorio.
Usamos docker search para explorar el registro y encontrar una imagen ligera y oficial: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker search <keyword>
La etiqueta [OK] confirma que la imagen es mantenida por el equipo oficial, garantizando seguridad y eficiencia:@SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker search alpine
NAME                DESCRIPTION                                     STARS     OFFICIAL
alpine              A minimal Docker image based on Alpine Linux…   11477     [OK]
alpine/git          A  simple git container running in alpine li…   252       
alpine/socat        Run socat command in alpine container           115       
alpine/curl                                                         12        
alpine/helm         Auto-trigger docker build for kubernetes hel…   70        
alpine/k8s          Kubernetes toolbox for EKS (kubectl, helm, i…   65        
alpine/bombardier   Auto-trigger docker build for bombardier whe…   28        
alpine/httpie       Auto-trigger docker build for `httpie` when …   22        
alpine/terragrunt   Auto-trigger docker build for terragrunt whe…   18        
alpine/openssl      openssl                                         8         
alpine/kubectl      Kubernetes command-line tool for managing cl…   1         
alpine/flake8       Auto-trigger docker build for fake8 via ci c…   2         
alpine/psql         psql — The PostgreSQL Command-Line Client       4         
alpine/ansible      run ansible and ansible-playbook in docker      36        
alpine/jmeter       run jmeter in Docker                            9         
alpine/semver       Docker tool for semantic versioning             4         
alpine/java         Repo containing the build scripts to produce…   5         
alpine/xml          several xml tools to work on xml file as jq …   2         
alpine/openclaw     OpenClaw - Your own personal AI assistant. A…   74        
alpine/mongosh      mongosh - MongoDB Command Line Database Tools   2         
alpine/mysql        mysql client                                    7         
alpine/cfn-nag      Auto-trigger docker build for cfn-nag when n…   0         
alpine/gcloud       Auto-trigger docker build for gcloud (google…   0         
alpine/crane                                                        0         
alpine/bundle       This repository has been archived by the own…   1       

Descargamos la imagen alpine desde el repositorio remoto a nuestro entorno local en Codespaces, y docker descarga la capa única de Alpine y verifica su integridad mediante el Digest: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker pull alpine
Using default tag: latest
latest: Pulling from library/alpine
589002ba0eae: Pull complete 
Digest: sha256:25109184c71bdad752c8312a8623239686a9a2071e8825f20acb8f2198c3f659
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest

Se hace la Localización de recursos oficiales, le descargamos las de capas de la imagen. Y luego desplegamos e interactuamos con el entorno aislado: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker run -it --name alpine_container alpine /bin/sh
/ # ls -a
.           .dockerenv  dev         home        media       opt         root        sbin        sys         usr
..          bin         etc         lib         mnt         proc        run         srv         tmp         var
/ # 

# Lab-Docker Run a Container
Actualizamos la lista de paquetes del sistema y descargamos el motor de Docker para poder crear, descargar y correr contenedores: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $sudo apt update sudo apt install docker.io

Este comando activa el servicio Docker: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo systemctl start docker

Comprueba si Docker está activo y se está ejecutando correctamente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo systemctl status docker

En este entorno, la configuración de permisos viene predefinida de fábrica. No es necesario agregar el usuario al grupo docker ni cerrar sesión para que los cambios surtan efecto; el motor está listo para operar desde el primer comando: sudo usermod -aG docker $USER

Descargamos la imagen de prueba oficial para confirmar que el motor de Docker tiene acceso al registro externo, La descarga exitosa de esta imagen confirma que nuestra conexión al Docker Hub está activa y funcional: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete 
Digest: sha256:85404b3c53951c3ff5d40de0972b1bb21fafa2e8daa235355baf44f33db9dbdd
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest

Ejecutamos la imagen de prueba para confirmar que el motor de Docker crea, gestiona y comunica los contenedores correctamente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash
Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/
For more examples and ideas, visit:
 https://docs.docker.com/get-started/

 Validamos el estado de todos los contenedores creados en la sesión, incluyendo los que ya finalizaron su tarea: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker ps -a
CONTAINER ID   IMAGE         COMMAND     CREATED          STATUS                       PORTS     NAMES
a385ccf7fb0c   hello-world   "/hello"    52 seconds ago   Exited (0) 52 seconds ago              crazy_meitner
66308933ca02   alpine        "/bin/sh"   13 minutes ago   Exited (130) 9 minutes ago             alpine_container

Para misiones más complejas, descargamos una imagen de infraestructura robusta como Nginx, A diferencia de las imágenes minimalistas, Nginx utiliza múltiples capas de software para funcionar. Docker optimiza la descarga gestionando cada capa de forma independiente y verificando su integridad final: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
ec781dee3f47: Pull complete 
980067d12da2: Pull complete 
4174e33a2c9e: Pull complete 
6b40784e4837: Pull complete 
f0b77348d9b0: Pull complete 
0289d65812c3: Pull complete 
9baba07a35b6: Pull complete 
Digest: sha256:dec7a90bd0973b076832dc56933fe876bc014929e14b4ec49923951405370112
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

Se validó no solo la gestión de imágenes livianas, sino también el despliegue de infraestructura web funcional con mapeo de puertos y ejecución en segundo plano: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker run -d -p 80:80 nginx
28c66715a54b941292dc34378565903f894396ad372cff3edd13d8076120615b

Verificar que el contenedor Nginx esté ejecutándose correctamente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                 NAMES
28c66715a54b   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, [::]:80->80/tcp   elastic_euclid

# Lab-Contenedores de listas de Docker
En GitHub Codespaces, el espacio de trabajo principal se ubica en /workspaces/, eliminando la necesidad de navegar hacia carpetas de usuario tradicionales como ~/project: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ cd ~/project
bash: cd: /home/codespace/project: No such file or directory

 Este comando se utiliza para poder enumerar todos los contenedores:@SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker container ls -a
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                        PORTS                                 NAMES
28c66715a54b   nginx         "/docker-entrypoint.…"   4 minutes ago    Up 4 minutes                  0.0.0.0:80->80/tcp, [::]:80->80/tcp   elastic_euclid
a385ccf7fb0c   hello-world   "/hello"                 6 minutes ago    Exited (0) 6 minutes ago                                            crazy_meitner
66308933ca02   alpine        "/bin/sh"                19 minutes ago   Exited (130) 15 minutes ago                                         alpine_container

Validamos la capacidad de Docker para reportar estados de contenedores específicos, incluso cuando no existen: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker container inspect jenkins
[]
Error response from daemon: No such container: jenkins

Utilizamos el modo "silencioso" para listar todos los contenedores existentes, incluso aquellos que no están visibles en la ejecución activa.@SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker container ls -aq
28c66715a54b
a385ccf7fb0c
66308933ca02

# Lab-Contenedores en ejecución con listas de Docker
A diferencia del comando -aq, docker ps funciona como un radar de tráfico en vivo, mostrando solo los motores que estan en el entorno de GitHub Codespaces: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                 NAMES
28c66715a54b   nginx     "/docker-entrypoint.…"   8 minutes ago   Up 8 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   elastic_euclid

Utilizamos filtros avanzados para localizar contenedores específicos por su identificador nominal dentro de la plataforma: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps --filter "name=jenkins"
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

Para finalizar, realizamos una auditoría de todos los recursos, comparando contenedores activos y finalizados en una sola vista, y el puerto corriendo correctamente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                        PORTS                                 NAMES
28c66715a54b   nginx         "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes                 0.0.0.0:80->80/tcp, [::]:80->80/tcp   elastic_euclid
a385ccf7fb0c   hello-world   "/hello"                 12 minutes ago   Exited (0) 12 minutes ago                                           crazy_meitner
66308933ca02   alpine        "/bin/sh"                25 minutes ago   Exited (130) 21 minutes ago    

# Laboratorio 4 : Configuración de un contenedor con la imagen mariadb
Para entornos que requieren persistencia y gestión de datos, desplegamos un motor de base de datos MariaDB configurado con variables de entorno: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker run -d --name some-mariadb -e MYSQL_ROOT_PASSWORD=my-secret-pw mariadb
Unable to find image 'mariadb:latest' locally
latest: Pulling from library/mariadb
817807f3c64e: Pull complete 
a9feb2f7987f: Pull complete 
1e2712d6dc88: Pull complete 
36b90120c666: Pull complete 
94e06fb80927: Pull complete 
8acc8dacec09: Pull complete 
ef13546effa3: Pull complete 
96a71e654f6a: Pull complete 
Digest: sha256:e16f61b8f6ed25111adbb1c5c19bbc2904efc8ed14029999af0cbe1c7ae18bf1
Status: Downloaded newer image for mariadb:latest
8ad7fb72a4e21383ef8ecea0aefeb358cbd9e961ffb386c13280c10c5b49af94

Validamos la coexistencia de múltiples servicios de infraestructura, cada uno operando en su propio entorno aislado pero dentro del mismo motor de Docker: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                 NAMES
8ad7fb72a4e2   mariadb   "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp                              some-mariadb
28c66715a54b   nginx     "/docker-entrypoint.…"   13 minutes ago       Up 13 minutes       0.0.0.0:80->80/tcp, [::]:80->80/tcp   elastic_euclid

Se demostró la capacidad de auditar y gestionar servicios en tiempo real sin necesidad de detener los procesos, garantizando la integridad de la configuración en caliente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker exec -it some-mariadb env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=8ad7fb72a4e2
TERM=xterm
MYSQL_ROOT_PASSWORD=my-secret-pw
GOSU_VERSION=1.19
LANG=C.UTF-8
MARIADB_VERSION=1:12.2.2+maria~ubu2404
HOME=/root

Validamos la integridad del servicio entrando directamente a la terminal de MariaDB y autenticándonos mediante las credenciales inyectadas: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker exec -it some-mariadb bash 
root@8ad7fb72a4e2:/# 
root@8ad7fb72a4e2:/# mariadb -u root -p"$MYSQL_ROOT_PASSWORD"
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 12.2.2-MariaDB-ubu2404 mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 

Con este comando nos pedira directamente la contraseña guardada para poder entrar a mariaDB: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker exec -it some-mariadb mariadb -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 5
Server version: 12.2.2-MariaDB-ubu2404 mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 

Eliminar el contenedor creado anteriormente o (mariaDB):@SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $  docker rm -f some-mariadb
some-mariadb

Configuramos el acceso externo a MariaDB vinculando el puerto del sistema anfitrión con el del contenedor, permitiendo conexiones desde clientes externos o aplicaciones en el mismo entorno: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker run -d -p 3306:3306 --name some-mariadb -e MYSQL_ROOT_PASSWORD=my-secret-pw mariadb
230e47aae0bc65386b7bef2304163e68d6a10dc1baf86283fcafcb45d70cba01

Finalizamos con una arquitectura funcional de dos capas, donde ambos servicios están expuestos y operativos simultáneamente en el puerto espacial: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                         NAMES
230e47aae0bc   mariadb   "docker-entrypoint.s…"   52 seconds ago   Up 52 seconds   0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp   some-mariadb
28c66715a54b   nginx     "/docker-entrypoint.…"   19 minutes ago   Up 19 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp           elastic_euclid

En el mundo de los contenedores, la mejor práctica es no ensuciar el host. Si el contenedor ya tiene la herramienta, la usamos desde ahí. Así podemos mantener el Codespace ligero y organizado: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker exec -it some-mariadb mariadb -u root -p -h localhost
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 12.2.2-MariaDB-ubu2404 mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 

# Practica-Búsqueda de imágenes del repositorio
Para completar la primera tarea, extraemos la imagen oficial de servidor web para nuestra infraestructura: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:dec7a90bd0973b076832dc56933fe876bc014929e14b4ec49923951405370112
Status: Image is up to date for nginx:latest
docker.io/library/nginx:latest

En esta fase de la misión, recolectamos recursos ligeros (alpine) y robustos (ubuntu) para diversificar nuestro arsenal de contenedores: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker pull alpine
Using default tag: latest
latest: Pulling from library/alpine
Digest: sha256:25109184c71bdad752c8312a8623239686a9a2071e8825f20acb8f2198c3f659
Status: Image is up to date for alpine:latest
docker.io/library/alpine:latest

@SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
817807f3c64e: Already exists 
Digest: sha256:0d39fcc8335d6d74d5502f6df2d30119ff4790ebbb60b364818d5112d9e3e932
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

El comando docker images actúa como nuestro inventario de realidad virtual, permitiéndonos ver qué herramientas tenemos disponibles localmente: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
mariadb       latest    16a5cac03562   43 hours ago   336MB
nginx         latest    1a1e63136420   46 hours ago   161MB
ubuntu        latest    f794f40ddfff   3 weeks ago    78.1MB
alpine        latest    a40c03cbb81c   7 weeks ago    8.44MB
hello-world   latest    1b44b5a3e06a   7 months ago   10.1kB

# Practica-Despliegue de batallas espaciales dockerizadas
Para garantizar una plataforma de comunicación segura entre las naves, desplegamos un servidor Nginx que actuará como nuestro centro de control de mensajes: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker run -d -p 80:80 --name comunicaciones-flota nginx
049d8de3c5436fe416bbbf5064e4796c86a0d8649789c884550c3ab9b793592e

Podemos utilizar el comando ps para poder verificar que se este ejecutando y escuchando el puerto 80: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                 NAMES
049d8de3c543   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, [::]:80->80/tcp   comunicaciones-flota

Para la transmisión ligera y segura de coordenadas tácticas, desplegamos un nodo alpine. Debido a su diseño minimalista, es el contenedor ideal para operaciones rápidas en naves de exploración: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker run -dit --name nodo-datos-alpine alpine
23725dc5e9f32a272858c6a958eb39f7626ed281917730771c9b94c88f21c292

Para que verifiquemos que todo este correcto sera el siguiente comando: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                 NAMES
23725dc5e9f3   alpine    "/bin/sh"                5 minutes ago   Up 5 minutes                                         nodo-datos-alpine
049d8de3c543   nginx     "/docker-entrypoint.…"   8 minutes ago   Up 8 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   comunicaciones-flota

# Practica-Docker Container Identification
Como primer paso, generamos un reporte oficial de todos los contenedores activos en la arena, extrayendo sus identificadores, imágenes y nombres: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps --format "{{.ID}} {{.Image}} {{.Names}}" > containers.txt

Validamos el contenido de los archivos de texto creados mediante la terminal. Estos archivos sirven como evidencia de los contenedores que estuvieron activos durante la jornada: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ cat containers.txt
23725dc5e9f3 alpine nodo-datos-alpine
049d8de3c543 nginx comunicaciones-flota

Filtramos los contenedores que usan la imagen jenkins/jenkins y guardamos el report: @SamuelMoreno19 ➜ /workspaces/practica-docker. (main) $ docker ps --filter "ancestor=jenkins/jenkins" --format "table {{.ID}}\t{{.Image}}\t{{.Names}}" > container_jenkins.txt

e confirma que no hay instancias de Jenkins consumiendo recursos en el entorno de pruebas actual, manteniendo el "puerto espacial" optimizado para los laboratorios de Nginx y Alpine: container_jenkins.txt: 
CONTAINER ID   IMAGE     NAMES


