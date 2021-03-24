# Apuntes sobre Docker

Docker es un sistema de contenedores que permite que cada uno de nuestros proyectos este autocontenido y empaquetado en una imagen ultra liviana de un sistema operativo Linux, el cual al desplegarse como contenedor **aprovecha partes del sistema operativo de la máquina anfitrión** para completar los componentes necesarios para ejecutarse correctamente, esto lo logra gracias a su arquitectura por capas, cada capa corresponde con una parte necesaria para que nuestro proyecto se ejecute en un contenedor sobre un sistema operativo aislado, en consecuencia cuando una nueva imagen llega a la máquina anfitrión y ya están presentes las capas más pesadas, normalmente del kernel y demas paquetes del OS, solo hace falta descargar e instalar las más livianas, que por lo general son los requerimientos de nuestro proyecto, por lo que no hace falta mover las capas más pesadas, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados como los utilizados en las máquinas virtuales.\
Cabe aclarar que el aislamiento de procesos en Docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo de la máquina anfitrión, no por un sistema operativo virtual que usa el hardware de la máquina anfitrión, en un sistema Linux esto es apreciable con solo revisar los procesos con top, en Windows y en Mac no es apreciable esto, ya que al instalar Docker desktop, Docker por debajo instala una maquina virtual con un sistema operativo Linux que es el que se utiliza para suplir las capas más bajas de los contenedores y por lo tanto es en el sistema operativo de esa máquina virtual en el que se ejecutan los procesos de los contenedores.\
Implementar Docker en nuestros proyectos les otorga una capa adicional de abstracción sobre el cual trabajara nuestro proyecto y también ayuda a atenuar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como los relacionados con la construcción, distribución y ejecución de nuestros proyectos:

- **Construcción:** Al construir o desarrollar aplicaciones con Docker uno de los principales beneficios es que inmediatamente se empieza a usar Docker los entornos de desarrollo y ejecución pueden ser equivalentes ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a Docker se pueden simular condiciones de ejecución con ciertos recursos como la RAM limitados mediante contenedores.
- **Distribución:** Al distribuir aplicaciones mediante imágenes de Docker se garantiza que las dependencias de nuestra aplicación serán instaladas y además, se garantiza que no tendrán conflicto con las del sistema operativo de la máquina anfitrión, ya que están en ambientes aislados, otro beneficio de utilizar imágenes de Docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se alteren nuestra aplicación se comportará de la misma forma.
- **Ejecución:** Ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además Docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

Además de las ventajas ya expuestas otra ventaja que también tiene usar Docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad. Las aplicaciones contenerizadas con Docker (que emplean Docker para construir y desplegar software) tienen varias características, pero los principales son las siguientes:

- **Son flexibles:** Docker Engine puede ejecutarse en casi cualquier parte.
- **Son livianas:** Al utilizar la arquitectura por capas y reutilizar partes del OS del anfitrión no hace falta empacar las partes más pesadas del OS usado en las imágenes.
- **Son portables:** Las imágenes creadas con Docker se ejecutan de la misma forma en cualquier máquina independientemente de su software y hardware, limitándose únicamente por el uso del hardware.
- **Tienen un bajo acoplamiento:** Cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos al contenedor para funcionar.
- **Son escalables:** Es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **Son seguras:** Los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones importantes del OS del anfitrión, a no ser que se configuren estas funcionalidades.

Docker se divide en 3 capas con las que es necesario interactuar de cierta forma para para acceder a todas las funcionalidades de Docker y sacarles provecho, las cuales son:

- **Docker server o Docker Daemon:** Es el núcleo de Docker, se encarga de manejar todas las entidades que administra Docker.
- **Rest API:** Permite comunicar el Docker Daemon con el CLI ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el Docker Daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al Docker Daemon mediante el uso de esta API y que es la única forma de interactuar con el Docker Daemon.
- **Docker CLI o cliente:** Interfaz de línea de comandos que se utiliza de forma local para comunicarse con el Docker Daemon, es la forma más sencilla de usar Docker.

Además de las capas con las que es necesario interactuar para usar Docker también es importante tener claros los recursos de los que dispone Docker para desplegar y construir aplicaciones, los cuales son:

- **Contenedores:** Son la clave del funcionamiento de Docker, son ambientes autocontenidos que aprovechan partes del sistema operativo de la máquina anfitrión para dar a nuestras aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier anfitrión con Docker Engine instalado.
- **Imágenes:** Las imágenes son la forma en la cual Docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga Docker Engine instalado.
- **Redes:** Las redes internas de Docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **Volúmenes de almacenamiento:** Los volúmenes de almacenamiento son la forma que provee Docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos o simplemente para poder usarlos en ejecuciones posteriores, los volúmenes de almacenamiento son totalmente administrados por Docker, lo que los hace inaccesibles para la máquina anfitrión.

## Instalación de Docker en Mac o Windows

