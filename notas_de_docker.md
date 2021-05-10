# Notas De Docker

- [Introducción](#introducción)
- [Instalación En Sistemas Mac O Windows](#instalación-en-sistemas-mac-o-windows)
- [Instalación En Sistemas Ubuntu](#instalación-en-sistemas-ubuntu)
  - [Comandos De Instalación](#comandos-de-instalación)
  - [Comprobación De La Instalación](#comprobación-de-la-instalación)
  - [En Caso De Errores](#en-caso-de-errores)
- [Manejo Básico De Docker](#manejo-básico-de-docker)
  - [Abrir El Manual De Docker](#abrir-el-manual-de-docker)
  - [Inspeccionar Un Comando De Docker](#inspeccionar-un-comando-de-docker)
  - [Inspeccionar La Versión Del Docker Engine](#inspeccionar-la-versión-del-docker-engine)
  - [Inspeccionar Información Del Docker Daemon](#inspeccionar-información-del-docker-daemon)
  - [Inspeccionar Los Recursos Usados Por Docker](#inspeccionar-los-recursos-usados-por-docker)
  - [Limpiar Recursos Residuales](#limpiar-recursos-residuales)
- [Administración De Contenedores](#administración-de-contenedores)
  - [Ejecutar Contenedores](#ejecutar-contenedores)
    - [Apuntes Adicionales Sobre La Ejecución De Contenedores](#apuntes-adicionales-sobre-la-ejecución-de-contenedores)
  - [Renombrar Contenedores](#renombrar-contenedores)
  - [Revisar El Estado De Los Contenedores](#revisar-el-estado-de-los-contenedores)
  - [Mover Archivos Y Directorio Entre El Anfitrión Y Los Contenedores](#mover-archivos-y-directorio-entre-el-anfitrión-y-los-contenedores)
  - [Inspeccionar Los Logs De Un Contenedor](#inspeccionar-los-logs-de-un-contenedor)
  - [Ejecutar Tareas En Contenedores](#ejecutar-tareas-en-contenedores)
    - [Comando Pré Construído Para Ver Procesos Dentro De Un Contenedor](#comando-pré-construído-para-ver-procesos-dentro-de-un-contenedor)
    - [Comando Pré Construído Para Ver Usar El Shell De Un Contenedor](#comando-pré-construído-para-ver-usar-el-shell-de-un-contenedor)
  - [Apagar Contenedores](#apagar-contenedores)
  - [Eliminar Contenedores](#eliminar-contenedores)
    - [Comando Pré Construído Para Eliminar Contenedores](#comando-pré-construído-para-eliminar-contenedores)
- [Administración De Imágenes](#administración-de-imágenes)
  - [Construir Imágenes](#construir-imágenes)
  - [Descargar Imágenes](#descargar-imágenes)
  - [Subir Imágenes](#subir-imágenes)
  - [Cambiar El Tag De Una Imágen](#cambiar-el-tag-de-una-imágen)
  - [Listar Imágenes](#listar-imágenes)
  - [Inspeccionar Capas De Una Imágen](#inspeccionar-capas-de-una-imágen)
  - [Eliminar Imágenes](#eliminar-imágenes)
    - [Comando Pré Construído Para Eliminar Imágenes](#comando-pré-construído-para-eliminar-imágenes)
- [Administración De Volúmenes](#administración-de-volúmenes)
  - [Crear Volúmenes](#crear-volúmenes)
  - [Listar Volúmenes](#listar-volúmenes)
  - [Eliminar Volúmenes](#eliminar-volúmenes)
    - [Comando Pré Construído Para Eliminar Volúmenes](#comando-pré-construído-para-eliminar-volúmenes)
- [Administración De Redes](#administración-de-redes)
  - [Crear Redes](#crear-redes)
  - [Listar Redes](#listar-redes)
  - [Inspeccionar Redes](#inspeccionar-redes)
  - [Conectar Y Desconectar Redes Con Contenedores](#conectar-y-desconectar-redes-con-contenedores)
  - [Eliminar Redes](#eliminar-redes)
    - [Comando Pré Construído Para Eliminar Redes](#comando-pré-construído-para-eliminar-redes)
- [Comandos Pre Construidos De Limpieza](#comandos-pre-construidos-de-limpieza)
- [Archivos Dockerfile](#archivos-dockerfile)
  - [Tips De Dockerfile](#tips-de-dockerfile)
  - [Ejemplo De Cache Por Capas En Dockerfile](#ejemplo-de-cache-por-capas-en-dockerfile)
  - [Ejemplo De Un Archivo Dockerignore](#ejemplo-de-un-archivo-dockerignore)
  - [Ejemplo De Entrypoint Y Cmd En Dockerfile](#ejemplo-de-entrypoint-y-cmd-en-dockerfile)
  - [Ejemplo De Un Dockerfile Multi Etapa](#ejemplo-de-un-dockerfile-multi-etapa)

<br>

## Introducción

[**docker**](https://docs.docker.com/get-started/overview/) es una plataforma de contenedores que permite que una aplicación este autocontenida y se ejecute sobre un contenedor, que es básicamente un sistema operativo linux superligero, los contenedores en docker se empacan y despliegan a partir de imágenes, las cuales indican al contenedor todo lo que requiere para ejecutar la aplicación y la forma en la que esta debe ser ejecutada, al desplegarse un nuevo contenedor a partir de una imagen este **aprovecha partes del sistema operativo de la máquina anfitrión** para completar las partes necesarias para ejecutarse correctamente, docker logra esto gracias a su arquitectura por capas, en un contenedor de docker cada capa corresponde con una parte necesaria para que el contenedor se ejecute como un sistema operativo aislado sobre el que se ejecutara la aplicación, en consecuencia cuando un nuevo contenedor llega a la máquina anfitrión empaquetado como imagen y se despliega, al ya estar presentes las capas más pesadas, normalmente del kernel y demas paquetes del sistema operativo, solo hace falta descargar e instalar las más livianas, que por lo general son las dependencias de la aplicación en sí, por lo que no hace falta mover las capas más pesadas dentro de la imagen, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados, como los utilizados en las máquinas virtuales.\
cabe aclarar que el aislamiento de procesos en docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo de la máquina anfitrión, no por un sistema operativo virtual que usa el hardware de la máquina anfitrión, en un sistema linux se pueden revisar todos los procesos de docker usando top o htop, en sistemas mac o windows no se pueden ver directamente los procesos de docker, ya que al instalar docker desktop, docker por debajo instala una maquina virtual con un sistema operativo linux que es el que se utiliza para completar las capas más bajas de los contenedores y por lo tanto es en el sistema operativo virtual de esa máquina virtual en el que se ejecutan los procesos de los mismos.\
al desplegar aplicaciones sobre contenedores de docker se agrega una capa adicional de abstracción (el contenedor en sí) sobre la cual trabaja la aplicación, utilizar esta capa adicional además de aportar las ventajas ya mencionadas también ayuda a simplificar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como lo son los relacionados con la construcción, distribución y ejecución de aplicaciones:

- **construcción:** al construir o desarrollar aplicaciones con docker uno de los principales beneficios es que cuando se empieza a usar docker los entornos de desarrollo y ejecución pueden ser equivalentes, ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a docker se pueden simular condiciones de ejecución con ciertos recursos como la ram limitados.
- **distribución:** al distribuir aplicaciones mediante imágenes de docker se garantiza que las dependencias de la aplicación serán instaladas y además, se garantiza que no tendrán conflicto con las del sistema operativo de la máquina anfitrión, ya que se instalan en ambientes aislados, otro beneficio de utilizar imágenes de docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se altere la aplicación esta se comportará de la misma forma siempre.
- **ejecución:** ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

otra ventaja de docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad. las aplicaciones contenerizadas con docker (que emplean docker para construir y desplegar software) tienen varias características, pero los principales son las siguientes:

- **son flexibles:** docker engine puede ejecutarse en casi cualquier parte y un contenedor solo necesita de docker engine para ejecutarse, por lo que los contenedores pueden ejecutarse casi en cualquier parte.
- **son livianas:** al utilizar la arquitectura por capas y reutilizar partes del sistema operativo de la máquina anfitrión no hace falta empacar las partes más pesadas del sistema operativo usado en las imágenes, por lo que usualmente las imágenes solo contienen las capas más ligeras de la aplicación.
- **son portables:** las imágenes creadas con docker se ejecutan de la misma forma en cualquier máquina que tenga docker engine independientemente de su software o hardware.
- **tienen un bajo acoplamiento:** cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos fuera del contenedor para funcionar.
- **son escalables:** es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **son seguras:** los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones o funciones del sistema operativo de la máquina anfitrión, a no ser que se configuren manualmente estos accesos.

docker como plataforma de contenedores se divide en tres capas, con cada una de estas capas es necesario interactuar de cierta forma para para acceder a todas las funcionalidades y poder sacarle provecho a docker, estas capas son:

- **docker server o docker daemon:** es el núcleo de docker, se encarga de manejar todas las entidades que administra docker.
- **rest api:** permite comunicar el docker daemon con el cli ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el docker daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al docker daemon mediante el uso de esta api y que es la única forma de interactuar con el docker daemon.
- **docker cli o cliente:** interfaz de línea de comandos que se utiliza de forma local para comunicarse con el docker daemon, es la forma más sencilla de usar docker.

además de las capas con las que es necesario interactuar para usar docker, docker también dispone de ciertos recursos o entidades que son los que se utilizan para desplegar, empacar y construir aplicaciones contenerizadas, los cuales son:

- **contenedores:** son la clave del funcionamiento de docker, son ambientes autocontenidos que aprovechan partes del sistema operativo de la máquina anfitrión para dar a las aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier anfitrión con docker engine instalado.
- **imágenes:** las imágenes son la forma en la cual docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga docker engine instalado.
- **redes:** las redes internas de docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **volúmenes de almacenamiento:** los volúmenes de almacenamiento son la forma que provee docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos o simplemente para poder usarlos en ejecuciones posteriores o para almacenarlos, los volúmenes de almacenamiento a pesar de ser espacios de almacenamiento en la máquina anfitrión son totalmente administrados por docker, lo que los hace inaccesibles para la máquina anfitrión.

<br>

## Instalación En Sistemas Mac O Windows

para realizar la instalación de docker en macos o en windows basta con descargar de [**docker hub**](https://hub.docker.com/) la aplicación de escritorio (docker desktop).

<br>

## Instalación En Sistemas Ubuntu

esta pequeña guía de instalación está basada en la [**guía oficial**](https://docs.docker.com/engine/install/ubuntu/) ofrecida en docker hub para instalar docker engine en **ubuntu** mediante el sistema de repositorios, cabe aclarar que en linux no hace falta instalar docker desktop como en mac o en windows, con solo docker engine es suficiente y además la manipulación del docker daemon en linux se hace solo por consola, sin interfaz gráfica, este proceso de instalación aplica para las siguientes versiones de **ubuntu**:

- ubuntu focal 20.04 (lts)
- ubuntu groovy 20.10
- ubuntu bionic 18.04 (lts)
- ubuntu xenial 16.04 (lts)

<br>

### Comandos De Instalación

```bash
sudo apt-get update

sudo apt-get remove docker docker-engine docker.io containerd runc
```

antes de iniciar con la instalación es necesario eliminar cualquier instalación previa de docker que se haya hecho en la máquina anfitrión, si no han habido instalaciones previas de docker en la máquina anfitrión se puede omitir el primer comando.

```bash
sudo apt-get update

sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
```

luego de haber desinstalado las versiones anteriores de docker se configuran los repositorios necesarios para instalar docker engine.

```bash
curl -fssl https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

tras configurar los repositorios necesarios lo siguiente es descargar la llave gpg oficial de docker.

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

una vez descargada la llave gpg lo siguiente es agregarla al archivo null.

```bash
sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar docker engine.

<br>

### Comprobación De La Instalación

una forma sencilla de comprobar el funcionamiento de docker engine es utilizando la imagen de hello-world, para hacer esto se ejecuta el siguiente comando.

```bash
docker run hello-world
```

otras alternativas más simples para comprobar el funcionamiento de la instalación es tratando de visualizar la información del docker engine o su versión para esto se puede ejecutar cualquiera de los siguientes comandos.

```bash
docker --version
```

```bash
docker info
```

<br>

### En Caso De Errores

un error comun al instalar docker en **ubuntu** es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el docker daemon, por lo tanto si se ejecutan comandos de docker sin usar el super usuario aparecerá un mensaje de error de denegación de permisos, como el presente a continuación.

```bash
docker: got permission denied while trying to connect to the docker daemon socket atunix:///var/run/docker.sock: post http:/%2fvar%2frun%2fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.see 'docker run --help'.
```

para solucionar este problema simplemente hay que indicar a docker que otro usuario también va a interactuar con el docker daemon, para esto se emplean los siguientes comandos.

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

muestra el manual de docker.

<br>

### Inspeccionar Un Comando De Docker

```unknown
docker <comando> --help
```

muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Inspeccionar La Versión Del Docker Engine

```bash
docker --version
```

permite ver la versión de docker engine instalada actualmente en la máquina anfitrión.

<br>

### Inspeccionar Información Del Docker Daemon

```unknown
docker info <parámetros>
```

muestra información del docker daemon, como el número de imágenes descargadas, el estado del modo swarm o incluso la versión del kernel, entre otros.

<br>

### Inspeccionar Los Recursos Usados Por Docker

```unknown
docker stats <parámetros> <id o nombre del contenedor>
```

muestra los recursos que está utilizando cada contenedor y docker en general, si se especifica un contenedor con su id o nombre se muestran solo los recursos que está usando ese contenedor.

<br>

### Limpiar Recursos Residuales

```unknown
docker system prune <parámetros>
```

elimina todos los volúmenes, contenedores y redes que no se estén usando, además de imágenes residuales.

<br>

## Administración De Contenedores

la administración de contenedores es una actividad clave al utilizar docker ya que los contenedores son las entidades más importantes que se pueden manejar en docker, esto se debe a que los contenedores son los encargados de virtualizar el ambiente aislado donde se ejecutarán las aplicaciones desplegadas con docker, es mediante el uso de contenedores que docker adquiere tres de sus características más importantes, concretamente el uso de contenedores aporta **flexibilidad**, **seguridad** y **bajo acoplamiento** a las aplicaciones. algunos de los comandos más importantes provistos por docker para administrar contenedores se listan en esta sección.

<br>

### Ejecutar Contenedores

```unknown
docker run <parámetros> <imagen> <comando>
```

ejecuta un contenedor usando la imagen especificada y ejecutando el comando indicado como proceso principal, en caso de ser dado un comando, si no es definido un comando para ejecutarse como proceso principal ni en la imagen (por defecto) ni por comando el contenedor nunca se inicia ya que un contenedor se detiene cuando su proceso principal finaliza y al no haber un proceso principal realmente el contenedor nunca arranca, algunos de los parámetros más útiles al ejecutar un contenedor con **docker run** son:

- **--name &lt;nombre del nuevo contenedor&gt;:** permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro docker asigna un nombre aleatorio al contenedor.
- **--interactive:** ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, al combinarlo con **--tty** se consigue una terminal interactiva entre el anfitrión y el contenedor.
- **--tty:** muestra en la salida estándar los resultados de ejecutar un comando, al combinarlo con **--interactive** se consigue una terminal interactiva entre el anfitrión y el contenedor.
- **--detach:** evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su id para poder manipularlo posteriormente en caso de que haga falta.
- **--publish &lt;puerto del anfitrión&gt;:&lt;puerto del contenedor&gt;:** expone el puerto designado del contenedor en el puerto designado de la máquina anfitrión.
- **--rm:** indica a docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **--volume &lt;ruta en el anfitrión&gt;:&lt;ruta en el contenedor&gt;:** crea un bind vinculando la ruta designada del contenedor con la ruta designada del anfitrión.
- **--mount src=&lt;nombre o id del volumen&gt;,dst=&lt;ruta en el contenedor&gt;:** vincula la ruta designada del contenedor a un volumen de docker.
- **--memory &lt;cantidad de memoria ram designada&gt; &lt;g|m&gt;:** limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que necesite.
- **--env &lt;nombre de la variable de ambiente&gt;=&lt;valor de la variable de ambiente&gt;:** establece una variable de ambiente a la que tendrá acceso el contenedor.

#### Apuntes Adicionales Sobre La Ejecución De Contenedores

- al restringir la memoria ram que puede usar una aplicación es posible que esta se finalice con el estatus **oomkilled**, el cual se puede ver al hacer un **docker inspect** sobre el contenedor, este estatus indica que el contenedor se detuvo debido a que la memoria con la que contaba le fue insuficiente para ejecutar todos sus procesos y por lo tanto colapsó y se detuvo.
- los status de salida con código por encima de 128 indican salidas forzosas y normalmente indican que el cierre de ese contenedor causó que varios procesos que se estaban llevando a cabo se detuvieran sin finalizarse.
- un código de salida 137 indica que el proceso fue cerrado por la señal **sigkill**.

<br>

### Renombrar Contenedores

```unknown
docker rename <nombre o id del contenedor> <nuevo nombre>
```

renombra el contenedor indicado.

<br>

### Revisar El Estado De Los Contenedores

```unknown
docker ps <parámetros>
```

muestra todos los contenedores activos en la máquina anfitrión, algunos de los parámetros más útiles al ver los datos de los contenedores activos con **docker ps** son:

- **--all:** incluye los contenedores que están actualmente inactivos.
- **--latest:** muestra sólo los datos del último contenedor ejecutado.

```unknown
docker inspect <parámetros> <nombre o id del contenedor>
```

muestra en formato json toda la información de la configuración del contenedor indicado.

<br>

### Mover Archivos Y Directorio Entre El Anfitrión Y Los Contenedores

```unknown
docker cp <parámetros> <ruta host> <nombre o id del contenedor>:<ruta contenedor>
```

copia un archivo o directorio desde la ruta de origen de la máquina anfitrión en la ruta de destino del contenedor indicado.

```unknown
docker cp <parámetros> <nombre o id del contenedor>:<ruta contenedor> <ruta host>
```

copia un archivo o directorio desde la ruta de origen del contenedor indicado en la ruta de destino de la máquina anfitrión.

<br>

### Inspeccionar Los Logs De Un Contenedor

```unknown
docker logs <parámetros> <nombre o id del contenedor>
```

sirve para ver los logs del contenedor indicado, algunos de los parámetros más útiles al ver los logs de un contenedor con **docker logs** son:

- **--follow:** permite hacer follow de los logs del contenedor, es decir que se liga la consola de la máquina anfitrión a la salida estándar del contenedor para logs para verlos en la medida en la que se imprimen.
- **--tail &lt;número de logs&gt;:** imprime los últimos logs limitándose al número de logs indicado.

<br>

### Ejecutar Tareas En Contenedores

```unknown
docker exec <parámetros> <nombre o id del contenedor> <comando>
```

permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando en un contenedor con **docker exec** son:

- **--detach:** evita que la terminal del anfitrión quede atada a la ejecución del comando en el contenedor, ejecutando en el background del contenedor el comando.

#### Comando Pré Construído Para Ver Procesos Dentro De Un Contenedor

```unknown
docker exec <nombre o id del contenedor> ps -ef
```

el comando anterior es una extensión de **docker exec** que muestra los procesos que se están ejecutando dentro del contenedor indicado.

#### Comando Pré Construído Para Ver Usar El Shell De Un Contenedor

```unknown
docker exec -it <nombre o id del contenedor> /bin/bash
```

el comando anterior es una extensión de **docker exec** que permite usar de forma interactiva el shell de un contenedor.

<br>

### Apagar Contenedores

```unknown
docker stop <parámetros> <nombre o id del contenedor>
```

apaga manualmente un contenedor usando la señal **sigterm**, en caso de que la señal **sigterm** no logre apagar el contenedor se envía la señal **sigkill** 5 segundos después.

```unknown
docker kill <parámetros> <nombre o id del contenedor>
```

apaga manualmente un contenedor usando la señal **sigkill**.

<br>

### Eliminar Contenedores

```unknown
docker rm <parámetros> <nombre o id del contenedor>
```

sirve para borrar contenedores, docker por defecto no elimina ningún contenedor, al finalizar el proceso principal del contenedor simplemente lo detiene, por lo que es usual tener que borrar contenedores manualmente para mantener el espacio de trabajo ordenado y evitar llenar el almacenamiento con contenedores que no es están usando, algunos de los parámetros más útiles al borrar un contenedor con **docker rm** son:

- **--force:** detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal **sigkill**.

```unknown
docker container prune <parámetros>
```

borra todos los contenedores inactivos.

#### Comando Pré Construído Para Eliminar Contenedores

```bash
docker rm -f $(docker ps -aq)
```

el comando anterior es una extensión de **docker rm** pero tiene la funcionalidad de eliminar todos los contenedores activos o inactivos, para eliminar los activos fuerza su detención antes de eliminarlos con la señal **sigkill**.

<br>

## Administración De Imágenes

en términos de relevancia las imágenes en docker podrían considerarse como el segundo tipo de entidad más relevantes después de los contenedores, estando casi a la par en relevancia, lo que hace a la administración de imágenes el segundo tipo de actividad más relevante al usar docker, si bien los contenedores son la forma de virtualizar un ambiente aislado sobre el que se ejecutara la aplicación, las imágenes se encargan de indicar la forma en la que el contenedor debe construir ese ambiente, además es gracias a las imágenes que es fácil mover, desplegar y replicar un contenedor las veces que haga falta, sin alterar el funcionamiento del mismo, es por esto que las imágenes son las que aportan a las aplicaciones contenerizadas las tres características restantes principales de docker, concretamente las imágenes aportan **escalabilidad**, **portabilidad** y **ligereza** a nuestros proyectos. algunos de los comandos más importantes provistos por docker para administrar imágenes se listan en esta sección.

<br>

### Construir Imágenes

```unknown
docker build <parámetros> <ruta del contexto>
```

crea y almacena una nueva imagen usando como contexto la ruta suministrada, el contexto es la ruta donde estan los archivos que se necesitan para construir la imagen, como los .dockerignore, **dockerfile** y los archivos que se cargaran a la imagen, entre otros, si no se dan parámetros la imagen se crea solo con un id, sin guardar un nombre o un tag, es importante que siempre en el contexto haya un **dockerfile**, ya que el **dockerfile** es el que indica la forma en la que se construye una imagen, algunos de los parámetros más útiles al crear una imagen con **docker build** son:

- **--tag &lt;nombre de la nueva imagen&gt;:&lt;tag de la nueva imagen&gt;:** permite personalizar el nombre y tag de la nueva imagen que será construida.
- **--file &lt;ruta del dockerfile&gt;:** permite cambiar o especificar la ruta al **dockerfile** con el cual se construirá la imagen.

<br>

### Descargar Imágenes

```unknown
docker pull <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

baja la imagen con el nombre y el tag especificado, si no se especifica un tag se baja la versión más reciente (latest) o por defecto de la imagen.

<br>

### Subir Imágenes

antes de subir una imagen a nuestro repositorio es necesario iniciar sesión con nuestro usuario en el cli de docker, esto se hace con el siguiente comando.

```unknown
docker login <parámetros>
```

una vez iniciada la sesión ya podemos cargar nuestra imagen a nuestro repositorio con el siguiente comando.

```unknown
docker push <parámetros> <repositorio o nombre de usuario de docker hub>/<nombre o id de la imagen>:<tag de la imagen>
```

sube la imagen con el nombre y el tag especificado al repositorio indicado.

<br>

### Cambiar El Tag De Una Imágen

```unknown
docker tag <nombre o id de la imagen de origen>:<tag de la imagen de origen> <repositorio o nombre de usuario de docker hub>/<nombre o id de la nueva imagen>:<tag de la nueva imagen>
```

crea una nueva imagen con un nuevo tag que hace referencia a una ya existente y que se puede publicar en nuestro repositorio.

<br>

### Listar Imágenes

```unknown
docker image ls <parámetros>
```

lista todas las imágenes almacenadas localmente.

<br>

### Inspeccionar Capas De Una Imágen

```unknown
docker history <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

muestra las capas de una imagen de forma simplificada.

otra herramienta muy útil para visualizar las capas de una imagen con más profundidad es [**dive**](https://github.com/wagoodman/dive), dive a diferencia del cli de docker da más información sobre las capas de cada imagen, algunos de los comandos básicos para ver información de las imágenes con dive son:

```unknown
dive <nombre o id de la imagen>:<tag de la imagen>
```

para abrir los detalles de la imagen con dive, luego de abrir una imagen podemos usar las siguientes combinaciones de teclas para navegar por las secciones de dive:

- **tab:** alternar entre el panel de capas y el panel de archivos.
- **flechas:** navegar entre las capas y archivos.
- **ctrl + u:** filtra los archivos que fueron cambiados en la capa actual.
- **ctrl + c:** salir de dive.

<br>

### Eliminar Imágenes

```unknown
docker image rm <parámetros> <nombre o id de la imagen>:<tag de la imagen>
```

elimina la imagen indicada.

```unknown
docker image prune <parámetros>
```

elimina todas las imágenes residuales o inactivas.

#### Comando Pré Construído Para Eliminar Imágenes

```bash
docker image rm -f $(docker image ls -q)
```

el comando anterior es una extensión de **docker image rm** pero tiene la funcionalidad de eliminar todos las imágenes independientemente de si son residuales o no.

<br>

## Administración De Volúmenes

los volúmenes son una parte fundamental al usar docker para desarrollar aplicaciones contenerizadas ya que son las unidades virtuales de almacenamiento que normalmente usan los contenedores para guardar y compartir datos entre ellos de forma sencilla, usar volúmenes garantiza que los datos almacenados persistirán incluso si se detienen o eliminan todos los contenedores que hacían uso del volumen, cabe aclarar que los volúmenes son espacios de memoria del anfitrión que docker usa para almacenar archivos de los contenedores, al igual que con los bind, pero a diferencia de los bind los volúmenes son administrados únicamente por docker y no conceden al contenedor acceso al sistema de directorios del anfitrión, lo que los hace más seguros de usar que los bind, es por esto último que los volúmenes son la opción más recomendable para almacenar datos de los contenedores en una solución desplegada para producción. los comandos provistos por docker para administrar volúmenes se listan en esta sección.

<br>

### Crear Volúmenes

```unknown
docker volume create <parámetros> <nombre>
```

crea un volúmen y le asigna el nombre indicado.

<br>

### Listar Volúmenes

```unknown
docker volume ls <parámetros>
```

lista todos los volúmenes disponibles.

<br>

### Eliminar Volúmenes

```unknown
docker volume rm <parámetros> <nombre>
```

elimina el volumen indicado.

```unknown
docker volume prune <parámetros>
```

elimina todos los volúmenes residuales o inactivos almacenados localmente.

#### Comando Pré Construído Para Eliminar Volúmenes

```bash
docker volume rm -f $(docker volume ls -q)
```

el comando anterior es una extensión de **docker volume rm** pero tiene la funcionalidad de eliminar todos los volúmenes independientemente de si son residuales o no.

<br>

## Administración De Redes

las redes son una parte fundamental al usar docker para desarrollar una aplicación contenerizada ya que usándolas se puede lograr que varios contenedores en la misma red se comunican, y cooperan generando un esquema de micro servicios, una de las principales ventajas de usar redes de docker es que se puede usar directamente el nombre del contenedor para establecer las comunicaciones y a diferencia de el uso de conexiones directas por api usando redes de docker no hace falta que un contenedor salga a internet para comunicarse con otro. los comandos provistos por docker para administrar redes se listan en esta sección.

<br>

### Crear Redes

```unknown
docker network create <parámetros> <nombre>
```

crea un nueva red de docker, algunos de los parámetros más útiles al crear una red con **docker network create** son:

- **--attachable:** habilita la opción de agregar contendores manualmente a la red.
- **--driver:** indica el driver con el que debe crearse la nueva red.

<br>

### Listar Redes

```unknown
docker network ls <parámetros>
```

lista todas las redes disponibles.

<br>

### Inspeccionar Redes

```unknown
docker network inspect <parámetros> <nombre o id de la red>
```

muestra la configuración de la red indicada en formato json y ciertos datos de la red, incluidos los contenedores conectados.

<br>

### Conectar Y Desconectar Redes Con Contenedores

```unknown
docker network connect <parámetros> <id o nombre de la red> <id o nombre del contenedor>
```

conecta un contenedor a una red.

```unknown
docker network disconnect <parámetros> <id o nombre de la red> <id o nombre del contenedor>
```

desconecta un contenedor de una red.

<br>

### Eliminar Redes

```unknown
docker network rm <parámetros> <nombre>
```

elimina la red indicada.

```unknown
docker network prune <parámetros>
```

elimina todas las redes residuales o inactivas.

#### Comando Pré Construído Para Eliminar Redes

```bash
docker network rm $(docker network ls -q)
```

el comando anterior es una extensión de **docker network rm** pero tiene la funcionalidad de eliminar todos las redes independientemente de si son residuales o no.

<br>

## Comandos Pre Construidos De Limpieza

los siguientes comandos simplemente son una compilación de los comandos de las secciones anteriores, en conjunto y ejecutados en secuencia eliminan todos los contenedores, imágenes, volúmenes y redes que se hayan creado sin discriminar si son o no residuales.

```bash
docker rm -f $(docker ps -aq)
docker image rm -f $(docker image ls -q)
docker volume rm -f $(docker volume ls -q)
docker network rm $(docker network ls -q)
```

<br>

## Archivos Dockerfile

los [**dockerfile**](https://docs.docker.com/engine/reference/builder/) son los archivos que usa docker al momento de construir una imagen para indicar qué archivos necesita esa imagen, qué dependencias tiene que instalar y que comandos deben ejecutarse al momento de iniciarse un contenedor a partir de esa imagen, cada instrucción que se ejecuta en un **dockerfile** en tiempo de construcción es una nueva capa, algunos de los instrucciones que se pueden usar en un **dockerfile** y sus funciones se listan a continuación:

- **from &lt;nombre de la imagen&gt;:&lt;versión de la imagen&gt;:** indica la imagen base, o primera capa que se va a utilizar para construir la nueva imagen, siempre es el primer comando de un **dockerfile**.
- **run &lt;comando&gt;:** ejecuta un comando en tiempo de construcción, los comandos que se ejecutan con run solo se ejecutan al momento de construir una imagen, no al momento de iniciar un contenedor a partir de una imagen resultante de un **dockerfile** que implemente esta instrucción.
- **workdir &lt;ruta dentro del contenedor&gt;:** establece un directorio de trabajo que será el directorio en el que se posicionará el contenedor al iniciar su ejecución.
- **copy &lt;ruta archivo 0, ruta archivo 1, ... ruta archivo n, ruta destino contenedor&gt;:** copia todos los archivos indicados en la ruta de destino de la imagen, cabe aclarar que docker en tiempo de construcción solo da acceso a la imagen al directorio especificado como contexto, por lo que los archivos que se quieren copiar a la imagen deben estar dentro del contexto de construcción para poder ser empaquetados dentro de la misma.
- **expose &lt;número de puerto&gt;:** expone un puerto del contenedor permitiendo que ese puerto sea vinculable o bindable a un puerto de la máquina anfitrión.
- **cmd &lt;"parte 1 del comando", "parte 2 del comando"&gt;:** exec form para ejecutar un comando, ejecutar procesos con exec form hace que los procesos se ejecuten directamente, lo que pone el proceso indicado como proceso principal del contenedor.
- **cmd &lt;comando entero&gt;:** bash form para ejecutar un comando, ejecutar procesos con bash form hace que los procesos se ejecuten como procesos hijos de un bash, lo que pone al bash como proceso principal del contenedor en lugar del proceso indicado.
- **entrypoint &lt;"parte 1 del comando", "parte 2 del comando"&gt;:** exec form para ejecutar un entrypoint, ejecuta el entrypoint como proceso principal.
- **entrypoint &lt;comando entero&gt;:** bash form para ejecutar un entrypoint, ejecuta el entrypoint como proceso hijo del bash.
- **volume &lt;ruta dentro del contenedor&gt;:** crea un volumen y monta los archivos de la ruta indicada en el volumen nuevo.

<br>

### Tips De Dockerfile

- docker no construye de nuevo las capas a no ser que haya cambios, esto lo logra utilizando el caché de capas, considerar el caché de capas al momento de construir un **dockerfile** puede facilitar el desarrollo, mejorando considerablemente el tiempo en el que de construye una imagen, ya que se puede ahorrar la reconstrucción de ciertas capas usando el cache.
- utilizando monitores de scripting y bind mounts, como nodemon, se puede lograr que docker actualice el código que se está ejecutando en tiempo de ejecución sin tener que reconstruir la imagen de nuevo.
- en docker existe un archivo llamado [**.dockerignore**](https://docs.docker.com/engine/reference/builder/#dockerignore-file) que funciona igual que [**.gitignore**](https://git-scm.com/docs/gitignore), su función es evitar que ciertos archivos se copien en la imagen al momento de construirla.
- los comandos ejecutados por entrypoints a diferencia de los ejecutados por cmd no pueden ser sobreescritos a no ser que se utilice un flag especial al momento de ejecutar un contenedor, por lo que si el contenedor está destinado a tener solo un uso específico es recomendable usar entrypoints en lugar de cmd para establecer el comando por defecto.
- los comandos ejecutados por entrypoints se ejecutan siempre como comandos por defecto al tener prioridad sobre los comandos ejecutados por cmd, además al combinarse entrypoints y cmd los comandos ejecutados por entrypoints utilizan los comandos de cmd como parámetros al final del comando del entrypoint, por lo que el comando del proceso principal termina siendo el comando del entrypoint concatenado con el comando de cmd, lo que hace que al no enviar comandos al momento de ejecutar el contenedor esté use lo que hay por defecto en cmd como parámetro y al enviar comandos estos se reemplazan en cmd y se usan como parámetros al final del comando del entrypoint.
- cuando cuando se utilizan entrypoints y cmd en un mismo **dockerfile** es importante que ambos utilicen o bash form o exec form, no es recomendable que usen formas diferentes de ejecutar el comando.
- en docker se pueden hacer construcciones con múltiples etapas en los **dockerfile**, al utilizar múltiples etapas se pueden crear imágenes previas a la imagen final de producción, la utilidad de utilizar construcciones con múltiples etapas es que se pueden generar imágenes de pruebas que contiene código adicional para las pruebas e imágenes finales, que son las imágenes resultantes de superar todas las etapas previas sin errores y contiene solo el codigo de produccion, si en algun momento de una construcción multi etapa falla la la construcción de una capa la construcción se detiene en ese punto.
- el resultado de construir una imagen con un **dockerfile** multi etapa siempre es la imagen resultante de la etapa final.
- cuando se realizan construcciones con múltiples etapas se utiliza el indicativo **as** junto a from para nombrar la imagen previa y además se puede utilizar **--from=&lt;nombre&gt;** para que una imagen posterior referencia una imagen previa.

### Ejemplo De Cache Por Capas En Dockerfile

```dockerfile
from node:14
copy ["package.json", "package-lock.json", "/usr/src/"]
workdir /usr/src
run npm install
copy [".", "/usr/src/"]
expose 3000
cmd ["node", "index.js"]
```

el efecto de utilizar el caché por capas en el **dockerfile** anterior copiando al principio solo los archivos de dependencias, instalarlas y luego copiando de nuevo todos los archivos, es que al momento de instalar dependencias se pueda utilizar el caché siempre que no hayan habido cambios en las declaraciones de las dependencias, si se copiaran todos los archivos y luego se instalarán dependencias siempre sería necesario instalar dependencias, ya que docker identificó cambios en la capa en la que se copian los archivos a pesar de que no sean los archivos de dependencias, por lo que no usaría cache en esa etapa y por lo tanto tampoco en la de instalación de dependencias, además del caché pr dependencias en el **dockerfile** anterior se expone la aplicación mediante el puerto 3000 y se inicia un proceso usando un comando cmd en exec form.

### Ejemplo De Un Archivo Dockerignore

```ignore
*.log
.dockerignore
.git
.gitignore
build/*
dockerfile
node_modules
npm-debug.log*
readme.md
```

el principal efecto de el .dockerignore anterior es evitar que la imagen de la aplicación se llene de archivos innecesarios para su ejecución como los pertenecientes a git y además evita que ciertos archivos que podrían generar errores como los pertenecientes al directorio node_modules se copien en imagen.

### Ejemplo De Entrypoint Y Cmd En Dockerfile

```dockerfile
from ubuntu:trusty
entrypoint ["/bin/ping", "-c", "3"]
cmd ["localhost"]
```

el efecto de utilizar comandos mediante entrypoints y cmd en el **dockerfile** anterior es que se puede cambiar la dirección a la que se hace ping al ejecutar un contenedor o al modificar el comando del contenedor sin poder alterar el resto del comando.

### Ejemplo De Un Dockerfile Multi Etapa

```dockerfile
# Etapa 1.
from node:12 as builder
copy ["package.json", "package-lock.json", "/usr/src/"]
workdir /usr/src
run npm install --only=production
copy [".", "/usr/src/"]
run npm install --only=development
run npm run test

# Etapa 2
from node:12
copy ["package.json", "package-lock.json", "/usr/src/"]
workdir /usr/src
run npm install --only=production
copy --from=builder ["/usr/src/index.js", "/usr/src/"]
expose 3000
cmd ["node", "index.js"]
```

el efecto de utilizar un **dockerfile** multi etapa en el **dockerfile** anterior es que en la primera etapa se copien los archivos y se realicen las pruebas necesarias, si se pasan las pruebas se construye una imagen final en base a los archivos de la imagen de prueba de la etapa 1.

<br>
