# Apreciaciones importantes sobre Docker

![Imagen 1. Arquitectura de capas de Docker vs arquitectura de VM.](/images/Docker_layers_arch.png)
_Imagen 1. Arquitectura de capas de Docker vs arquitectura de VM._

Docker es un sistema de contenedores que permite que cada uno de nuestros proyectos este autocontenido y empaquetado en una imagen ultra liviana de un sistema operativo Linux, el cual al desplegarse como contenedor **aprovecha partes del sistema operativo de la máquina anfitriona** como se muestra en la **Imagen 1** para completar los componentes necesarios para ejecutarse correctamente, esto lo logra gracias a su arquitectura por capas, cada capa corresponde con una parte necesaria para que nuestro proyecto se ejecute en un contenedor sobre un sistema operativo aislado, en consecuencia cuando una nueva imagen llega a la máquina anfitriona y ya están presentes las capas más pesadas, normalmente del kernel y demas paquetes del OS, solo hace falta descargar e instalar las más livianas, que normalmente son los requerimientos de nuestro proyecto, por lo que no hace falta mover las capas más pesadas, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados como los utilizados en máquinas virtuales.
Cabe aclarar que el aislamiento de procesos en Docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo de la máquina anfitriona, en un sistema Linux esto es apreciable con solo revisar los procesos en top, en Windows y en Mac no es apreciable esto, ya que al instalar Docker desktop, Docker por debajo instala una maquina virtual con un sistema operativo Linux que es el que se utiliza para suplir las capas más bajas de los contenedores y por lo tanto es en el sistema operativo de esa máquina virtual en el que se ejecutan los procesos de los contenedores.
Implementar Docker en nuestros proyectos les otorga una capa adicional de abstracción mediante la virtualización de un sistema operativo sobre el cual trabaja nuestro proyecto, implementar Docker en nuestros proyectos también ayuda a atenuar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como los relacionados con la construcción, distribución y ejecución de nuestras aplicaciones:

- **Construcción:** Al construir o desarrollar aplicaciones con Docker uno de los principales beneficios es que inmediatamente se empieza a usar Docker los entornos de desarrollo y ejecución pueden ser equivalentes ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a Docker se pueden simular condiciones de ejecución con ciertos recursos como la RAM limitados mediante contenedores.
- **Distribución:** Al distribuir aplicaciones mediante imágenes de Docker se garantiza que las dependencias de nuestra aplicación serán instaladas y además, se garantiza que no tendrán conflicto con las del sistema operativo de la máquina anfitrión, ya que están en ambientes aislados, otro beneficio de utilizar imágenes de Docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se alteren nuestra aplicación se comportará de la misma forma.
- **Ejecución:** Ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además Docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

Además de las ventajas ya expuestas otra ventaja que también tiene usar Docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad Las aplicaciones contenerizadas con Docker (que emplean Docker para construir y desplegar software) tienen varias características, pero los principales son las siguientes:

- **Flexibles:** Docker engine puede ejecutarse en casi cualquier parte.
- **Livianas:** Al utilizar la arquitectura por capas y reutilizar partes del OS del anfitrión no hace falta empacar las partes más pesadas del OS usado en las imágenes.
- **Portables:** Las imágenes creadas con Docker se ejecutan de la misma forma en cualquier máquina independientemente de su software y hardware, limitándose únicamente por el uso del hardware.
- **Bajo acoplamiento:** Cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos al contenedor para funcionar.
- **Escalables:** Es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **Seguras:** Los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones importantes del OS del anfitrión, a no ser que se configuren estas funcionalidades.

![Imagen 2. Arquitectura y recursos de Docker.](/images/Docker_engine_arch.png)
_Imagen 2. Arquitectura y recursos de Docker._

Los componentes fundamentales que son necesarios para poder interactuar y sacarle provecho a Docker son expuestos en la **Imagen 2** la cual muestra la arquitectura de Docker y los recursos que administra Docker para conseguir las funcionalidades mencionadas anteriormente, Para empezar Docker se divide en 3 capas con las que es necesario interactuar para acceder a sus funcionalidades, las cuales son:

- **Docker server o Docker daemon:** Es el núcleo de Docker, se encarga de manejar todas las entidades que administra Docker.
- **Rest API:** Permite comunicar el Docker daemon con el CLI ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el Docker daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al Docker daemon mediante el uso de esta API y que es la única forma de interactuar con el Docker daemon.
- **Docker CLI o cliente:** Interfaz de línea de comandos que se utiliza de forma local para comunicarse con el Docker daemon, es la forma más sencilla de usar Docker.

Además de las interfaces necesarias para interactuar con Docker también es importante tener claros los recursos de los que dispone Docker para desplegar aplicaciones, los cuales son:

- **Contenedores:** Son la clave del funcionamiento de Docker, son ambientes autocontenidos que aprovechan partes del sistema operativo de la máquina anfitriona para dar a nuestras aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier anfitrión con Docker engine instalado.
- **Imágenes:** Las imágenes son la forma en la cual Docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga Docker engine instalado.
- **Redes:** Las redes internas de Docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **Volúmenes de almacenamiento:** Los volúmenes de almacenamiento son la forma que provee Docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos o simplemente para poder usarlos en ejecuciones posteriores, los volúmenes de almacenamiento son totalmente administrados por Docker, lo que los hace inaccesibles para la máquina anfitriona.