Para realizar la instalación de Docker en MacOS o en Windows basta con descargar de [Docker Hub](https://hub.docker.com/) la aplicación de escritorio.

## Instalación de Docker en Ubuntu

Esta pequeña guía de instalación está basada en la [guía oficial](https://docs.docker.com/engine/install/ubuntu/) ofrecida en Docker Hub para instalar Docker Engine en **Ubuntu** mediante el sistema de repositorios, cabe aclarar que en Linux no hace falta instalar Docker desktop como en Mac o en Windows, con solo Docker Engine es suficiente y además la manipulación del Docker Daemon en Linux se hace solo por consola, sin interfaz gráfica, este proceso de instalación aplica para las siguientes versiones de Ubuntu:

- Ubuntu Focal 20.04 (LTS)
- Ubuntu Groovy 20.10
- Ubuntu Bionic 18.04 (LTS)
- Ubuntu Xenial 16.04 (LTS)

## Comandos de instalación de Docker

```bash
sudo apt-get remove -y docker docker-engine docker.io containerd runc
```

Antes de iniciar con la instalación es necesario eliminar cualquier instalación previa de Docker que se haya hecho en la máquina anfitrión, si no han habido instalaciones previas de Docker en la máquina anfitrión se puede omitir el primer comando.

```bash
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Luego de haber desinstalado las versiones viejas de Docker se configuran los repositorios necesarios para instalar Docker Engine.

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Tras configurar los repositorios necesarios lo siguiente es agregar la llave GPG oficial de Docker.

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg]https://download.docker.com/linux/ubuntu(lsb_release -cs) stable" | sudo tee/etc/apt/sources.list.d/docker.list > /dev/null
```

Una vez configurados los repositorios necesarios y la llave GPG oficial de Docker lo siguiente es configurar el repositorio estable desde el cual se instalará Docker Engine.

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

Por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar Docker Engine.

### Comprobación de la instalación

Una forma sencilla de comprobar el funcionamiento de Docker Engine es utilizando la imagen de Hello-World, para hacer esto se ejecuta el siguiente comando.

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

### En caso de errores

Un error comun al instalar Docker en Ubuntu es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el Docker Daemon, por lo tanto si tratamos de usar alguno de los comandos de Docker con nuestro usuario obtendremos un mensaje de error de denegación de permisos, como el presente a continuación.

```bash
docker: Got permission denied while trying to connect to the Docker Daemon socket atunix:///var/run/docker.sock: Post http:/%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.See 'docker run --help'.
```

Para solucionar este problema simplemente debemos indicar a Docker que nuestro usuario también va a interactuar con el Docker Daemon, esto lo podemos realizar fácilmente con los siguientes comandos.

```bash
sudo addgroup --system docker
sudo adduser $USER docker
newgrp docker
```

## Comandos básicos de administración en Docker

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

Permite ver la versión de Docker instalada actualmente en la máquina anfitrión.

```bash
docker info [parámetros]
```

Muestra la información del Docker Daemon, como el número de imágenes descargadas, el estado de Swarm o incluso la versión del kernel, entre otros.

```bash
docker stats [parámetros] [id o nombre del contenedor]
```

Muestra los recursos que está utilizando cada contenedor y docker en general, si se especifica un contenedor con su id o nombre se muestran solo los recursos que está usando ese contenedor.

```bash
docker system prune [parámetros]
```

Elimina todos los volúmenes, contenedores y redes que no se estén usando, además de imágenes residuales.

## Administración de contenedores

La administración de contenedores es una actividad clave al utilizar Docker ya que los contenedores son las entidades más importantes que podemos manejar en Docker, esto se debe a que los contenedores son los encargados de virtualizar al ambiente aislado donde se ejecutarán nuestros proyectos, es mediante el uso de contenedores que Docker adquiere tres de sus características más importantes, concretamente el uso de contenedores aporta **flexibilidad**, **seguridad** y **bajo acoplamiento** a nuestros proyectos.

Algunos de los comandos más importantes provistos por Docker para administrar contenedores se listan en esta sección.

### Ejecutar contenedores

```bash
docker run [parámetros] [imagen] [comando]
```

Ejecuta un contenedor usando la imagen especificada y ejecutando el comando especificado como proceso principal en caso de ser dado un comando luego de la imagen, es importante entender que si no es definido definido un proceso principal ni en la imagen (por defecto) ni por comando el contenedor nunca se inicia ya que un contenedor se detiene cuando su proceso principal finaliza y al no abre proceso principal realmente el contenedor nunca arranca, algunos de los parámetros más útiles al ejecutar un contenedor con **docker run** son:

- **--name [nombre del nuevo contenedor]:** Permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro Docker asigna también un nombre al contenedor.
- **--interactive:** Ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, al combinarlo con **--tty** se consigue una terminal interactiva entre el anfitrión y el contenedor.
- **--tty:** Muestra en la salida estándar los resultados de ejecutar un comando, al combinarlo con **--interactive** se consigue una terminal interactiva entre el anfitrión y el contenedor.
- **--detach:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **--publish [puerto del anfitrión]:[puerto del contenedor]:** Expone el puerto designado del contenedor en el puerto designado de la máquina anfitrión.
- **--rm:** Indica a Docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **--volume [ruta en el anfitrión]:[ruta en el contenedor]:** Crea un bind ligando los archivos de la ruta del contenedor con los de la ruta del anfitrión.
- **--mount src=[nombre o id del volumen],dst=[ruta en el contenedor]:** Liga los archivos que están en la ruta designada del contenedor a un volumen de Docker.
- **--memory [cantidad de memoria ram designada][g|m]:** Limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que requiera.
- **--env [nombre de la variable de ambiente]=[valor de la variable de ambiente]:** Establece una variable de ambiente a la que tendrá acceso el contenedor.

#### Apuntes adicionales sobre la ejecución de contenedores

- Al restringir la memoria ram que puede usar una aplicación es posible que este finaliza con el estatus **OOMKilled**, , el cual se puede ver con un **docker inspect** del contenedor, este estatus indica que el contenedor se detuvo debido a que la memoria con la que contaba le fue insuficiente para ejecutar todos sus procesos y por lo tanto colapsó y se detuvo.
- Los status de salida con código por encima de 128 indican salidas forzosas y normalmente indican que el cierre de ese contenedor causó que varios procesos que se estaban llevando a cabo se detuvieran sin finalizarse.
- Un código de salida 137 indica que el proceso fue cerrado por la señal **sigkill**.

### Cambiar nombres de los contenedores

```bash
docker rename [nombre o id del contenedor] [nuevo nombre]
```

Asigna un nuevo nombre al contenedor especificado.

### Revisar el estado de los contenedores

```bash
docker ps [parámetros]
```

Muestra todos los contenedores activos en la máquina anfitrión, junto con datos como su id, nombre, nombre de imagen, estatus, puertos expuestos, tiempo de creación y comando del proceso principal, algunos de los parámetros más útiles al visualizar datos de los contenedores con **docker ps** son:

- **--all:** Muestra los mismos datos que **docker ps** pero además incluye los contenedores que están actualmente inactivos.
- **--latest:** Muestra los mismos datos que **docker ps** pero muestra solo los datos del último contenedor activo.

```bash
docker inspect [parámetros] [nombre o id del contenedor]
```

Muestra en un archivo JSON toda la información de la configuración de un contenedor en concreto.

### Mover archivos y directorio entre el anfitrión y los contenedores

```bash
docker cp [parámetros] [ruta host] [nombre o id del contenedor]:[ruta contenedor]
```

Copia un archivo o directorio desde la ruta de origen de la máquina anfitrión en la ruta de destino del contenedor designado.

```bash
docker cp [parámetros] [nombre o id del contenedor]:[ruta contenedor] [ruta host]
```

Copia un archivo o directorio desde la ruta de origen del contenedor designado en la ruta de destino de la máquina anfitrión.

### Visualizar los logs de los contenedores

```bash
docker logs [parámetros] [nombre o id del contenedor]
```

Sirve para ver los logs de un contenedor especificado, algunos de los parámetros más útiles al ver los logs de un contenedor con **docker logs** son:

- **--follow:** Permite hacer follow de los logs del contenedor, es decir que se liga la consola de la máquina anfitrión a los logs para verlos en la medida en la que se imprimen.
- **--tail [número de logs]:** Imprime los últimos logs limitándose al número de logs indicado.

### Ejecutar tareas en contenedores

```bash
docker exec [parámetros] [nombre o id del contenedor] [comando]
```

Permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando un contenedor con **docker exec** son:

- **--detach:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.

#### Comando pré construído para ver procesos dentro de un contenedor

```bash
docker exec [nombre o id del contenedor] ps -ef
```

El comando anterior es una extensión de **docker exec** que muestra los procesos que se están ejecutando dentro del contenedor indicado.

### Apagar contenedores

```bash
docker stop [parámetros] [nombre o id del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigterm**, en caso de que la señal **sigterm** no logre apagar el contenedor se envía la señal **sigkill** 5 segundos después.

```bash
docker kill [parámetros] [nombre o id del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigkill**.

### Eliminar contenedores

```bash
docker rm [parámetros] [nombre o id del contenedor]
```

Sirve para borrar contenedores, Docker por defecto no elimina ningún contenedor, al finalizar el proceso principal del contenedor simplemente lo detiene, por lo que es usual tener que borrar contenedores manualmente para mantener en espacio de trabajo ordenado y evitar llenar el almacenamiento con contenedores que no es están usando, algunos de los parámetros más útiles al borrar un contenedor con **docker rm** son:

- **--force:** Detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal **sigkill**.

```bash
docker container prune [parámetros]
```

Borra todos los contenedores inactivos.

#### Comando pré construído para eliminar contenedores

```bash
docker rm -f $(docker ps -aq)
```

El comando anterior es una extensión de **docker rm** pero tiene la funcionalidad de eliminar todos los contenedores activos o inactivos y para eliminar los activos fuerza su detención antes de eliminarlos con la señal **sigkill**.

## Administración de imágenes

En términos de relevancia las imágenes en Docker podrían considerarse como el segundo tipo de entidad más relevantes después de los contenedores, estando casi a la par en relevancia, lo que hace a la administración de imágenes el segundo tipo de actividad más relevante al usar Docker, si bien los contenedores son la forma de virtualizar un ambiente aislado sobre el que se ejecutara nuestro proyecto, las imágenes se encargan de indicar la forma en la que el contenedor debe construir ese ambiente, además es gracias a las imágenes que es fácil mover, desplegar y replicar un proyecto las veces que haga falta, sin alterar el funcionamiento del mismo, es por esto que las imágenes son las que aportan a nuestros proyectos las tres características restantes principales de Docker, concretamente las imágenes aportan **escalabilidad**, **portabilidad** y **ligereza** a nuestros proyectos.
Algunos de los comandos más importantes provistos por Docker para administrar imágenes se listan en esta sección.

### Construir imágenes

```bash
docker build [parámetros] [ruta del contexto]
```

Crea y almacena una nueva imagen usando como contexto la ruta suministrada, el contexto es la ruta donde estan los archivos que se necesitan para construir la imagen, como los .dockerignore, Dockerfile y los archivos que se cargaran a la imagen, entre otros, si no se dan parámetros la imagen se crea solo con un id, sin guardar un nombre o un tag, es importante que siempre en el contexto haya un Dockerfile, ya que el Dockerfile es el que indica la forma en la que se construye una imagen, algunos de los parámetros más útiles al crear una imagen con **docker build** son:

- **--tag [nombre de la nueva imagen]:[tag de la nueva imagen]:** Permite personalizar el nombre y tag de la nueva imagen que será construida.
- **--file [ruta del Dockerfile]:** Permite cambiar o especificar la ruta al Dockerfile con el cual se construirá la imagen.

### Bajar imágenes

```bash
docker pull [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Baja la imagen con el nombre y el tag especificado, si no se especifica un tag se baja la versión más reciente o por defecto de la imagen.

### Subir imágenes

Antes de subir una imagen a nuestro repositorio es necesario iniciar sesión con nuestro usuario en el CLI de Docker, esto se hace con el siguiente comando.

```bash
docker login [parámetros]
```

Una vez iniciada la sesión ya podemos cargar nuestra imagen a nuestro repositorio con el siguiente comando.

```bash
docker push [parámetros] [repositorio o nombre de usuario de Docker Hub]/[nombre o id de la imagen]:[tag de la imagen]
```

Sube la imagen con el nombre y el tag especificado al repositorio indicado.

### Cambiar tags de imágenes

```bash
docker tag [nombre o id de la imagen de origen]:[tag de la imagen de origen] [repositorio o nombre de usuario de Docker Hub]/[nombre o id de la nueva imagen]:[tag de la nueva imagen]
```

Crea una nueva imagen que se hace referencia a una ya existente y que se puede publicar en nuestro repositorio.

### Listar imágenes

```bash
docker image ls [parámetros]
```

Lista todas las imágenes almacenadas localmente.

### Visualizar capas de imágenes

```bash
docker history [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Muestra las capas de una imagen de forma simplificada.

Otra herramienta muy útil para visualizar las capas de una imagen con más profundidad es [dive](https://github.com/wagoodman/dive), dive a diferencia de los comandos nativos de Docker da más información sobre las capas de cada imagen, algunos de los comandos básicos para ver información de las imágenes con dive son:

```bash
dive [nombre o id de la imagen]:[tag de la imagen]
```

Para abrir los detalles de la imagen con dive, luego de abrir una imagen con dive podemos usar las siguientes combinaciones de teclas para navegar por las secciones de dive:

- **tab:** Alternar entre el panel de capas y el panel de archivos.
- **flechas:** Navegar entre las capas y archivos.
- **ctrl + u:** Filtra los archivos que fueron cambiados en la capa actual.
- **ctrl + c:** Salir de dive.

### Eliminar imágenes

```bash
docker image rm [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Elimina la imagen indicada.

```bash
docker image prune [parámetros]
```

Elimina todas las imágenes residuales o inactivas.

#### Comando pré construído para eliminar imágenes

```bash
docker image rm -f $(docker image ls -q)
```

El comando anterior es una extensión de **docker image rm** pero tiene la funcionalidad de eliminar todos las imágenes independientemente de si son residuales o no.

## Administración de volúmenes

Los volúmenes son una parte fundamental al usar Docker para desarrollar una solución ya que son las unidades virtuales de almacenamiento que normalmente usan los contenedores para guardar y compartir datos entre ellos de forma sencilla, usar volúmenes garantiza que los datos almacenados persistirán incluso si se detiene o elimina el contenedor que hacía uso del volumen, cabe aclarar que los volúmenes son espacios de memoria del anfitrión que Docker usa para almacenar archivos de los contenedores, al igual que con los bind, pero a diferencia de los bind los volúmenes solo son administrados únicamente por Docker y no conceden al contenedor acceso al sistema de directorios del anfitrión, lo que los hace más seguros de usar que los bind, es por esto último que los volúmenes son la opción más recomendable al utilizar un medio de almacenamiento de datos del contenedor una solución desplegada para producción.
Los comandos provistos por Docker para administrar volúmenes se listan en esta sección.

### Crear volúmenes

```bash
docker volume create [parámetros] [nombre]
```

Crea un volúmen y le asigna el nombre indicado.

### Listar volúmenes

```bash
docker volume ls [parámetros]
```

Lista todos los volúmenes de Docker mostrando su driver y nombre.

### Eliminar volúmenes

```bash
docker volume rm [parámetros] [nombre]
```

Elimina el volumen indicado.

```bash
docker volume prune [parámetros]
```

Elimina todos los volúmenes residuales o inactivos almacenados localmente.

#### Comando pré construído para eliminar volúmenes

```bash
docker volume rm -f $(docker volume ls -q)
```

El comando anterior es una extensión de **docker volume rm** pero tiene la funcionalidad de eliminar todos los volúmenes independientemente de si son residuales o no.

## Administración de redes

Las redes son una parte fundamental al usar Docker para desarrollar una solución ya que usándolas se puede lograr que varios contenedores en la misma red se comunican, y cooperan generando un esquema de micro servicios, una de las principales ventajas de usar redes de Docker es que se puede usar directamente el nombre del contenedor para establecer las comunicaciones y a diferencia de el uso de conexiones directas por API usando redes de Docker no hace falta que un contenedor salga a internet para comunicarse con otro.
Los comandos provistos por Docker para administrar redes se listan en esta sección.

### Crear redes

```bash
docker network create [parámetros] [nombre]
```

Crea un nueva red de Docker, algunos de los parámetros más útiles al crear una red con **docker network create** son:

- **--attachable:** Habilita la opción de agregar contendores manualmente a la red.
- **--driver:** Indica el driver con el que debe crearse la nueva red.

### Listar redes

```bash
docker network ls [parámetros]
```

Lista todas las redes de Docker, mostrando su nombre, tipo de driver, id y alcance:

### Inspeccionar redes

```bash
docker network inspect [parámetros] [nombre o id de la red]
```

Muestra todas las configuración de una red en formato JSON, incluidos los contenedores conectados a ella.

### Conectar y desconectar redes con contenedores

```bash
docker network connect [parámetros] [id o nombre de la red] [id o nombre del contenedor]
```

Conecta un contenedor a una red.

```bash
docker network disconnect [parámetros] [id o nombre de la red] [id o nombre del contenedor]
```

Desconecta un contenedor de una red.

### Eliminar redes

```bash
docker network rm [parámetros] [nombre]
```

Elimina la red indicada.

```bash
docker network prune [parámetros]
```

Elimina todas las redes residuales o inactivas.

#### Comando pré construído para eliminar redes

```bash
docker network rm $(docker network ls -q)
```

El comando anterior es una extensión de **docker network rm** pero tiene la funcionalidad de eliminar todos las redes independientemente de si son residuales o no.

## Comandos pre construidos de limpieza

Los siguientes comandos simplemente son una compilación de los comandos de las secciones anteriores, en conjunto y ejecutados en secuencia eliminan todos los contenedores, imágenes, volúmenes y redes que se hayan creado.

```bash
docker rm -f $(docker ps -aq)
docker image rm -f $(docker image ls -q)
docker volume rm -f $(docker volume ls -q)
docker network rm $(docker network ls -q)
```

## Archivos Dockerfile

Los [**Dockerfile**](https://docs.docker.com/engine/reference/builder/) son los archivos que usa Docker al momento de construir una imagen para indicar qué archivos necesita esa imagen, qué dependencias tiene que instalar y que comandos deben ejecutarse al momento de iniciarse como un contenedor a partir de esa imagen, cada instrucción que se ejecuta en un Dockerfile en tiempo de construcción es una nueva capa, algunos de los instrucciones que se pueden usar en un Dockerfile y sus funciones se listan a continuación:

- **FROM [nombre de la imagen]:[versión de la imagen]:** Indica la imagen base, o primera capa que se va a utilizar para construir la nueva imagen, siempre es el primer comando de un Dockerfile.
- **RUN [comando]:** Ejecuta un comando en tiempo de construcción, los comandos que se ejecutan con **RUN** solo se ejecutan al momento de construir una imagen, no al momento de iniciar un contenedor a partir de una imagen resultante de un Dockerfile que implemente esta instrucción.
- **WORKDIR [ruta dentro del contenedor]:** Establece un directorio de trabajo que será el directorio en el que se posicionará el contenedor al iniciar su ejecución.
- **COPY [ruta archivo 0, ruta archivo 1, ... ruta archivo n, ruta destino contenedor]:** Copia todos los archivos indicados en la ruta de destino de la imagen, cabe aclarar que Docker solo da acceso a la imagen en tiempo de construcción al directorio especificado como contexto, por lo que los archivos que se quieren copiar a la imagen deben estar dentro del contexto de construcción para poder ser empaquetados dentro de la misma.
- **EXPOSE [número de puerto]:** Expone un puerto del contenedor permitiendo que ese puerto sea vinculable o bindable a un puerto de la máquina anfitrión.
- **CMD ["parte 1 del comando", "parte 2 del comando"]:** Exec form para ejecutar un comando, ejecutar procesos con exec form hace que los procesos se ejecuten directamente, lo que pone el proceso indicado como proceso principal del contenedor.
- **CMD [comando entero]:** Bash form para ejecutar un comando, ejecutar procesos con bash form hace que los procesos se ejecuten como procesos hijos de un bash, lo que pone al bash como proceso principal del contenedor en lugar del proceso indicado.
- **ENTRYPOINT ["parte 1 del comando", "parte 2 del comando"]:** Exec form para ejecutar un entrypoint, ejecuta el entrypoint como proceso principal.
- **ENTRYPOINT [comando entero]:** Bash form para ejecutar un entrypoint, ejecuta el entrypoint como proceso hijo del bash.
- **VOLUME [ruta dentro del contenedor]:** Crea un volumen y monta los archivos de la ruta indicada en el volumen nuevo.

### Tips de Dockerfile

- Docker no construye de nuevo las capas a no ser que haya cambios, esto lo logra utilizando el caché de capas, es importante construir los Dockerfile considerando el caché de capas para facilitar el proceso de desarrollo.
- Utilizando monitores de scripting y bind mounts, como nodemon, se puede lograr que Docker actualice el código que se está ejecutando en tiempo de ejecución sin tener que reconstruir la imagen de nuevo.
- En Docker existe un archivo llamado [**.dockerignore**](https://docs.docker.com/engine/reference/builder/) que funciona igual que **.gitignore**, su función es evitar que cierto tipo de archivos copien la imagen al construirla.
- Los **entrypoint** a diferencia de **cmd** no pueden ser sobreescritos a no ser que se utilice un flag especial al momento de ejecutar un contenedor, por lo que si el contenedor está destinado a tener solo un uso específico es recomendable usar **entrypoints** en lugar de **cmd** para establecer el comando por defecto.
- Los **entrypoint** se ejecutan siempre como comandos por defecto al tener prioridad sobre los comandos de **cmd**, además al combinarse **entrypoints** y **cmd** los **entrypoint** utilizan los comandos de **cmd** como parámetros al final del comando del **entrypoint**, por lo que el comando del proceso principal termina siendo el comando del **entrypoint** concatenado con el comando de **cmd**, lo que hace que al no enviar comandos al momento de ejecutar el contenedor esté use lo que hay por defecto en **cmd** como parámetro y al enviar comandos estos se reemplazan en **cmd** y se usan como parámetros al final del comando del **entrypoint**.
- Cuando cuando se utilizan **entrypoints** y **cmd** en un mismo Dockerfile es importante que ambos utilicen o bash form o exec form, no es recomendable que usen formas diferentes de ejecutar el comando.
- En Docker se pueden hacer construcciones con múltiples etapas en los Dockerfile, al utilizar múltiples etapas se pueden crear imágenes previas a la imagen final de producción, la utilidad de utilizar construcciones con múltiples etapas es que se pueden generar imágenes de pruebas que contiene código adicional para las pruebas e imágenes finales, que son las imágenes resultantes de superar todas las etapas previas sin errores y contiene solo el codigo de produccion, si en algun momento de una construcción multi etapa falla la la construcción de una capa la construcción se detiene en ese punto.
- El resultado de construir una imagen con un Dockerfile multi etapa siempre es la imagen resultante de la etapa final.
- Cuando se realizan construcciones con múltiples etapas se utiliza el indicativo **as** junto a **FROM** para nombrar la imagen previa y además se puede utilizar **--from=nombre** para que una imagen posterior referencia una imagen previa.

#### Ejemplo de cache por capas en Dockerfile

```dockerfile
FROM node:14
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install
COPY [".", "/usr/src/"]
EXPOSE 3000
CMD ["node", "index.js"]
```

#### Ejemplo de .dockerignore

```ignore
*.log
.dockerignore
.git
.gitignore
build/*
Dockerfile
node_modules
npm-debug.log*
README.md
```

#### Ejemplo de entrypoint y cmd en Dockerfile

```dockerfile
FROM ubuntu:trusty
ENTRYPOINT ["/bin/ping", "-c", "3"]
CMD ["localhost"]
```

#### Ejemplo de un Dockerfile multi etapa

```dockerfile
# etapa 1.
FROM node:12 as builder
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install --only=production
COPY [".", "/usr/src/"]
RUN npm install --only=development
RUN npm run test

# etapa 2
FROM node:12
COPY ["package.json", "package-lock.json", "/usr/src/"]
WORKDIR /usr/src
RUN npm install --only=production
COPY --from=builder ["/usr/src/index.js", "/usr/src/"]
EXPOSE 3000
CMD ["node", "index.js"]
```

## Instalación de Docker Compose en Ubuntu

Docker Compose se instala junto a las versiones de escritorio de Windows o Mac, sin embargo en la versión de Ubuntu es necesario instalarlo manualmente con los siguientes comandos, los cuales son extraídos de la guia oficial de [Docker Hub](https://docs.docker.com/compose/install/):

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Archivos docker-compose.yml

Docker Compose permite usar los 4 recursos de Docker juntos fácilmente desde un solo archivo [**docker-compose.yml**](https://docs.docker.com/compose/compose-file/), usando este archivo también llamado **compose file** se pueden integrar fácilmente recursos de red, volúmenes, imagenes y contenedores sin necesidad de administrar uno a uno cada tipo de recurso, en síntesis lo que permite Docker Compose es describir de forma declarativa la arquitectura de servicios que la aplicación necesita, y Docker se encargará de crear e integrar cada recursos declarado por detrás evitandonos tener que administraba uno a uno los recursos, algunos de los componentes que soporta **Docker Compose** y sus funciones son:

- **version:** Indica la versión del compose file, dependiendo de la versión de Docker Engine se soportan ciertas características y ciertas versiones de compose-file.
- **services:** Indica que servicios componen la aplicación, básicamente son las partes o componentes que interactúan para formar nuestra aplicación y que funcione correctamente, un servicio no es un container explícitamente ya que un servicio puede componerse de uno o muchos contenedores.
- **image:** Establece la imagen que se va a utilizar para ejecutar los contenedores de cierto servicio.
- **environment:** Permite definir variables de ambiente a las que pueden acceder los contenedores de un servicio.
- **depends_on:** Establece las dependencias entre servicios, si un servicio declara dependencia de otro este no deberá ejecutarse si antes no se ejecuta el o los servicios de los que depende.
- **ports:** Bindea un puerto o un rango de puertos de la máquina anfitrión con un puerto de uno o varios contenedores.
- **volumes:** Indica los volúmenes y bind mounts de un servicio.
- **command:** Cambia el comando por defecto del servicio.
- **build:** Indica el contexto con el que se debe construir una nueva imagen que se desplegará en todos los contenedores del servicio indicado, el nombre de la nueva imagen se construye en base al nombre del directorio de trabajo y el nombre del servicio en el siguiente formato **[nombre del directorio de trabajo]\_[nombre del servicio]**.
- **networks:** Indica las redes a las que se deben conectar los contenedores de un servicio.

### Tips de Docker Compose

- Al usar Docker Compose Docker por detrás crea una red dedicada a esa arquitectura a la que conecta todos los contenedores de todos los servicios declarados, el nombre de la red se asigna en base al nombre del directorio de trabajo en el siguiente formato **[nombre del directorio de trabajo]\_default**.
- Al usar Docker Compose Docker por detras trata de asignar nombres únicos a cada contenedor para evitar conflictos a causa de los nombres, los nombres de los contenedores se asigna en base del nombre del directorio de trabajo, el nombre del servicio y un número que diferencia los diferentes contenedores de un servicio en el siguiente formato **[nombre del directorio de trabajo]\_[nombre del servicio]\_[número de contenedor]**.
- Al usar Docker Compose Docker por detrás se asegura que a pesar de los nuevos nombres asignados a los contenedores estos sigan siendo alcanzables por los demás contenedores solo con el nombre del servicio que ejecutan.
- Junto a **docker-compose.yml** se puede utilizar **docker-compose.override.yml**, la ventaja de utilizar Docker Compose.override es que se puede personalizar el compose-file sin cambiarlo directamente, lo que evita alterar el compose-file de producción pero nos permite probar pequeños cambios en el sin alterarlo directamente, además Docker por defecto tratar de unir y conservar las definiciones de ambos archivos.
- Las variables de entorno son sencillas de manejar con los archivos **compose** y **compose.override** ya que simplemente se unen las definiciones de ambas y en caso de redefinición en **compose.override** simplemente se sobreescribe el valor de la variable.
- Para el manejo de los puertos lo recomendable es no utilizar definiciones de puertos fuera de **compose** y en caso de hacerse la definición de los puertos debe estar solo en un archivo.
- Las dependencias de servicios se usan siempre desde el **compose.override**.
- Para usar un **compose.override** solo hace falta construir la imagen de forma normal, Docker por defecto detecta el archivo de sobre escritura y lo utiliza.
- Al poner **image** y **build** en un mismo compose la imagen se construye pero se le asigna el nombre de imagen en lugar del nombre por defecto.

#### Ejemplo de un Docker Compose con dos servicios y volúmenes

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes:
      - disc:/home/node/app
    command: nodemon index.js

  db:
    image: mongo
```

El compose anterior utiliza un volumen en app, además de una variable de ambiente, un puerto vinculado, un cambio en el comando por defecto y construye una imagen para los contenedores del servicio app.

#### Ejemplo de un Docker Compose con dos servicios y bind mount

```yml
version: "3.8"

services:
  app:
    image: alpine
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000-3001:3000"
    volumes:
      - .:/home/node/app
      - /home/node/app/node_modules

  db:
    image: mongo
```

El compose anterior utiliza un bind mount, indica una ruta que no debe ser alterada por el bind, además, utiliza una variable de ambiente y un rango de puertos del anfitrión que pueden ser vinculados a los contenedores del servicio app.

#### Ejemplo de un docker-compose.override

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      NUEVA_VARIABLE: "mongodb://db:27017/test"
```

Al declarar un **docker-compose.override.yml** como el anterior junto a cualquiera de los **docker-compose.yml** se logra que se construya la imagen y se agregue la variable de ambiente nueva a la imagen.

## Subcomandos de Docker Compose

Docker Compose tiene varios subcomandos similares a los usados en la administración regular de Docker, algunos de los más relevantes para utilizar aplicaciones basadas en Docker Compose son:

### Comandos de administración general de una aplicación compose

```bash
docker-compose [comando] --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Construir las imágenes necesarias para una aplicación compose

```bash
docker-compose build [parámetros] [nombre del servicio]
```

Construye las imágenes que requieren ser construidas según el **compose file**, al especificarse uno o varios servicios solo se construirán las imágenes de los servicios indicados.

### Iniciar una aplicación compose

```bash
docker-compose up [parámetros] [nombre del servicio]
```

Levanta la arquitectura descrita por el **compose file** en caso de no indicarse un servicio en concreto, si se indica un servicio solo ese servicio será ejecutado, algunos de los parámetros más útiles al utilizar **docker-compose up** para levantar una arquitectura son:

- **--detach:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **--scale [nombre o id del servicio]=[número de contenedores]:** Escala un determinado servicio al número de contenedores indicado.

### Revisar el estado de los contenedores generados por una aplicación compose

```bash
docker-compose ps [parámetros] [nombre del servicio]
```

Muestra el estado de los contenedores creados por el **compose file** en caso de no indicarse un servicio en concreto, si se indica un servicio solo se mostrará el estado de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose ps** para ver el estado de los contenedores pertenecientes a una arquitectura son:

- **--all:** Muestra todos los contenedores de la aplicación independientemente de si están o no ejecutados.

### Revisar los logs de una aplicación compose

```bash
docker-compose logs [parámetros] [nombre del servicio]
```

Muestra los logs de todos los contenedores usados por la aplicación en caso de no indicarse un servicio en concreto, si se indica un servicio sólo se mostrarán solo los logs de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose logs** para ver los logs de una arquitectura son:

- **--follow:** Sirve para hacer follow a los logs de toda la aplicación o de cierto servicio si se indica el servicio.
- **--tail [número de logs]:** Imprime los últimos logs limitándose al número de logs indicado de toda la aplicación o de cierto servicio si se indica el servicio.

### Ejecutar comandos en servicios de una aplicación compose

```bash
docker-compose exec [parámetros] [nombre del servicio] [comando]
```

Ejecuta un comando dentro del o los contenedores pertenecientes a un servicio de una aplicación compose.

### Detener y eliminar todos los servicios de una aplicación compose

```bash
docker-compose down [parámetros]
```

Detiene y elimina todos los recursos usados por una aplicación compose.

## Docker Swarm

Docker Swarm es la solución nativa que ofrece Docker para montar aplicaciones basadas en cómputo distribuido y en contenedores, lo que propone Docker Swarm es que al montar un cluster en el que se quieren desplegar aplicaciones contenerizadas bajo el esquema de servicios el cluster debe ser fácilmente administrable, bajo esta premisa Docker Swarm ha llegado hasta el punto en el que el desarrollador puede tratar la totalidad del cluster como si se tratase de un solo entorno de Docker que atraviesan muchas máquinas, gracias a esto es que usando Docker Swarm es posible administrar un cluster casi con la facilidad con la que se administra una sola máquina con un solo Docker Daemon, cuando en realidad son varias máquinas cada uno con su propio Docker Daemon. Para conseguir este funcionamiento Docker Swarm se basa en tres conceptos fundamentales, estos tres conceptos son **Swarm**, **Nodos** y **Servicios**, cada uno de estos conceptos corresponde a un tipo de entidad que compone una aplicación basada en Docker Swarm, las definiciones resumidas de cada uno de estos conceptos se listan a continuación:

- **Swarm:** Swarm, cluster o enjambre son referencias del mismo concepto, una agrupación de varias máquinas que cooperan para realizar la misma tarea, en el caso de Docker Swarm, desplegar contenedores de una aplicación para aumentar su disponibilidad y escalabilidad.
- **Nodos:** Los nodos son todas las máquinas que componen el Swarm, cluster o enjambre, entre los nodos se reparten las tareas que deben ser ejecutadas, en el caso de Docker Swarm, los contenedores que deben ser ejecutados y la gestión de recursos necesaria para mantener el correcto funcionamiento del cluster.
- **Servicios:** Los servicios son uno o varios contendores que ejecutan la misma aplicación en diferentes nodos en un mismo cluster, con el objetivo de que ese servicio tenga una muy alta disponibilidad y además sea altamente escalable.

Es gracias a la división de las labores de administración de la aplicación en estas tres entidades que las aplicaciones desplegadas con Docker Swarm son muy fáciles de administrar, ya que se pueden administrar como entidades separadas a pesar de que forman parte de una misma aplicación, siempre tomando en cuenta la forma en la cual alterar una entidad afectará el comportamiento de la aplicación y de las demás entidades.\
Al utilizar Docker Swarm las máquinas que componen el cluster o nodos se divide en dos tipos, **Managers** y **Workers**, siendo los Managers los encargados de gestionar los recursos el cluster, mientras que los Workers se encargaran de ejecutar las tareas que les son asignadas por los Managers, las funciones específicas de los dos tipos de nodo se lista a continuación:

- **Managers:** Gestiona las comunicaciones, distribuyen las tareas, gestionan los recursos y se encargan de re posicionar contenedores y tareas en caso de caídas de algún nodo del cluster.
- **Workers:** Ejecutan los contenedores de la aplicación.

Por lo general en una aplicación basado en Docker Swarm hay más nodos Worker que Manager, ya que los Worker son el núcleo de la aplicación al ser los que ejecutan la aplicacion como tal, mientras que los Manager están dedicados exclusivamente a gestionar el cluster, si bien los manager también pueden ejecutar contendores de la aplicación no es recomendable, ya que esto generaría una competencia de recursos entre las tareas de gestión del cluster y de ejecución de contenedores de la aplicación, lo que podría generar errores en la gestión del cluster y en consecuencia en la totalidad de la aplicación.\
Las únicas restricciones al momento de crear una aplicación usando Docker Swarm es que todos los nodos deben estar en la misma red o subred y deben ser visibles entre ellos, además todos tiene que tener instalado el Docker Daemon, idealmente de la misma versión.\
Antes de desplegar una aplicación basada en Docker Swarm lo adecuado es revisar que la aplicación cumpla ciertos factores para poder sacarle todo el provecho al cluster, si bien hay muchos factores a considerar, hay consenso en [12 factores clave](https://12factor.net/) que deben ser tomados en cuenta antes de decidir si una aplicación está lista o no para ser desplegada con Docker Swarm, muy resumidamente los 12 factores son:

1. El código fuente de la aplicación debe estar en un repositorio versionado y además debe haber una paridad de 1 a 1 entre el repositorio y la aplicación, por lo que no puede haber código de varias aplicaciones diferentes en el repositorio.

1. Las dependencias deben estar declaradas explícitamente en un archivo de dependencias, el cual debe estar empaquetado junto al código fuente de la aplicación, siempre debe asumirse que las dependencias no están instaladas por lo que es necesario instalarlas con su archivo de dependencias correspondiente.

1. Las definiciones de configuración de la aplicación deben estar empaquetadas junto a la aplicación y la aplicación debe estar diseñada para que bajo ninguna circunstancia la configuración cambie en función del servidor.

1. Los servicios de apoyo con los que interactúa la aplicación se tratan como aplicaciones externas a las que la aplicación se conecta, no como componentes o complementos de la aplicación como tal.

1. Se deben separar estrictamente las etapas de construcción, liberación y ejecución, no debe haber procesos en etapas que no les corresponden, por ejemplo, un proceso de construcción jamás debe ocurrir en una etapa de ejecución, máximo en una etapa de ejecución se pueden hacer configuraciones.

1. La aplicación tiene que poder ejecutarse como un proceso stateless, es decir que no debe depender de ciertos estados de memoria o archivos que ya están en la máquina y en caso de necesitar archivos deben ser capaces de generarlos.

1. Las aplicaciones deben exponerse a sí mismas mediante puertos vinculados entre el host y la aplicación, siempre evitando utilizar intermediarios.

1. La aplicación debe poder ejecutarse con múltiples instancias en paralelo.

1. La aplicación debe poder apagarse, destruirse y levantarse muy rápidamente.

1. El entorno de desarrollo y el entorno de producción deben ser lo más parecidos posibles.

1. Todos los logs de la aplicación deben emitirse por la salida estándar, de tal modo que si se necesitan simplemente se puedan inspeccionar y recolectar.

1. Todas las labores de administración deben poder realizarse sin alterar la ejecución de la aplicación, es decir que no debe ser necesario reiniciar la aplicación en cierto modo o con cierto estado para poder administrar.

Docker Swarm además viene instalado con Docker Engine, por lo que no hace falta instalarlo una vez ya está instalado Docker Engine.

## Administración de un cluster

El cluster, enjambre o Swarm es lo que permite que una aplicación basada en Docker Swarm escale sobre un hardware virtualmente infinito, es por esto que si bien el cluster no es muy difícil de administrar y no hay muchos comandos con los cuales administrarlo, es importante tener en cuenta los comandos necesarios para administrar y escalar el cluster, ya que del cluster depende que tanto puede escalar la aplicación a nivel de Hardware.

### Comandos básicos de administración de un cluster

```bash
docker swarm [comando] --help
```

Muestra a grandes rasgos los comandos disponibles para administrar el cluster y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Iniciar un cluster

```bash
docker swarm init [parámetros]
```

Inicia un cluster utilizando la máquina actual como el primer manager del cluster, algunos de los parámetros más útiles al utilizar **docker swarm init** para iniciar un cluster son:

- **--advertise-addr [ip]:** Al iniciar un cluster en una máquina con múltiples interfaces de red se utiliza para indicar al manager cuál de estas debe utilizar para las comunicaciones del cluster.

### Conectar máquinas al cluster

```bash
docker swarm join-token [parametros] [worker|manager]
```

Genera un token que es utilizado para agregar una nueva máquina al cluster, hay dos tipos de tokens, uno para agregar managers y otro para agregar workers, al utilizar este comando además de imprimir el token se imprime el comando que permitirá utilizarlo para unir una máquina nueva al cluster.

### Desconectar máquinas del cluster

```bash
docker swarm leave [parametros]
```

Permite a la máquina actual abandonar el cluster, para dejar el cluster con **docker swarm leave** solo puede utilizarse un parámetro adicional, éste es:

- **--force:** Permite forzar a la máquina actual a abandonar el cluster, cuando se requiere que un manager abandone el cluster suele ser necesario utilizar este parámetro, ya que Docker Swarm no permite que los manager abandonen el cluster fácilmente por seguridad.

## Administración de nodos pertenecientes a un cluster

Los nodos son las maquinas que estan conectadas al cluster, no hay muchas opciones para administrar nodos, pero varios de estos comandos son muy útiles y es bueno tomarlos en cuenta, además, la administración de nodos sólo puede hacerse desde un manager, ya que los workers no suelen tener acceso a estas acciones.

### Comandos básicos de administración de nodos

```bash
docker node [comando] --help
```

Muestra a grandes rasgos los comandos disponibles para administrar los nodos de un cluster y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Listar los nodos conectados al cluster

```bash
docker node ls [parámetros]
```

Lista los nodos pertenecientes a un cluster, mostrando su id, nombre, estatus, disponibilidad, su versión de Docker Engine y si es manager o worker, además, se indica con \* el nodo en el que se está actualmente.

### Inspeccionar un nodo

```bash
docker node inspect [parámetros] [id o nombre del nodo]
```

Muestra en detalle la configuración de un nodo en un archivo JSON, algunos de los parámetros más útiles al inspeccionar un nodo con **docker node inspect** son:

- **--pretty:** Cambia el formato JSON con el que se muestran los datos por un formato clásico de consola que es más fácil de leer, pero omite ciertas partes de la configuración al cambiar el formato del texto.

### Actualizar las configuraciones de un nodo

```bash
docker node update [parámetros] [id o nombre del nodo]
```

Permite actualizar ciertas configuraciones de un nodo, algunos de los parámetros más útiles al actualizar la configuración de un nodo con **docker node update** son:

- **--availability [active|pause|drain]:** Permite cambiar la disponibilidad de un nodo, en estado activo se le pueden asignar tareas al nodo sin problema, en estado pausado el nodo no recibe tareas y en estado de drenado se sacan del nodo todas las tareas y se envían a otros nodos antes de ser puesto el nodo en estado pausado.

## Administración de servicios basados en Docker Swarm

Los servicios son la base de Docker Swarm, al igual que en Docker Compose un servicio es una aplicación contenerizada que está desplegada en uno o más contenedores, en Docker Swarm la ventaja es que estos contenedores pueden estar ejecutándose en cualquier nodo del cluster y además pueden moverse entre nodos fácilmente, es debido a esto que los servicios son altamente disponibles y escalables, al trabajar con servicios se trabaja implícitamente con contenedores ya que Docker Swarm se encarga de gestionar los contenedores en función de la declaración del servicio.

### Comandos básicos de administración de servicios

```bash
docker service [comando] --help
```

Muestra a grandes rasgos los comandos disponibles para administrar servicios y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Iniciar un servicio

```bash
docker service create [parámetros] [nombre o id de la imagen] [comando]
```

Permite iniciar un servicio basado en Docker Swarm especificando la imagen y el comando del proceso principal, si no se especifica el comando del proceso principal se usa el proceso principal por defecto, algunos de los parámetros más útiles al iniciar un servicio con **docker service create** son:

- **--name [nombre del servicio]:** Establece el nombre indicado como nombre del servicio.
- **--publish [puerto del anfitrión]:[puerto del contenedor]:** Utiliza la red ingress y el routing mesh de Docker Swarm para exponer la aplicación.
- **--replicas [número de réplicas]:** Establece el número de réplicas o contenedores que deben ejecutarse de cierto servicio.
- **--constraint node.role==[worker|manager]:** Limita los contenedores del servicio para que solo se ejecuten en los nodos con cierto rol.
- **--network:** Conecta los servicios a cierta red que tenga un driver overlay, si no se indica una red Docker conectara los servicios a la red ingress por defecto.

### Visualizar servicios

```bash
docker service ls [parámetros]
```

Lista todos los servicios del cluster junto con su id, nombre, modo, número de réplicas, imagen y puertos.

### Visualizar tareas de un servicio

```bash
docker service ps [parámetros] [id o nombre del servicio]
```

Muestra las tareas de uno o más servicios, además de su id, nombre, imagen, nodo de ejecución, estado actual y deseado, errores y puertos.

### Inspeccionar un servicio

```bash
docker service inspect [parámetros] [id o nombre del servicio]
```

Muestra en detalle la configuración de un servicio en un archivo JSON, algunos de los parámetros más útiles al inspeccionar un servicio con **docker service inspect** son:

- **--pretty:** Cambia el formato JSON con el que se muestran los datos por un formato clásico de consola que es más fácil de leer, pero omite ciertas partes de la configuración al cambiar el formato del texto.

### Modificar la configuración de un servicio

```bash
docker service update [parámetros] [id o nombre del servicio]
```

Actualiza la configuración de un servicio, algunos de los parámetros más útiles al actualizar las configuraciones de un servicio con **docker service update** son:

- **--args [comando]:** Cambia el comando o los parámetros de la tarea principal según la configuración de la imagen del servicio.
- **--replicas [número de réplicas]:** Actualiza el número de réplicas de servicio.
- **--update-parallelism [número de tareas en paralelo]:** Cambia el número de tareas que se actualizan en paralelo, 0 actualiza todo en paralelo.
- **--update-order [start-first|stop-first]:** Cambia el orden en el que se actualizan las tareas, con stop-first las tareas se finalizan antes de iniciar las nuevas tareas, con start-first las tareas viejas no se apagan hasta que las nuevas están arriba.
- **--update-failure-action [pause|continue|rollback]:** Cambia la acción por defecto que se debe realizar en caso de fallar una tarea.
- **--update-max-failure-ratio [porcentaje de fallo]:** Indica el porcentaje de tareas que pueden fallar antes de realizar la acción en caso de fallo.
- **--rollback-parallelism [número de tareas de restauración paralelo]:** Cambia el número de tareas que se restauran en paralelo, 0 actualiza todo en paralelo.
- **--constraint-add node.role==[worker|manager]:** Modifica las restricciones de carga de un servicio a nodos con cierto rol.
- **--env-add [nombre de la variable de entorno]=[valor de la variable de entorno]:** Agrega o actualiza el valor de una o varias variables de entorno.

### Visualizar logs de un servicio

```bash
docker service logs [parámetros] [id o nombre del servicio|id o nombre de la tarea]
```

Muestra los logs de los de un servicio o tarea, algunos de los parámetros más útiles al visualizar los logs de un servicio o tarea con **docker service logs** son:

- **--follow:** Permite hacer follow de los logs del servicio o tarea, es decir que se liga la consola de la máquina anfitrión a los logs para verlos en la medida en la que se imprimen.

### Escalar un servicio

```bash
docker service scale [parámetros] [id o nombre del servicio]=[número de réplicas]
```

Permite escalar uno o varios servicios estableciendo el número de réplicas necesarias por cada servicio.

### Restaurar un servicio a su estado anterior

```bash
docker service rollback [parámetros] [id o nombre del servicio]
```

Permite restaurar un servicio a su estado anterior.

### Eliminar un servicio

```bash
docker service rm [id o nombre del servicio]
```

Elimina un servicio junto con todos sus contenedores y tareas.

## Administración de redes de Docker Swarm

Al utilizar Docker en modo Swarm Docker necesita dos tipos de redes adicionales a las que se usan normalmente, las cuales se usan para comunicar las diferentes tareas o contenedores de un servicio a nivel de nodo y cluster, estas redes son: **docker_gwbridge** e **ingress**, la red docker_gwbrigde por su parte se encarga de comunicar los contenedores del nodo entre ellos y la red ingress, ingress por su parte se encarga de la comunicación de todas las redes docker_gwbrigde a través de todos los nodos del cluster, formando así una red que comunica todos los contenedores de un servicio cuyos contenedores están distribuidos en diferentes nodos, también se diferencian en el alcance y driver, docker_gwbridge está disponible sólo dentro de un nodo y utiliza un driver **bridge** estándar, mientras que ingress está disponible en todos los nodos y utiliza un driver **overlay**, al crear un cluster basado en Docker Swarm las redes docker_gwbridge se crean automáticamente y se conectan a ingress (que es una red creada por defecto), pero es importante saber crear redes con funcionalidades similares a las cuales conectar varios servicios para lograr comunicación entre los contenedores de diferentes servicios sin sobrecargar ingress.

### Crear una red overlay

```bash
docker network create --driver overlay [nombre de la red]
```

Crea una red con un driver overlay la cual tiene conectividad con todo el cluster y funciona de forma similar a la red ingress, por lo que uno o varios servicios se pueden conectar a la nueva red.

## Archivos stack-file.yml

Los archivos [**stack-file.yml**](https://docs.docker.com/compose/compose-file/) son compose file, utilizan la misma sintaxis y muchos de los componentes de un compose file normal, pero los stack file se utilizan con un propósito diferente del de los compose file, la principal diferencia es que los stack file sirven para generar esquemas de servicios basados en Docker Swarm, también llamados **Docker Stacks**, por lo que los servicios de un stack file se ejecutan sobre un cluster en lugar de en una sola máquina, los stack file además soportan componentes que no se utilizan en Docker Compose ya que Docker al identificar en Docker Compose el tipo de aplicación ignora los componentes que son válidos solo en los Docker Stacks, algunos de estos nuevos componentes y sus utilidades son:

- **delpoy:** Restringe los nodos donde se pueden ejecutar las tareas de un servicio.

### Tips de Docker Stacks

#### Ejemplo de un stack file

```yml
version: "3"

services:
  app:
    image: alpine
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    deploy:
      placement:
        constraints: [node.role==worker]

  db:
    image: mongo
```

## Subcomandos de Docker Stacks

Para utilizar stack files como origen de una arquitectura basada en Docker Swarm hay varios subcomandos similares a los usados en la administración regular de Docker Swarm y Docker Compose, algunos de los más relevantes para utilizar aplicaciones basadas en Docker Swarm con stack files son:

### Comandos de administración general de un stack

```bash
docker stack [comando] --help
```

Muestra a grandes rasgos los comandos disponibles para administrar Docker Stacks y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Iniciar o actualizar un stack

```bash
docker stack deploy [parámetros] [nombre del nuevo stack]
```

Inicia o actualiza un stack, algunos de los parámetros más útiles al utilizar **docker stack deploy** para iniciar un stack son:

- **--compose-file [ruta al stack file]:** Establece el compose file que se utilizará para generar el nuevo stack.
- **--orchestrator [swarm|kubernetes|all]:** Establece el orquestador del stack, por defecto se usa swarm.

### Listar stacks

```bash
docker stack ls [parámetros]
```

### Listar tareas de un stack

```bash
docker stack ps [parámetros] [nombre del stack]
```

Lista todas las tareas pertenecientes a un stack.

### Listar servicios de un stack

```bash
docker stack services [parámetros] [nombre del stack]
```

Lista todos los servicios pertenecientes a un stack.

### Eliminar un stack

```bash
docker stack rm [parámetros] [nombre del stack]
```

Elimina un stack junto con todas sus tareas, contenedores, redes y volúmenes.
