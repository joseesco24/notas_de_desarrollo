# Apreciaciones importantes sobre Docker

Docker es un sistema de contenedores que permite que cada uno de nuestros proyectos este autocontenido y empaquetado en una imagen ultra liviana de un sistema operativo Linux, el cual al desplegarse como contenedor **aprovecha partes del sistema operativo de la máquina anfitrión** para completar los componentes necesarios para ejecutarse correctamente, esto lo logra gracias a su arquitectura por capas, cada capa corresponde con una parte necesaria para que nuestro proyecto se ejecute en un contenedor sobre un sistema operativo aislado, en consecuencia cuando una nueva imagen llega a la máquina anfitrión y ya están presentes las capas más pesadas, normalmente del kernel y demas paquetes del OS, solo hace falta descargar e instalar las más livianas, que por lo general son los requerimientos de nuestro proyecto, por lo que no hace falta mover las capas más pesadas, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados como los utilizados en las máquinas virtuales.\
Cabe aclarar que el aislamiento de procesos en Docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo de la máquina anfitrión, no por un sistema operativo virtual que usa el hardware de la máquina anfitrión, en un sistema Linux esto es apreciable con solo revisar los procesos con top, en Windows y en Mac no es apreciable esto, ya que al instalar Docker desktop, Docker por debajo instala una maquina virtual con un sistema operativo Linux que es el que se utiliza para suplir las capas más bajas de los contenedores y por lo tanto es en el sistema operativo de esa máquina virtual en el que se ejecutan los procesos de los contenedores.\
Implementar Docker en nuestros proyectos les otorga una capa adicional de abstracción sobre el cual trabajara nuestro proyecto y también ayuda a atenuar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como los relacionados con la construcción, distribución y ejecución de nuestros proyectos:

- **Construcción**: Al construir o desarrollar aplicaciones con Docker uno de los principales beneficios es que inmediatamente se empieza a usar Docker los entornos de desarrollo y ejecución pueden ser equivalentes ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a Docker se pueden simular condiciones de ejecución con ciertos recursos como la RAM limitados mediante contenedores.
- **Distribución**: Al distribuir aplicaciones mediante imágenes de Docker se garantiza que las dependencias de nuestra aplicación serán instaladas y además, se garantiza que no tendrán conflicto con las del sistema operativo de la máquina anfitrión, ya que están en ambientes aislados, otro beneficio de utilizar imágenes de Docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se alteren nuestra aplicación se comportará de la misma forma.
- **Ejecución**: Ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además Docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

Además de las ventajas ya expuestas otra ventaja que también tiene usar Docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad. Las aplicaciones contenerizadas con Docker (que emplean Docker para construir y desplegar software) tienen varias características, pero los principales son las siguientes:

- **Son flexibles**: Docker engine puede ejecutarse en casi cualquier parte.
- **Son livianas**: Al utilizar la arquitectura por capas y reutilizar partes del OS del anfitrión no hace falta empacar las partes más pesadas del OS usado en las imágenes.
- **Son portables**: Las imágenes creadas con Docker se ejecutan de la misma forma en cualquier máquina independientemente de su software y hardware, limitándose únicamente por el uso del hardware.
- **Tienen un bajo acoplamiento**: Cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos al contenedor para funcionar.
- **Son escalables**: Es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **Son seguras**: Los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones importantes del OS del anfitrión, a no ser que se configuren estas funcionalidades.

Docker se divide en 3 capas con las que es necesario interactuar de cierta forma para para acceder a todas las funcionalidades de Docker y sacarles provecho, las cuales son:

- **Docker server o Docker daemon**: Es el núcleo de Docker, se encarga de manejar todas las entidades que administra Docker.
- **Rest API**: Permite comunicar el Docker daemon con el CLI ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el Docker daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al Docker daemon mediante el uso de esta API y que es la única forma de interactuar con el Docker daemon.
- **Docker CLI o cliente**: Interfaz de línea de comandos que se utiliza de forma local para comunicarse con el Docker daemon, es la forma más sencilla de usar Docker.