# Instalación de Docker en Mac o Windows

Para realizar la instalación de Docker en MacOS o en Windows basta con descargar de [Docker Hub](https://hub.docker.com/) el aplicativo de escritorio.

# Instalación de Docker en Linux

Esta pequeña guía de instalación está basada en la [guía oficial](https://docs.docker.com/engine/install/ubuntu/) ofrecida en Docker Hub para instalar Docker engine en **Ubuntu** mediante el sistema de repositorios y es válida para las siguientes versiones de **Ubuntu**, cabe calcular que en Linux no hace falta instalar Docker desktop como en Mac o en Windows, con solo Docker engine es suficiente y además la manipulación del Docker daemon en Linux se hace solo por consola, sin interfaz gráfica.

- Ubuntu Focal 20.04 (LTS)
- Ubuntu Groovy 20.10
- Ubuntu Bionic 18.04 (LTS)
- Ubuntu Xenial 16.04 (LTS)

## Comandos de Instalación de Docker

Antes de iniciar con la instalación es necesario eliminar cualquier instalación previa de Docker que se haya hecho en la máquina anfitriona, si no han habido instalaciones previas de Docker en la máquina anfitriona se puede omitir el primer comando.

```bash
sudo apt-get remove -y docker docker-engine docker.io containerd runc
```

Luego de haber desinstalado las versiones viejas de Docker se configuran los repositorios necesarios para instalar Docker engine.

```bash
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Tras configurar los repositorios necesarios lo siguiente es agregar la llave GPG oficial de Docker.

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Una vez configurados los repositorios necesarios y la llave GPG oficial de Docker lo siguiente es configurar el repositorio estable desde el cual se instalará Docker engine.

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg]https://download.docker.com/linux/ubuntu(lsb_release -cs) stable" | sudo tee/etc/apt/sources.list.d/docker.list > /dev/null
```

Por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar Docker engine.

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

## Comprobación de la instalación

Una forma sencilla de comprobar el funcionamiento de Docker engine es utilizando la imagen de Hello-World, para hacer esto se ejecuta el siguiente comando.

```bash
docker run hello-world
```

Otras alternativas más simples para comprobar el funcionamiento de la instalación es tratando de visualizar la información del Docker engine o su versión para esto se puede ejecutar cualquiera de los siguientes comandos.

```bash
docker --version
```

```bash
docker info
```

## En caso de errores

Un error comun al instalar Docker en Ubuntu es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el Docker daemon, por lo tanto si tratamos de usar alguno de los comandos de Docker con nuestro usuario obtendremos un mensaje de error de denegación de permisos, como el presente a continuación.

```bash
docker: Got permission denied while trying to connect to the Docker daemon socket atunix:///var/run/docker.sock: Post http:/%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.See 'docker run --help'.
```

Para solucionar este problema simplemente debemos indicar a Docker que nuestro usuario también va a interactuar con el Docker daemon, esto lo podemos realizar fácilmente con los siguientes comandos.

```bash
sudo usermod -aG docker $USER
newgrp docker
```

# Comandos Básicos

```bash
man docker
```

Muestra el manual de Docker.

```bash
docker [comando] --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar el comando del que se necesita más información se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

```bash
docker --version
```

Permite ver la versión de Docker instalada actualmente en la máquina anfitriona.

```bash
docker info
```

Muestra la información del Docker Daemon, como el número de imágenes descargadas, el estado de Swarm o incluso la versión del kernel, entre otros.

```bash
docker stats
```

Muestra los recursos que está utilizando cada contenedor y docker en general.

```bash
docker system prune
```

Elimina todos los volúmenes, contenedores y redes que no se estén usando.

# Administración de contenedores

La administración de contenedores es una actividad clave al utilizar Docker ya que los contenedores son las entidades más importantes manejadas por Docker, para adminsitrara contenedores manualmente Docker nos da varios comandos que se pueden utilizar en Docker CLI para: ejecutar, eliminar y alterar el comportamiento de los contenedores, entre otras acciones posibles, algunos de los comandos más importantes provistos por Docker para administrar contenedores se listan en esta sección.

## Ejecutar un contenedor

```bash
docker run [parámetros] [imagen] [comando]
```

Ejecuta un contenedor usando la imagen especificada y ejecutando el comando especificado como proceso principal en caso de ser dado un comando luego de la imagen, es importante entender que si la imagen no tiene definido un proceso principal ni en la imagen ni por comando el contenedor se ejecutará y apagará casi al instante ya que un contenedor se detiene cuando su proceso principal finaliza y el proceso principal por defecto es solo abrir un archivo, algunos de los parámetros más útiles al ejecutar un contenedor con **docker run** son:

- **--name [nombre]:** Permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro Docker asigna también un nombre al contenedor.
- **-it:** Ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, it significa interactive terminal.
- **-d:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **-p [puerto anfitrión]:[puerto contenedor]:** Expone el puerto designado del contenedor en el puerto designado de la máquina anfitriona.
- **--rm:** Indica a Docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **-v [ruta anfitrión]:[ruta contenedor]:** Crea un bind ligando los archivos de la ruta del contenedor con los de la ruta del anfitrión.
- **--mount src=[volumen],dst=[ruta contenedor]:** Liga los archivos que están en la ruta designada del contenedor a un volumen de Docker.
- **--memory [ram designada][g:gigas o:megas]:** Limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que requiera.

## Cambiar el nombre de un contenedor

```bash
docker rename [id o nombre del contenedor] [nuevo nombre]
```

Asigna un nuevo nombre al contenedor especificado.

## Revisar el estado de un contenedor

```bash
docker ps [parámetros]
```

Muestra todos los contenedores activos en la máquina anfitriona, junto con datos como su id, nombre, nombre de imagen, estatus, puertos expuestos, tiempo de creación y comando del proceso principal, algunos de los parámetros más útiles al visualizar datos de los contenedores con **docker ps** son:

- **-a:** Muestra los mismos datos que **docker ps** pero además incluye los contenedores que están actualmente inactivos.
- **-l:** Muestra los mismos datos que **docker ps** pero muestra solo los datos del último contenedor activo.

```bash
docker inspect [id o nombre del contenedor]
```

Muestra en un archivo JSON toda la información de la configuración de un contenedor en concreto.

## Mover archivos y directorio entre el anfitrión y un contenedor

```bash
docker cp [ruta host] [id o nombre del contenedor]:[ruta contenedor]
```

Copia un archivo o directorio desde la ruta de origen de la máquina anfitrión en la ruta de destino del contenedor designado.

```bash
docker cp [id o nombre del contenedor]:[ruta contenedor] [ruta host]
```

Copia un archivo o directorio desde la ruta de origen del contenedor designado en la ruta de destino de la máquina anfitriona.

## Ver los logs de un contenedor

```bash
docker logs [parámetros] [id o nombre del contenedor]
```

Sirve para ver los logs de un contenedor especificado, algunos de los parámetros más útiles al ver los logs de un contenedor con **docker logs** son:

- **-f:** Permite hacer follow de los logs del contenedor, es decir que se liga la consola de la máquina anfitriona a los logs para verlos en la medida en la que se imprimen.
- **--tail [número de logs]:** Imprime los últimos logs limitándose al número de logs indicado.

## Ejecutar tareas en un contenedor

```bash
docker exec [parámetros] [id o nombre del contenedor] [comando]
```

Permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando un contenedor con **docker exec** son:

- **-d:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.

#### Comando pré construído:

```bash
docker exec [id o nombre del contenedor] ps -ef
```

El comando anterior es una extensión de **docker exec** que muestra los procesos que se están ejecutando dentro del contenedor indicado.

## Apagar un contenedor

```bash
docker stop [id o nombre del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigterm**, en caso de que la señal **sigterm** no logre apagar el contenedor se envía la señal **sigkill** 5 segundos después.

```bash
docker kill [id o nombre del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigkill**.

## Eliminar un contenedor

```bash
docker rm [parámetros] [id o nombre del contenedor]
```

Sirve para borrar contenedores, Docker por defecto no elimina ningún contenedor, al finalizar el proceso principal del contenedor simplemente lo detiene, por lo que es usual tener que borrar contenedores manualmente para mantener en espacio de trabajo ordenado y evitar llenar el almacenamiento con contenedores que no es están usando, algunos de los parámetros más útiles al borrar un contenedor con **docker rm** son:

- **-f:** Detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal **sigkill**.

```bash
docker container prune
```

Borra todos los contenedores inactivos.

#### Comando pré construído:

```bash
docker rm -f $(docker ps -aq)
```

El comando anterior es una extensión de **docker rm** pero tiene la funcionalidad de eliminar todos los contenedores activos o inactivos y para eliminar los activos fuerza su detención antes de eliminarlos con la señal **sigkill**.

# Administración de volúmenes

Los volúmenes son parte fundamental de Docker ya que son las unidades virtuales de almacenamiento que normalmente usan los contenedores para guardar y compartir datos de forma sencilla, si bien solo hay un par de comandos para administrar volúmenes es importante conocerlos para trabajar fácilmente con ellos, ya que usarlos nos garantiza que los datos persistirán incluso si se detiene o elimina el contenedor, cabe aclarar que los volúmenes son espacios de memoria del anfitrión que Docker usa para almacenar archivos de los contenedores, al igual que con los bind, pero a diferencia de los bind los volúmenes solo son administrados por Docker y no dan acceso al contenedor al sistema de directorio del anfitrión, lo que los hace más seguros de usar que los bind.

## Crear volúmenes

```bash
docker volume create [nombre]
```

Crea un volúmen y le asigna el nombre indicado.

## Listar volúmenes

```bash
docker volume ls
```

Lista todos los volúmenes de Docker mostrando su driver y nombre.

## Borrar volúmenes

```bash
docker volume rm [nombre]
```

Elimina el volumen indicado.

```bash
docker volume prune
```

Elimina todos los volúmenes locales inactivos.
