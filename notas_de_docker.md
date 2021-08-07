# Notas De Docker

[**Docker**](https://docs.docker.com/get-started/overview/) es una plataforma de código abierto que permite desplegar y gestionar contenedores, usando Docker se puede lograr entre otras cosas que una aplicación este autocontenida y se ejecute en un contenedor, que es básicamente un sistema operativo Linux superligero. Los contenedores en Docker se empacan y despliegan a partir de imágenes, las cuales indican al contenedor todo lo que requiere para ejecutar la aplicación y la forma en la que esta debe ser ejecutada, al desplegarse un nuevo contenedor a partir de una imagen este aprovecha partes del sistema operativo del host para completar las partes necesarias para ejecutarse correctamente. Docker logra esto gracias a su arquitectura por capas, en un contenedor de Docker cada capa corresponde con una parte necesaria para que el contenedor se ejecute como un sistema operativo aislado en el que se ejecutará la aplicación, por esto cuando un nuevo contenedor llega al host empaquetado como imagen y se despliega, al ya estar presentes las capas más pesadas, normalmente del kernel y demas paquetes del sistema operativo, solo hace falta descargar e instalar las más livianas, que por lo general son las dependencias de la aplicación en sí, por lo que no hace falta mover las capas más pesadas usando las imágenes, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados, como los utilizados en las máquinas virtuales.\
Cabe aclarar que el aislamiento de procesos en Docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo del host, no por un sistema operativo virtual que usa el hardware del host.\
Al desplegar aplicaciones en contenedores de Docker se agrega una capa adicional de abstracción (el contenedor en sí) sobre la cual trabaja la aplicación, utilizar esta capa adicional además de aportar las ventajas ya mencionadas también ayuda a simplificar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como lo son los relacionados con la construcción, distribución y ejecución de aplicaciones.

- **Construcción:** Al construir o desarrollar aplicaciones con Docker uno de los principales beneficios es que los entornos de desarrollo y ejecución se vuelven equivalentes, ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a Docker se pueden simular condiciones de ejecución con ciertos recursos limitados.
- **Distribución:** Al distribuir aplicaciones mediante imágenes de Docker se garantiza que las dependencias de la aplicación serán instaladas y que no tendrán conflicto con las del sistema operativo del host ya que se instalan en ambientes aislados, otro beneficio de utilizar imágenes de Docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se altere la aplicación esta se comportará de la misma forma siempre.
- **Ejecución:** Ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además Docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

Otra ventaja de Docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad. Las aplicaciones contenerizadas con Docker (que emplean Docker para construir y desplegar software) tienen varias características, pero las principales son las siguientes.

- **Son flexibles:** Docker Engine puede ejecutarse en casi cualquier parte y un contenedor solo necesita de Docker Engine para ejecutarse, por lo que los contenedores pueden ejecutarse casi en cualquier parte.
- **Son livianas:** Al utilizar la arquitectura por capas y reutilizar partes del sistema operativo del host no hace falta empacar las partes más pesadas del sistema operativo usado en las imágenes, por lo que usualmente las imágenes solo contienen las capas más ligeras de la aplicación.
- **Son portables:** Las imágenes creadas con Docker se ejecutan de la misma forma en cualquier máquina que tenga Docker Engine independientemente de su software o hardware.
- **Tienen un bajo acoplamiento:** Cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos fuera del contenedor para funcionar.
- **Son escalables:** Es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **Son seguras:** Los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones o funciones del sistema operativo del host, a no ser que se configuren manualmente estos accesos.

Docker como plataforma de contenedores se divide en tres capas, con cada una de estas capas es necesario interactuar de cierta forma para para acceder a todas las funcionalidades y poder sacarle provecho a Docker, estas capas son.

- **Docker Daemon:** Es el núcleo de Docker, se encarga de manejar todas las entidades que administra Docker.
- **Rest Api:** Permite comunicar el Docker Daemon con el CLI ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el Docker Daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al Docker Daemon mediante el uso de esta api y que es la única forma de interactuar con el Docker Daemon.
- **Docker CLI:** Interfaz de línea de comandos que se utiliza de forma local para comunicarse con el Docker Daemon, es la forma más sencilla de usar Docker.

Además de las capas con las que es necesario interactuar para usar Docker, Docker también dispone de ciertos recursos o entidades que son los que se utilizan para desplegar, empacar y construir aplicaciones contenerizadas, los cuales son.

- **Contenedores:** Son la clave del funcionamiento de Docker, son ambientes autocontenidos que aprovechan partes del sistema operativo del host para dar a las aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier host con Docker Engine instalado.
- **Imágenes:** Las imágenes son la forma en la cual Docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga Docker Engine instalado.
- **Redes:** Las redes internas de Docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **Volúmenes:** Los volúmenes son la forma que provee Docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos, para poder usarlos en ejecuciones posteriores o simplemente para almacenarlos, los volúmenes a pesar de ser espacios de almacenamiento en el host son totalmente administrados por Docker, lo que los hace inaccesibles para el host.

<br>

## Instalación En Sistemas Mac O Windows

Para realizar la instalación de Docker en MacOS o en Windows basta con descargar de [**Docker Hub**](https://hub.docker.com/) la aplicación de escritorio (Docker Desktop).

<br>

## Instalación En Sistemas Ubuntu

Esta pequeña guía de instalación está basada en la [**Guía Oficial**](https://docs.docker.com/engine/install/ubuntu/) ofrecida en Docker Hub para instalar Docker Engine en Ubuntu mediante el sistema de repositorios, cabe aclarar que en Linux no hace falta instalar Docker Desktop como en Mac o en Windows, con solo Docker Engine es suficiente y además la manipulación del Docker Daemon en Linux se hace solo mediante el Docker CLI, sin interfaz gráfica, este proceso de instalación aplica para las siguientes versiones de Ubuntu.

- Ubuntu Focal 20.04 (lts)
- Ubuntu Groovy 20.10
- Ubuntu Bionic 18.04 (lts)
- Ubuntu Xenial 16.04 (lts)

<br>

### Comandos De Instalación

```bash
sudo apt-get update

sudo apt-get remove docker docker-engine docker.io containerd runc
```

Antes de iniciar con la instalación es necesario eliminar cualquier instalación previa de Docker que se haya hecho en host, si no han habido instalaciones previas de Docker se puede omitir el primer comando.

```bash
sudo apt-get update

sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
```

Luego de haber desinstalado las versiones anteriores de Docker se configuran los repositorios necesarios para instalar Docker Engine.

```bash
curl -fssl https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Tras configurar los repositorios necesarios lo siguiente es descargar la llave GPG oficial de docker.

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Una vez descargada la llave GPG lo siguiente es agregarla al archivo null.

```bash
sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

Por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar Docker Engine.

<br>

### Comprobación De La Instalación

Una forma sencilla de comprobar el funcionamiento de Docker Engine es utilizando la imagen hello-world, para hacer esto se ejecuta el siguiente comando.

```bash
docker run hello-world
```

Otras alternativas más simples para comprobar el funcionamiento de la instalación es tratando de visualizar la información del Docker Engine o su versión para esto se puede ejecutar cualquiera de los siguientes comandos.

```bash
docker --version
```

```bash
docker info
```

<br>

### En Caso De Errores De Permisos

Un error comun al instalar Docker en Ubuntu es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el Docker Daemon, por lo tanto si se ejecutan comandos de Docker sin usar el super usuario aparecerá un mensaje de error de denegación de permisos, como el presente a continuación.

```bash
docker: got permission denied while trying to connect to the Docker Daemon socket atunix:///var/run/docker.sock: post http:/%2fvar%2frun%2fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.see 'docker run --help'.
```

Para solucionar este problema simplemente hay que indicar a Docker que otro usuario también va a interactuar con el Docker Daemon, para esto se emplean los siguientes comandos.

```bash
sudo addgroup --system docker
sudo adduser $user docker
newgrp docker
```

<br>

## Manejo Básico De Docker

<br>

### Abrir El Manual De Docker

```bash
man docker
```

Muestra el manual de Docker.

<br>

### Inspeccionar Un Comando De Docker

```unknown
docker <comando> --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Inspeccionar La Versión Del Docker Engine

```bash
docker --version
```

Permite ver la versión de Docker Engine instalada actualmente en el host.

<br>

### Inspeccionar Información Del Docker Daemon

```unknown
docker info <parámetros>
```

Muestra información del Docker Daemon, como el número de imágenes descargadas, el estado de Docker Swarm o incluso la versión del kernel, entre otros.

<br>

### Inspeccionar Los Recursos Usados Por Docker

```unknown
docker stats <parámetros> <id o nombre del contenedor>
```

Muestra los recursos que está utilizando cada contenedor y Docker en general, si se especifica un contenedor con su id o nombre se muestran solo los recursos que está usando ese contenedor.

<br>

### Limpiar Recursos Residuales

```unknown
docker system prune <parámetros>
```

Elimina todos los volúmenes, contenedores y redes que no se estén usando, además de también elimina las imágenes residuales.

<br>

## Administración De Contenedores

La administración de contenedores es una actividad clave al utilizar Docker ya que los contenedores son las entidades más importantes que se pueden manejar en Docker, esto se debe a que los contenedores son los encargados de virtualizar el ambiente aislado donde se ejecutarán las aplicaciones desplegadas con Docker. Es mediante el uso de contenedores que Docker adquiere tres de sus características más importantes, concretamente el uso de contenedores aporta flexibilidad, seguridad y bajo acoplamiento a las aplicaciones que usan Docker. Algunos de los comandos más importantes provistos por Docker para administrar contenedores se listan en esta sección.

<br>

### Ejecutar Contenedores

```unknown
docker run <parámetros> <imagen> <comando>
```

Ejecuta un contenedor usando la imagen especificada y ejecutando el comando indicado como proceso principal, en caso de ser dado un comando, si no es definido un comando para ejecutarse como proceso principal ni en la imagen (por defecto) ni por comando el contenedor nunca se inicia ya que un contenedor se detiene cuando su proceso principal finaliza y al no haber un proceso principal realmente el contenedor nunca arranca, algunos de los parámetros más útiles al ejecutar un contenedor con **docker run** son:

- **--name &lt;nombre del nuevo contenedor&gt;:** Permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro Docker asigna un nombre aleatorio al contenedor.
- **-i, --interactive:** Ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, al combinarlo con **--tty** se consigue una terminal interactiva entre el host y el contenedor.
- **-t, --tty:** Muestra en la salida estándar los resultados de ejecutar un comando, al combinarlo con **--interactive** se consigue una terminal interactiva entre el host y el contenedor.
- **-d, --detach:** Evita que la terminal del host quede atada a la ejecución del contenedor ejecutandolo en background e imprimiendo su id para poder manipularlo posteriormente en caso de que haga falta.
- **-p, --publish &lt;puerto del host&gt;:&lt;puerto del contenedor&gt;:** Expone el puerto designado del contenedor en el puerto designado del host.
- **--rm:** Indica a Docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **-v, --volume &lt;ruta en el host&gt;:&lt;ruta en el contenedor&gt;:** Vincula la ruta designada del contenedor con la ruta designada del host.
- **--mount src=&lt;nombre o id del volumen&gt;,dst=&lt;ruta en el contenedor&gt;:** Vincula la ruta designada del contenedor a un volumen de Docker.
- **--memory &lt;cantidad de memoria ram designada&gt; &lt;g|m&gt;:** Limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que necesite.
- **--cpus:** Permite establecer el numero de nucleos del procesador que puede usar el contenedor.
- **-e, --env &lt;nombre de la variable de entorno&gt;=&lt;valor de la variable de entorno&gt;:** Establece una o varias variables de entorno a las que tendrá acceso el contenedor.

#### Apuntes Adicionales Sobre La Ejecución De Contenedores

- Al restringir la memoria ram que puede usar un contenedor es posible que esta se finalice con el estatus oomkilled, el cual se puede ver al hacer un **docker inspect** sobre el contenedor, este estatus indica que el contenedor se detuvo debido a que la memoria con la que contaba le fue insuficiente para ejecutar todos sus procesos y por lo tanto colapsó y se detuvo.
- Los status de salida con código por encima de 128 indican salidas forzosas y normalmente indican que el cierre de ese contenedor causó que varios procesos que se estaban llevando a cabo se detuvieran sin finalizarse.
- Un código de salida 137 indica que el proceso fue cerrado por la señal sigkill.

<br>

### Renombrar Contenedores

```unknown
docker rename <nombre o id del contenedor> <nuevo nombre>
```

Renombra el contenedor indicado.

<br>

### Revisar El Estado De Los Contenedores

```unknown
docker ps <parámetros>
```

Muestra todos los contenedores activos en el host, algunos de los parámetros más útiles al ver los datos de los contenedores activos con **docker ps** son:

- **-a, --all:** Incluye los contenedores que están actualmente inactivos.
- **-l, --latest:** Muestra sólo los datos del último contenedor ejecutado.

```unknown
docker inspect <parámetros> <nombre o id del contenedor>
```

Muestra en formato json toda la información de la configuración del contenedor indicado.

<br>

### Mover Archivos Y Directorio Entre El Host Y Los Contenedores

```unknown
docker cp <parámetros> <ruta host> <nombre o id del contenedor>:<ruta contenedor>
```

Copia un archivo o directorio desde la ruta de origen del host en la ruta de destino del contenedor indicado.

```unknown
docker cp <parámetros> <nombre o id del contenedor>:<ruta contenedor> <ruta host>
```

Copia un archivo o directorio desde la ruta de origen del contenedor indicado en la ruta de destino del host.

<br>

### Inspeccionar Los Logs De Un Contenedor

```unknown
docker logs <parámetros> <nombre o id del contenedor>
```

Sirve para ver los logs del contenedor indicado, algunos de los parámetros más útiles al ver los logs de un contenedor con **docker logs** son:

- **-f, --follow:** Permite hacer follow de los logs del contenedor, es decir que se liga el Docker CLI a la salida estándar del contenedor para logs para verlos en la medida en la que se imprimen.
- **-n, --tail &lt;número de logs&gt;:** Imprime los últimos logs limitándose al número de logs indicado.

<br>

### Ejecutar Tareas En Contenedores

```unknown
docker exec <parámetros> <nombre o id del contenedor> <comando>
```

Permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando en un contenedor con **docker exec** son:

- **-d, --detach:** Evita que la terminal del host quede atada a la ejecución del comando en el contenedor ejecutandolo en background.

#### Comando Pré Construído Para Ver Procesos Dentro De Un Contenedor

```unknown
docker exec <nombre o id del contenedor> ps -ef
```

El comando anterior es una extensión de **docker exec** que muestra los procesos que se están ejecutando dentro del contenedor indicado.

#### Comando Pré Construído Para Ver Usar El Shell De Un Contenedor

```unknown
docker exec -it <nombre o id del contenedor> /bin/bash
```

El comando anterior es una extensión de **docker exec** que permite usar de forma interactiva el shell de un contenedor.

<br>

### Apagar Contenedores

```unknown
docker stop <parámetros> <nombre o id del contenedor>
```

Apaga manualmente un contenedor usando la señal sigterm, en caso de que la señal sigterm no logre apagar el contenedor se envía la señal sigkill 5 segundos después.

```unknown
docker kill <parámetros> <nombre o id del contenedor>
```

Apaga manualmente un contenedor usando la señal sigkill.

<br>

### Eliminar Contenedores

```unknown
docker rm <parámetros> <nombre o id del contenedor>
```

Sirve para borrar contenedores, Docker por defecto no elimina ningún contenedor, al finalizar el proceso principal del contenedor simplemente lo detiene, por lo que es usual tener que borrar contenedores manualmente para mantener el espacio de trabajo ordenado y evitar llenar el almacenamiento con contenedores que no es están usando, algunos de los parámetros más útiles al borrar un contenedor con **docker rm** son:

- **-f, --force:** Detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal sigkill.

```unknown
docker container prune <parámetros>
```

Borra todos los contenedores inactivos.

#### Comando Pré Construído Para Eliminar Contenedores

```bash
docker rm -f $(docker ps -aq)
```

El comando anterior es una extensión de **docker rm** pero tiene la funcionalidad de eliminar todos los contenedores activos o inactivos, para eliminar los activos fuerza su detención antes de eliminarlos con la señal sigkill.

<br>

## Administración De Imágenes

En términos de relevancia las imágenes en Docker podrían considerarse como el segundo tipo de entidad más relevantes después de los contenedores, estando casi a la par en relevancia, lo que hace a la administración de imágenes el segundo tipo de actividad más relevante al usar Docker, si bien los contenedores son la forma de virtualizar un ambiente aislado sobre el que se ejecutara la aplicación, las imágenes se encargan de indicar la forma en la que el contenedor debe construir ese ambiente, además es gracias a las imágenes que es fácil mover, desplegar y replicar un contenedor las veces que haga falta, sin alterar el funcionamiento del mismo, es por esto que las imágenes son las que aportan a las aplicaciones contenerizadas las tres características restantes principales de Docker, concretamente las imágenes aportan escalabilidad, portabilidad y ligereza a las aplicaciones contenerizadas con Docker. Algunos de los comandos más importantes provistos por Docker para administrar imágenes se listan en esta sección.

<br>

### Construir Imágenes

```unknown
docker build <parámetros> <ruta del contexto>
```

Crea y almacena una nueva imagen usando como contexto la ruta suministrada, el contexto es la ruta donde estan los archivos que se necesitan para construir la imagen, como los .dockerignore, Dockerfile y los archivos que se cargaran a la imagen, entre otros, si no se dan parámetros la imagen se crea solo con un id, sin guardar un nombre o un tag, es importante que siempre en el contexto haya un Dockerfile, ya que el Dockerfile es el que indica la forma en la que se construye una imagen, algunos de los parámetros más útiles al crear una imagen con **docker build** son:

- **-t, --tag &lt;nombre de la nueva imagen&gt;:&lt;tag de la nueva imagen&gt;:** Permite personalizar el nombre y tag de la nueva imagen que será construida.
- **-f, --file &lt;ruta del Dockerfile&gt;:** Permite cambiar o especificar la ruta del Dockerfile con el cual se construirá la imagen.

<br>

### Descargar Imágenes

```unknown
docker pull <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

Descarga la imagen con el nombre y el tag especificado, si no se especifica un tag se baja la versión más reciente (latest) o por defecto de la imagen.

<br>

### Subir Imágenes

Antes de subir una imagen a nuestro repositorio es necesario iniciar sesión con nuestro usuario en el CLI de Docker, esto se hace con el siguiente comando.

```unknown
docker login <parámetros>
```

Una vez iniciada la sesión ya podemos cargar nuestra imagen a nuestro repositorio con el siguiente comando.

```unknown
docker push <parámetros> <repositorio o nombre de usuario de Docker Hub>/<nombre o id de la imagen>:<tag de la imagen>
```

Sube la imagen con el nombre y el tag especificado al repositorio indicado.

<br>

### Cambiar El Tag De Una Imágen

```unknown
docker tag <nombre o id de la imagen de origen>:<tag de la imagen de origen> <repositorio o nombre de usuario de Docker Hub>/<nombre o id de la nueva imagen>:<tag de la nueva imagen>
```

Crea una nueva imagen con un nuevo tag que hace referencia a una ya existente y que se puede publicar en nuestro repositorio.

<br>

### Listar Imágenes

```unknown
docker image ls <parámetros>
```

Lista todas las imágenes almacenadas localmente.

<br>

### Inspeccionar Capas De Una Imágen

```unknown
docker history <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

Muestra las capas de una imagen de forma simplificada.

Otra herramienta muy útil para visualizar las capas de una imagen con más profundidad es [**dive**](https://github.com/wagoodman/dive), dive a diferencia del CLI de Docker da más información sobre las capas de cada imagen, algunos de los comandos básicos para ver información de las imágenes con dive son:

```unknown
dive <nombre o id de la imagen>:<tag de la imagen>
```

Para abrir los detalles de la imagen con dive, luego de abrir una imagen podemos usar las siguientes combinaciones de teclas para navegar por las secciones de dive:

- **tab:** Alternar entre el panel de capas y el panel de archivos.
- **flechas:** Navegar entre las capas y archivos.
- **ctrl + u:** Filtra los archivos que fueron cambiados en la capa actual.
- **ctrl + c:** Salir de dive.

<br>

### Eliminar Imágenes

```unknown
docker image rm <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

Elimina la imagen indicada.

```unknown
docker image prune <parámetros>
```

Elimina todas las imágenes residuales o inactivas.

#### Comando Pré Construído Para Eliminar Imágenes

```bash
docker image rm -f $(docker image ls -q)
```

El comando anterior es una extensión de **docker image rm** pero tiene la funcionalidad de eliminar todos las imágenes independientemente de si son residuales o no.

<br>

## Administración De Volúmenes

Los volúmenes son una parte fundamental al usar Docker para desarrollar aplicaciones contenerizadas ya que son las unidades virtuales de almacenamiento que normalmente usan los contenedores para guardar y compartir datos entre ellos de forma sencilla, usar volúmenes garantiza que los datos almacenados persistirán incluso si se detienen o eliminan todos los contenedores que hacían uso del volumen, cabe aclarar que los volúmenes son espacios de memoria del host que Docker usa para almacenar archivos de los contenedores, al igual que con los bind, pero a diferencia de los bind los volúmenes son administrados únicamente por Docker y no conceden al contenedor acceso al sistema de directorios del host, lo que los hace más seguros de usar que los bind, es por esto último que los volúmenes son la opción más recomendable para almacenar datos de los contenedores en una solución desplegada para producción. Los comandos provistos por Docker para administrar volúmenes se listan en esta sección.

<br>

### Crear Volúmenes

```unknown
docker volume create <parámetros> <nombre>
```

Crea un volúmen y le asigna el nombre indicado.

<br>

### Listar Volúmenes

```unknown
docker volume ls <parámetros>
```

Lista todos los volúmenes disponibles.

<br>

### Eliminar Volúmenes

```unknown
docker volume rm <parámetros> <nombre>
```

Elimina el volumen indicado.

```unknown
docker volume prune <parámetros>
```

Elimina todos los volúmenes residuales o inactivos almacenados localmente.

#### Comando Pré Construído Para Eliminar Volúmenes

```bash
docker volume rm -f $(docker volume ls -q)
```

El comando anterior es una extensión de **docker volume rm** pero tiene la funcionalidad de eliminar todos los volúmenes independientemente de si son residuales o no.

<br>

## Administración De Redes

Las redes son una parte fundamental al usar Docker para desarrollar una aplicación contenerizada ya que usándolas se puede lograr que varios contenedores en la misma red se comunican, y cooperan generando un esquema de micro servicios, una de las principales ventajas de usar redes de Docker es que se puede usar directamente el nombre del contenedor para establecer las comunicaciones y a diferencia de el uso de conexiones directas por api usando redes de Docker no hace falta que un contenedor salga a internet para comunicarse con otro. Los comandos provistos por Docker para administrar redes se listan en esta sección.

<br>

### Crear Redes

```unknown
docker network create <parámetros> <nombre>
```

Crea un nueva red de Docker, algunos de los parámetros más útiles al crear una red con **docker network create** son:

- **--attachable:** Habilita la opción de agregar contendores manualmente a la red.
- **-d, --driver:** Indica el driver con el que debe crearse la nueva red.

<br>

### Listar Redes

```unknown
docker network ls <parámetros>
```

Lista todas las redes disponibles.

<br>

### Inspeccionar Redes

```unknown
docker network inspect <parámetros> <nombre o id de la red>
```

Muestra la configuración de la red indicada en formato json y ciertos datos de la red, incluidos los contenedores conectados.

<br>

### Conectar Y Desconectar Redes Con Contenedores

```unknown
docker network connect <parámetros> <id o nombre de la red> <id o nombre del contenedor>
```

Conecta un contenedor a una red.

```unknown
docker network disconnect <parámetros> <id o nombre de la red> <id o nombre del contenedor>
```

Desconecta un contenedor de una red.

<br>

### Eliminar Redes

```unknown
docker network rm <parámetros> <nombre>
```

Elimina la red indicada.

```unknown
docker network prune <parámetros>
```

Elimina todas las redes residuales o inactivas.

#### Comando Pré Construído Para Eliminar Redes

```bash
docker network rm $(docker network ls -q)
```

El comando anterior es una extensión de **docker network rm** pero tiene la funcionalidad de eliminar todos las redes independientemente de si son residuales o no.

<br>

## Comandos Pre Construidos De Limpieza

Los siguientes comandos simplemente son una compilación de los comandos de las secciones anteriores, en conjunto y ejecutados en secuencia eliminan todos los contenedores, imágenes, volúmenes y redes que se hayan creado sin discriminar si son o no residuales.

```bash
docker rm -f $(docker ps -aq)
docker image rm -f $(docker image ls -q)
docker volume rm -f $(docker volume ls -q)
docker network rm $(docker network ls -q)
```

<br>

## Archivos Dockerfile

Los [**Dockerfile**](https://docs.docker.com/engine/reference/builder/) son los archivos que usa Docker al momento de construir una imagen para indicar qué archivos necesita esa imagen, qué dependencias tiene que instalar y que comandos deben ejecutarse al momento de iniciarse un contenedor a partir de esa imagen, cada instrucción que se ejecuta en un Dockerfile en tiempo de construcción es una nueva capa, algunos de los instrucciones que se pueden usar en un Dockerfile y sus funciones se listan a continuación:

- **FROM &lt;nombre de la imagen&gt;:&lt;versión de la imagen&gt;:** Indica la imagen base, o primera capa que se va a utilizar para construir la nueva imagen, siempre es el primer comando de un Dockerfile.
- **RUN &lt;comando&gt;:** Ejecuta un comando en tiempo de construcción, los comandos que se ejecutan con run solo se ejecutan al momento de construir una imagen, no al momento de iniciar un contenedor a partir de una imagen resultante de un Dockerfile que implemente esta instrucción.
- **WORKDIR &lt;ruta dentro del contenedor&gt;:** Establece un directorio de trabajo que será el directorio en el que se posicionará el contenedor al iniciar su ejecución.
- **COPY &lt;ruta archivo 0, ruta archivo 1, ... ruta archivo n, ruta destino contenedor&gt;:** Copia todos los archivos indicados en la ruta de destino de la imagen, cabe aclarar que Docker en tiempo de construcción solo da acceso a la imagen al directorio especificado como contexto, por lo que los archivos que se quieren copiar a la imagen deben estar dentro del contexto de construcción para poder ser empaquetados dentro de la misma.
- **EXPOSE &lt;número de puerto&gt;:** Expone uno o varios puertos del contenedor permitiendo que sean vinculables a uno o varios puertos del host.
- **CMD &lt;"parte 1 del comando", "parte 2 del comando"&gt;:** Exec form para ejecutar un comando, ejecutar procesos con Exec form hace que los procesos se ejecuten directamente, lo que pone el proceso indicado como proceso principal del contenedor.
- **CMD &lt;comando entero&gt;:** Bash form para ejecutar un comando, ejecutar procesos con Bash form hace que los procesos se ejecuten como procesos hijos de un bash, lo que pone al bash como proceso principal del contenedor en lugar del proceso indicado.
- **ENTRYPOINT &lt;"parte 1 del comando", "parte 2 del comando"&gt;:** Exec form para ejecutar un entrypoint, ejecuta el entrypoint como proceso principal.
- **ENTRYPOINT &lt;comando entero&gt;:** Bash form para ejecutar un entrypoint, ejecuta el entrypoint como proceso hijo del bash.
- **VOLUME &lt;rutas dentro del contenedor&gt;:** Crea un volumen y monta los archivos de las rutas indicadas en el volumen nuevo.

<br>

### Tips De Dockerfile

- Docker no construye de nuevo las capas a no ser que haya cambios, esto lo logra utilizando el caché de capas, considerar el caché de capas al momento de construir un Dockerfile puede facilitar el desarrollo, mejorando considerablemente el tiempo en el que de construye una imagen, ya que se puede ahorrar la reconstrucción de ciertas capas usando el cache.
- Utilizando monitores de scripting y bind mounts, como nodemon, se puede lograr que Docker actualice el código que se está ejecutando en tiempo de ejecución sin tener que reconstruir la imagen de nuevo.
- En Docker existe un archivo llamado [**.dockerignore**](https://docs.docker.com/engine/reference/builder/#dockerignore-file) que funciona igual que [**.gitignore**](https://git-scm.com/docs/gitignore), su función es evitar que ciertos archivos se copien en la imagen al momento de construirla.
- Los comandos ejecutados por entrypoints a diferencia de los ejecutados por cmd no pueden ser sobreescritos a no ser que se utilice un flag especial al momento de ejecutar el contenedor, por lo que si el contenedor está destinado a tener solo un uso específico es recomendable usar entrypoints en lugar de cmd para establecer el comando principal del contenedor.
- Los comandos ejecutados por entrypoints se ejecutan siempre como comandos por defecto al tener prioridad sobre los comandos ejecutados por cmd, además al combinarse entrypoints y cmd los comandos ejecutados por entrypoints utilizan los comandos de cmd como parámetros al final del comando del entrypoint, por lo que el comando del proceso principal termina siendo el comando del entrypoint concatenado con el comando de cmd, lo que hace que al no enviar comandos al momento de ejecutar el contenedor esté use lo que hay por defecto en cmd como parámetro y al enviar comandos estos se reemplazan en cmd y se usan como parámetros al final del comando del entrypoint.
- Cuando cuando se utilizan entrypoints y cmd en un mismo Dockerfile es importante que ambos utilicen o Bash form o Exec form, no es recomendable que usen formas diferentes de ejecutar el comando.
- En Docker se pueden hacer construcciones con múltiples etapas en los Dockerfile, al utilizar múltiples etapas se pueden crear imágenes previas a la imagen final de producción, la utilidad de utilizar construcciones con múltiples etapas es que se pueden generar imágenes de pruebas que contiene código adicional para las pruebas e imágenes finales, que son las imágenes resultantes de superar todas las etapas previas sin errores y contiene solo el codigo de produccion, si en algun momento de una construcción multi etapa falla la la construcción de una capa la construcción se detiene en ese punto.
- El resultado de construir una imagen con un Dockerfile multi etapa siempre es la imagen resultante de la etapa final.
- Cuando se realizan construcciones con múltiples etapas se utiliza el indicativo **as** junto a from para nombrar la imagen previa y además se puede utilizar **--from=&lt;nombre&gt;** para que una imagen posterior referencia una imagen previa.

<br>

### Ejemplo De Cache Por Capas En Dockerfile

```dockerfile
FROM node:14
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install
COPY [".", "/usr/src/"]
EXPOSE 3000
CMD ["node", "index.js"]
```

El efecto de utilizar el caché por capas en el Dockerfile anterior copiando al principio solo los archivos de dependencias, instalarlas y luego copiando de nuevo todos los archivos, es que al momento de instalar dependencias se pueda utilizar el caché siempre que no hayan habido cambios en las declaraciones de las dependencias, si se copiaran todos los archivos y luego se instalarán dependencias siempre sería necesario instalar dependencias, ya que Docker identificó cambios en la capa en la que se copian los archivos a pesar de que no sean los archivos de dependencias, por lo que no usaría cache en esa etapa y por lo tanto tampoco en la de instalación de dependencias, además del caché pr dependencias en el Dockerfile anterior se expone la aplicación mediante el puerto 3000 y se inicia un proceso usando un comando cmd en Exec form.

<br>

### Ejemplo De Un Archivo Dockerignore

```ignore
*.log
.dockerignore
.git
.gitignore
build/*
Dockerfile
node_modules
npm-debug.log*
readme.md
```

El principal efecto de el .dockerignore anterior es evitar que la imagen de la aplicación se llene de archivos innecesarios para su ejecución como los pertenecientes a git y además evita que ciertos archivos que podrían generar errores como los pertenecientes al directorio node_modules se copien en imagen.

<br>

### Ejemplo De Entrypoint Y Cmd En Dockerfile

```dockerfile
FROM ubuntu:trusty
ENTRYPOINT ["/bin/ping", "-c", "3"]
CMD ["localhost"]
```

El efecto de utilizar comandos mediante entrypoints y cmd en el Dockerfile anterior es que se puede cambiar la dirección a la que se hace ping al ejecutar un contenedor o al modificar el comando del contenedor sin poder alterar el resto del comando.

<br>

### Ejemplo De Un Dockerfile Multi Etapa

```dockerfile
# Etapa 1.
FROM node:12 as builder
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install --only=production
COPY [".", "/usr/src/"]
RUN npm install --only=development
RUN npm run test

# Etapa 2
FROM node:12
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install --only=production
COPY --from=builder ["/usr/src/index.js", "/usr/src/"]
EXPOSE 3000
CMD ["node", "index.js"]
```

El efecto de utilizar un Dockerfile multi etapa en el Dockerfile anterior es que en la primera etapa se copien los archivos y se realicen las pruebas necesarias, si se pasan las pruebas se construye una imagen final en base a los archivos de la imagen de prueba de la etapa 1.

<br>