Además de las capas con las que es necesario interactuar para usar Docker también es importante tener claros los recursos de los que dispone Docker para desplegar y construir aplicaciones, los cuales son:

- **Contenedores**: Son la clave del funcionamiento de Docker, son ambientes autocontenidos que aprovechan partes del sistema operativo de la máquina anfitrión para dar a nuestras aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier anfitrión con Docker engine instalado.
- **Imágenes**: Las imágenes son la forma en la cual Docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga Docker engine instalado.
- **Redes**: Las redes internas de Docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **Volúmenes de almacenamiento**: Los volúmenes de almacenamiento son la forma que provee Docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos o simplemente para poder usarlos en ejecuciones posteriores, los volúmenes de almacenamiento son totalmente administrados por Docker, lo que los hace inaccesibles para la máquina anfitrión.

## Instalación de Docker en Mac o Windows

Para realizar la instalación de Docker en MacOS o en Windows basta con descargar de [Docker Hub](https://hub.docker.com/) la aplicación de escritorio.

## Instalación de Docker en Ubuntu

Esta pequeña guía de instalación está basada en la [guía oficial](https://docs.docker.com/engine/install/ubuntu/) ofrecida en Docker Hub para instalar Docker engine en **Ubuntu** mediante el sistema de repositorios, cabe aclarar que en Linux no hace falta instalar Docker desktop como en Mac o en Windows, con solo Docker engine es suficiente y además la manipulación del Docker daemon en Linux se hace solo por consola, sin interfaz gráfica, este proceso de instalación aplica para las siguientes versiones de Ubuntu:

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

Luego de haber desinstalado las versiones viejas de Docker se configuran los repositorios necesarios para instalar Docker engine.

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Tras configurar los repositorios necesarios lo siguiente es agregar la llave GPG oficial de Docker.

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg]https://download.docker.com/linux/ubuntu(lsb_release -cs) stable" | sudo tee/etc/apt/sources.list.d/docker.list > /dev/null
```

Una vez configurados los repositorios necesarios y la llave GPG oficial de Docker lo siguiente es configurar el repositorio estable desde el cual se instalará Docker engine.

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

Por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar Docker engine.

### Comprobación de la instalación

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

### En caso de errores

Un error comun al instalar Docker en Ubuntu es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el Docker daemon, por lo tanto si tratamos de usar alguno de los comandos de Docker con nuestro usuario obtendremos un mensaje de error de denegación de permisos, como el presente a continuación.

```bash
docker: Got permission denied while trying to connect to the Docker daemon socket atunix:///var/run/docker.sock: Post http:/%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.See 'docker run --help'.
```

Para solucionar este problema simplemente debemos indicar a Docker que nuestro usuario también va a interactuar con el Docker daemon, esto lo podemos realizar fácilmente con los siguientes comandos.

```bash
sudo usermod -aG docker $USER
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

- **--name [nombre del nuevo contenedor]**: Permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro Docker asigna también un nombre al contenedor.
- **-it**: Ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, it significa interactive terminal.
- **-d**: Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **-p [puerto del anfitrión]:[puerto del contenedor]**: Expone el puerto designado del contenedor en el puerto designado de la máquina anfitrión.
- **--rm**: Indica a Docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **-v [ruta en el anfitrión]:[ruta en el contenedor]**: Crea un bind ligando los archivos de la ruta del contenedor con los de la ruta del anfitrión.
- **--mount src=[nombre o id del volumen],dst=[ruta en el contenedor]**: Liga los archivos que están en la ruta designada del contenedor a un volumen de Docker.
- **--memory [cantidad de memoria ram designada][g:gigas o:megas]**: Limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que requiera.
- **--env [nombre de la variable de ambiente]=[valor de la variable de ambiente]**: Establece una variable de ambiente a la que tendrá acceso el contenedor.

#### Apuntes adicionales

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

- **-a**: Muestra los mismos datos que **docker ps** pero además incluye los contenedores que están actualmente inactivos.
- **-l**: Muestra los mismos datos que **docker ps** pero muestra solo los datos del último contenedor activo.

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

- **-f**: Permite hacer follow de los logs del contenedor, es decir que se liga la consola de la máquina anfitrión a los logs para verlos en la medida en la que se imprimen.
- **--tail [número de logs]**: Imprime los últimos logs limitándose al número de logs indicado.

### Ejecutar tareas en contenedores

```bash
docker exec [parámetros] [nombre o id del contenedor] [comando]
```

Permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando un contenedor con **docker exec** son:

- **-d**: Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.

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

- **-f**: Detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal **sigkill**.

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

- **-t [nombre de la nueva imagen]:[tag de la nueva imagen]**: Permite personalizar el nombre y tag de la nueva imagen que será construida.
- **--f [ruta del Dockerfile]**: Permite cambiar o especificar la ruta al Dockerfile con el cual se construirá la imagen.

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

- **tab**: Alternar entre el panel de capas y el panel de archivos.
- **flechas**: Navegar entre las capas y archivos.
- **ctrl + u**: Filtra los archivos que fueron cambiados en la capa actual.
- **ctrl + c**: Salir de dive.

### Eliminar imágenes

```bash
docker image rm [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Elimina la imagen indicada.

```bash
docker image prune [parámetros]
```

Elimina todas las imágenes residuales o inactivas.

#### Comando pré construído para eliminar imagenes

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

- **--attachable**: Habilita la opción de agregar contendores manualmente a la red.
- **--internal**: Restringe el acceso externo de la red.

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

Los Dockerfile son los archivos que usa Docker al momento de construir una imagen para indicar qué archivos necesita esa imagen, qué dependencias tiene que instalar y que comandos deben ejecutarse al momento de iniciarse como un contenedor a partir de esa imagen, cada instrucción que se ejecuta en un Dockerfile en tiempo de construcción es una nueva capa, algunos de los instrucciones que se pueden usar en un Dockerfile y sus funciones se listan a continuación:

- **FROM [nombre de la imagen]:[versión de la imagen]**: Indica la imagen base, o primera capa que se va a utilizar para construir la nueva imagen, siempre es el primer comando de un Dockerfile.
- **RUN [comando]**: Ejecuta un comando en tiempo de construcción, los comandos que se ejecutan con **RUN** solo se ejecutan al momento de construir una imagen, no al momento de iniciar un contenedor a partir de una imagen resultante de un Dockerfile que implemente esta instrucción.
- **WORKDIR [ruta dentro del contenedor]**: Establece un directorio de trabajo que será el directorio en el que se posicionará el contenedor al iniciar su ejecución.
- **COPY [ruta archivo 0, ruta archivo 1, ... ruta archivo n, ruta destino contenedor]**: Copia todos los archivos indicados en la ruta de destino de la imagen, cabe aclarar que Docker solo da acceso a la imagen en tiempo de construcción al directorio especificado como contexto, por lo que los archivos que se quieren copiar a la imagen deben estar dentro del contexto de construcción para poder ser empaquetados dentro de la misma.
- **EXPOSE [número de puerto]**: Expone un puerto del contenedor permitiendo que ese puerto sea vinculable o bindable a un puerto de la máquina anfitrión.
- **CMD ["parte 1 del comando", "parte 2 del comando"]**: Exec form para ejecutar un comando, ejecutar procesos con exec form hace que los procesos se ejecuten directamente, lo que pone el proceso indicado como proceso principal del contenedor.
- **CMD [comando entero]**: bash form para ejecutar un comando, ejecutar procesos con bash form hace que los procesos se ejecuten como procesos hijos de un bash, lo que pone al bash como proceso principal del contenedor en lugar del proceso indicado.
- **ENTRYPOINT ["parte 1 del comando", "parte 2 del comando"]**: Exec form para ejecutar un entrypoint, ejecuta el entrypoint como proceso principal.
- **ENTRYPOINT [comando entero]**: bash form para ejecutar un entrypoint, ejecuta el entrypoint como proceso hijo del bash.

### Tips de Dockerfile

- Docker no construye de nuevo las capas a no ser que haya cambios, esto lo logra utilizando el caché de capas, es importante construir los Dockerfile considerando el caché de capas para facilitar el proceso de desarrollo.
- Utilizando monitores de scripting y bind mounts, como nodemon, se puede lograr que Docker actualice el código que se está ejecutando en tiempo de ejecución sin tener que reconstruir la imagen de nuevo.
- En Docker existe un archivo llamado **.dockerignore** que funciona igual que **.gitignore**, su función es evitar que cierto tipo de archivos copien la imagen al construirla.
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

## Instalación de Docker compose en Ubuntu

Docker-compose se instala junto a las versiones de escritorio de Windows o Mac, sin embargo en la versión de Ubuntu es necesario instalarlo manualmente con los siguientes comandos, los cuales son extraídos de la guia oficial de [Docker Hub](https://docs.docker.com/compose/install/):

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Subcomandos de Docker compose

Docker-compose tiene varios subcomandos similares a los usados en la administración regular de Docker, algunos de los más relevantes son:

### Comandos de administración general de compose

```bash
docker-compose [comando] --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar el comando del que se necesita más información se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

### Construir las imágenes necesarias para una aplicación de compose

```bash
docker-compose build [parámetros] [nombre del servicio]
```

Construye las imágenes que requieren ser construidas según el **compose file**, al especificarse uno o varios servicios solo se construirán las imágenes de los servicios indicados.

### Iniciar una aplicación con compose

```bash
docker-compose up [parámetros] [nombre del servicio]
```

Levanta la arquitectura descrita por el **compose file** en caso de no indicarse un servicio en concreto, si se indica un servicio solo ese servicio será ejecutado, algunos de los parámetros más útiles al utilizar **docker-compose up** para levantar una arquitectura son:

- **-d**: Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **--scale [nombre o id del servicio]=[número de contenedores]**: Escala un determinado servicio al número de contenedores indicado.

### Revisar el estado de los contenedores generados por compose

```bash
docker-compose ps [parámetros] [nombre del servicio]
```

Muestra el estado de los contenedores creados por el **compose file** en caso de no indicarse un servicio en concreto, si se indica un servicio solo se mostrará el estado de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose ps** para ver el estado de los contenedores pertenecientes a una arquitectura son:

- **-a**: Muestra todos los contenedores de la aplicación independientemente de si están o no ejecutados.

### Revisar los logs de una aplicación compose

```bash
docker-compose logs [parámetros] [nombre del servicio]
```

Muestra los logs de todos los contenedores usados por la aplicación en caso de no indicarse un servicio en concreto, si se indica un servicio sólo se mostrarán solo los logs de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose logs** para ver los logs de una arquitectura son:

- **-f**: Sirve para hacer follow a los logs de toda la aplicación o de cierto servicio si se indica el servicio.
- **--tail [número de logs]**: Imprime los últimos logs limitándose al número de logs indicado de toda la aplicación o de cierto servicio si se indica el servicio.

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

## Archivos docker-compose.yml

Docker-compose permite usar los 4 recursos de Docker juntos fácilmente desde un solo archivo **docker-compose.yml**, usando este archivo también llamado **compose file** se pueden integrar fácilmente recursos de red, volúmenes, imagenes y contenedores sin necesidad de administrar uno a uno cada tipo de recurso, en síntesis lo que permite Docker-compose es describir de forma declarativa la arquitectura de servicios que la aplicación necesita, y Docker se encargará de crear e integrar cada recursos declarado por detrás evitandonos tener que administraba uno a uno los recursos, algunos de los componentes que soporta **Docker-compose** y sus funciones son:

- **versión**: Indica la versión del compose file, dependiendo de la versión del compose file se indica a Docker-compose qué features puede o no soportar.
- **services**: Indica que servicios componen la aplicación, básicamente son las partes o componentes que interactúan para formar nuestra aplicación y que funcione correctamente, un servicio no es un container explícitamente ya que un servicio puede componerse de uno o muchos contenedores.
- **image**: Establece la imagen que se va a utilizar para ejecutar los contenedores de cierto servicio.
- **environment**: Permite definir variables de ambiente a las que pueden acceder los contenedores de un servicio.
- **depends_on**: Establece las dependencias entre servicios, si un servicio declara dependencia de otro este no deberá ejecutarse si antes no se ejecuta el o los servicios de los que depende.
- **ports**: Bindea un puerto o un rango de puertos de la máquina anfitrión con un puerto de uno o varios contenedores.
- **volumes**: Indica los volúmenes y bind mounts de un servicio.
- **command**: Cambia el comando por defecto del servicio.
- **build**: Indica el contexto con el que se debe construir una nueva imagen que se desplegará en todos los contenedores del servicio indicado, el nombre de la nueva imagen se construye en base al nombre del directorio de trabajo y el nombre del servicio en el siguiente formato **[nombre del directorio de trabajo]\_[nombre del servicio]**.

### Tips de Docker-compose

- Al usar Docker-compose Docker por detrás crea una red dedicada a esa arquitectura a la que conecta todos los contenedores de todos los servicios declarados, el nombre de la red se asigna en base al nombre del directorio de trabajo en el siguiente formato **[nombre del directorio de trabajo]\_default**.
- Al usar Docker-compose Docker por detras trata de asignar nombres únicos a cada contenedor para evitar conflictos a causa de los nombres, los nombres de los contenedores se asigna en base del nombre del directorio de trabajo, el nombre del servicio y un número que diferencia los diferentes contenedores de un servicio en el siguiente formato **[nombre del directorio de trabajo] _ [nombre del servicio] _ [número de contenedor]**.
- Al usar Docker-compose Docker por detrás se asegura que a pesar de los nuevos nombres asignados a los contenedores estos sigan siendo alcanzables por los demás contenedores solo con el nombre del servicio que ejecutan.
- Junto a **docker-compose.yml** se puede utilizar **docker-compose.override.yml**, la ventaja de utilizar docker-compose.override es que se puede personalizar el compose-file sin cambiarlo directamente, lo que evita alterar el compose-file de producción pero nos permite probar pequeños cambios en el sin alterarlo directamente, además Docker por defecto tratar de unir y conservar las definiciones de ambos archivos.
- Las variables de entorno son sencillas de manejar con los archivos **compose** y **compose.override** ya que simplemente se unen las definiciones de ambas y en caso de redefinición en **compose.override** simplemente se sobreescribe el valor de la variable.
- Para el manejo de los puertos lo recomendable es no utilizar definiciones de puertos fuera de **compose** y en caso de hacerse la definición de los puertos debe estar solo en un archivo.
- Las dependencias de servicios se usan siempre desde el **compose.override**.
- Para usar un **compose.override** solo hace falta construir la imagen de forma normal, Docker por defecto detecta el archivo de sobre escritura y lo utiliza.
- Al poner **image** y **build** en un mismo compose la imagen se construye pero se le asigna el nombre de imagen en lugar del nombre por defecto.

#### Ejemplo de un Docker-compose con dos servicios y volúmenes

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

#### Ejemplo de un Docker-compose con dos servicios y bind mount

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

#### Ejemplo de un Docker-compose.override

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      NUEVA_VARIABLE: "mongodb://db:27017/test"
```

Al declarar un **docker-compose.override.yml** como el anterior junto a cualquiera de los **docker-compose.yml** se logra que se construya la imagen y se agregue la variable de ambiente nueva a la imagen.

## Docker swarm
