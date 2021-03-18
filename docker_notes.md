# Apreciaciones importantes sobre Docker

Docker es un sistema de contenedores que permite que cada uno de nuestros proyectos este autocontenido y empaquetado en una imagen ultra liviana de un sistema operativo Linux, el cual al desplegarse como contenedor **aprovecha partes del sistema operativo de la máquina anfitrión** para completar los componentes necesarios para ejecutarse correctamente, esto lo logra gracias a su arquitectura por capas, cada capa corresponde con una parte necesaria para que nuestro proyecto se ejecute en un contenedor sobre un sistema operativo aislado, en consecuencia cuando una nueva imagen llega a la máquina anfitrión y ya están presentes las capas más pesadas, normalmente del kernel y demas paquetes del OS, solo hace falta descargar e instalar las más livianas, que por lo general son los requerimientos de nuestro proyecto, por lo que no hace falta mover las capas más pesadas, es por esto que las imágenes suelen ser muy livianas y además al desplegarse como contenedores proveen todas las funcionalidades de un sistema operativo totalmente virtualizado y aislado, sin ser los contenedores sistemas operativos virtualizados totalmente desacoplados como los utilizados en las máquinas virtuales.
<br>
Cabe aclarar que el aislamiento de procesos en Docker es puramente lógico ya que por debajo los procesos son ejecutados por el sistema operativo de la máquina anfitrión, no por un sistema operativo virtual que usa el hardware de la máquina anfitrión, en un sistema Linux esto es apreciable con solo revisar los procesos con top, en Windows y en Mac no es apreciable esto, ya que al instalar Docker desktop, Docker por debajo instala una maquina virtual con un sistema operativo Linux que es el que se utiliza para suplir las capas más bajas de los contenedores y por lo tanto es en el sistema operativo de esa máquina virtual en el que se ejecutan los procesos de los contenedores.
<br>
Implementar Docker en nuestros proyectos les otorga una capa adicional de abstracción sobre el cual trabajara nuestro proyecto y también ayuda a atenuar algunos de los desafíos más importantes al momento de realizar un desarrollo profesional de software, como los relacionados con la construcción, distribución y ejecución de nuestros proyectos:

- **Construcción:** Al construir o desarrollar aplicaciones con Docker uno de los principales beneficios es que inmediatamente se empieza a usar Docker los entornos de desarrollo y ejecución pueden ser equivalentes ya que todos los contenedores tendrán las mismas dependencias, paquetes y se ejecutarán sobre el mismo sistema operativo independientemente de si es un ambiente de desarrollo o de ejecución, además incluso gracias a Docker se pueden simular condiciones de ejecución con ciertos recursos como la RAM limitados mediante contenedores.
- **Distribución:** Al distribuir aplicaciones mediante imágenes de Docker se garantiza que las dependencias de nuestra aplicación serán instaladas y además, se garantiza que no tendrán conflicto con las del sistema operativo de la máquina anfitrión, ya que están en ambientes aislados, otro beneficio de utilizar imágenes de Docker es que se pueden distribuir y usar fácilmente, ya que son bastante ligeras y además la instalación de dependencias es un proceso automatizado, por lo que independientemente del número de copias siempre que se hagan con base en la misma imagen y no se alteren nuestra aplicación se comportará de la misma forma.
- **Ejecución:** Ya que los entornos de ejecución y desarrollo son equivalentes gracias a que se ejecutan bajo el mismo sistema operativo utilizando las mismas dependencias pre establecidas se descarta totalmente la posibilidad de que algo que funciona en desarrollo no funcione en un entorno de ejecución productivo, además Docker incluso permite limitar recursos, razón por la cual se pueden simular incluso condiciones de ejecución adversas.

Además de las ventajas ya expuestas otra ventaja que también tiene usar Docker es que los contenedores a diferencia de las máquinas virtuales tiene un costo de administración mínimo y además se destruyen, construyen y despliegan con mucha facilidad. Las aplicaciones contenerizadas con Docker (que emplean Docker para construir y desplegar software) tienen varias características, pero los principales son las siguientes:

- **Son flexibles:** Docker engine puede ejecutarse en casi cualquier parte.
- **Son livianas:** Al utilizar la arquitectura por capas y reutilizar partes del OS del anfitrión no hace falta empacar las partes más pesadas del OS usado en las imágenes.
- **Son portables:** Las imágenes creadas con Docker se ejecutan de la misma forma en cualquier máquina independientemente de su software y hardware, limitándose únicamente por el uso del hardware.
- **Tienen un bajo acoplamiento:** Cada aplicación contenerizada es una aplicación autocontenida, no requiere de recursos externos al contenedor para funcionar.
- **Son escalables:** Es extremadamente sencillo replicar varios contenedores para que trabajen al mismo tiempo e incluso es fácil configurarlos para que se comuniquen y trabajen cooperando entre ellos.
- **Son seguras:** Los contenedores acceden solo a los recursos a los que deben acceder, jamás acceden a secciones importantes del OS del anfitrión, a no ser que se configuren estas funcionalidades.

Docker se divide en 3 capas con las que es necesario interactuar de cierta forma para para acceder a todas las funcionalidades de Docker y sacarles provecho, las cuales son:

- **Docker server o Docker daemon:** Es el núcleo de Docker, se encarga de manejar todas las entidades que administra Docker.
- **Rest API:** Permite comunicar el Docker daemon con el CLI ya sea local o remoto, además de con otras interfaces que necesiten interactuar con el Docker daemon, como programas de administración de contenedores, es importante resaltar que cada lenguaje posee su forma de acceder al Docker daemon mediante el uso de esta API y que es la única forma de interactuar con el Docker daemon.
- **Docker CLI o cliente:** Interfaz de línea de comandos que se utiliza de forma local para comunicarse con el Docker daemon, es la forma más sencilla de usar Docker.

Además de las capas con las que es necesario interactuar para usar Docker también es importante tener claros los recursos de los que dispone Docker para desplegar y construir aplicaciones, los cuales son:

- **Contenedores:** Son la clave del funcionamiento de Docker, son ambientes autocontenidos que aprovechan partes del sistema operativo de la máquina anfitrión para dar a nuestras aplicaciones ambientes de ejecución iguales y aislados de forma lógica en cualquier anfitrión con Docker engine instalado.
- **Imágenes:** Las imágenes son la forma en la cual Docker puede empaquetar, transportar y replicar el funcionamiento de un contenedor en cualquier máquina que tenga Docker engine instalado.
- **Redes:** Las redes internas de Docker permiten que las diferentes aplicaciones desplegadas en diferentes contenedores puedan interactuar entre sí.
- **Volúmenes de almacenamiento:** Los volúmenes de almacenamiento son la forma que provee Docker para que una aplicación desplegada en un contenedor puede almacenar datos para que otro contenedor pueda usarlos o simplemente para poder usarlos en ejecuciones posteriores, los volúmenes de almacenamiento son totalmente administrados por Docker, lo que los hace inaccesibles para la máquina anfitrión.

<br>

# Instalación de Docker en Mac o Windows

Para realizar la instalación de Docker en MacOS o en Windows basta con descargar de [Docker Hub](https://hub.docker.com/) la aplicación de escritorio.

<br>

# Instalación de Docker en Ubuntu

Esta pequeña guía de instalación está basada en la [guía oficial](https://docs.docker.com/engine/install/ubuntu/) ofrecida en Docker Hub para instalar Docker engine en **Ubuntu** mediante el sistema de repositorios, cabe aclarar que en Linux no hace falta instalar Docker desktop como en Mac o en Windows, con solo Docker engine es suficiente y además la manipulación del Docker daemon en Linux se hace solo por consola, sin interfaz gráfica, este proceso de instalación aplica para las siguientes versiones de Ubuntu:

- Ubuntu Focal 20.04 (LTS)
- Ubuntu Groovy 20.10
- Ubuntu Bionic 18.04 (LTS)
- Ubuntu Xenial 16.04 (LTS)

<br>

## Comandos de instalación de Docker

```shell
sudo apt-get remove -y docker docker-engine docker.io containerd runc
```

Antes de iniciar con la instalación es necesario eliminar cualquier instalación previa de Docker que se haya hecho en la máquina anfitrión, si no han habido instalaciones previas de Docker en la máquina anfitrión se puede omitir el primer comando.

```shell
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Luego de haber desinstalado las versiones viejas de Docker se configuran los repositorios necesarios para instalar Docker engine.

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Tras configurar los repositorios necesarios lo siguiente es agregar la llave GPG oficial de Docker.

```shell
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg]https://download.docker.com/linux/ubuntu(lsb_release -cs) stable" | sudo tee/etc/apt/sources.list.d/docker.list > /dev/null
```

Una vez configurados los repositorios necesarios y la llave GPG oficial de Docker lo siguiente es configurar el repositorio estable desde el cual se instalará Docker engine.

```shell
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

Por último se utilizan los comandos anteriores para actualizar el índice de paquetes de apt y luego instalar Docker engine.

<br>

## Comprobación de la instalación

Una forma sencilla de comprobar el funcionamiento de Docker engine es utilizando la imagen de Hello-World, para hacer esto se ejecuta el siguiente comando.

```shell
docker run hello-world
```

Otras alternativas más simples para comprobar el funcionamiento de la instalación es tratando de visualizar la información del Docker engine o su versión para esto se puede ejecutar cualquiera de los siguientes comandos.

```shell
docker --version
```

```shell
docker info
```

<br>

## En caso de errores

Un error comun al instalar Docker en Ubuntu es que al realizar la instalacion solo el usuario root posee permisos para ejecutar acciones manipulando el Docker daemon, por lo tanto si tratamos de usar alguno de los comandos de Docker con nuestro usuario obtendremos un mensaje de error de denegación de permisos, como el presente a continuación.

```shell
docker: Got permission denied while trying to connect to the Docker daemon socket atunix:///var/run/docker.sock: Post http:/%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create: dial unix/var/run/docker.sock: connect: permission denied.See 'docker run --help'.
```

Para solucionar este problema simplemente debemos indicar a Docker que nuestro usuario también va a interactuar con el Docker daemon, esto lo podemos realizar fácilmente con los siguientes comandos.

```shell
sudo usermod -aG docker $USER
newgrp docker
```

<br>

# Comandos básicos de administración en Docker

```shell
man docker
```

Muestra el manual de Docker.

<br>

```shell
docker [comando] --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar el comando del que se necesita más información se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

```shell
docker --version
```

Permite ver la versión de Docker instalada actualmente en la máquina anfitrión.

<br>

```shell
docker info [parámetros]
```

Muestra la información del Docker Daemon, como el número de imágenes descargadas, el estado de Swarm o incluso la versión del kernel, entre otros.

<br>

```shell
docker stats [parámetros] [id o nombre del contenedor]
```

Muestra los recursos que está utilizando cada contenedor y docker en general, si se especifica un contenedor con su id o nombre se muestran solo los recursos que está usando ese contenedor.

<br>

```shell
docker system prune [parámetros]
```

Elimina todos los volúmenes, contenedores y redes que no se estén usando, además de imágenes residuales.

<br>

# Administración de contenedores

La administración de contenedores es una actividad clave al utilizar Docker ya que los contenedores son las entidades más importantes que podemos manejar en Docker, esto se debe a que los contenedores son los encargados de virtualizar al ambiente aislado donde se ejecutarán nuestros proyectos, es mediante el uso de contenedores que Docker adquiere tres de sus características más importantes, concretamente el uso de contenedores aporta **flexibilidad**, **seguridad** y **bajo acoplamiento** a nuestros proyectos.
<br>
Algunos de los comandos más importantes provistos por Docker para administrar contenedores se listan en esta sección.

<br>

## Ejecutar contenedores

```shell
docker run [parámetros] [imagen] [comando]
```

Ejecuta un contenedor usando la imagen especificada y ejecutando el comando especificado como proceso principal en caso de ser dado un comando luego de la imagen, es importante entender que si la imagen no tiene definido un proceso principal ni en la imagen ni por comando el contenedor se ejecutará y apagará casi al instante ya que un contenedor se detiene cuando su proceso principal finaliza y el proceso principal por defecto es solo abrir un archivo, algunos de los parámetros más útiles al ejecutar un contenedor con **docker run** son:

- **--name [nombre del nuevo contenedor]:** Permite asignar un nombre personalizado al contenedor el cual puede ser utilizado para referenciar al contenedor como si fuera su id, además es único e irrepetible, en caso de no especificarse un nombre con este parámetro Docker asigna también un nombre al contenedor.
- **-it:** Ejecuta el contenedor y abre una terminal mediante la cual se puede interactuar con el contenedor, it significa interactive terminal.
- **-d:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **-p [puerto del anfitrión]:[puerto del contenedor]:** Expone el puerto designado del contenedor en el puerto designado de la máquina anfitrión.
- **--rm:** Indica a Docker que ese contenedor debe eliminarse tan pronto como se detiene, es decir al finalizar su proceso principal.
- **-v [ruta en el anfitrión]:[ruta en el contenedor]:** Crea un bind ligando los archivos de la ruta del contenedor con los de la ruta del anfitrión.
- **--mount src=[nombre o id del volumen],dst=[ruta en el contenedor]:** Liga los archivos que están en la ruta designada del contenedor a un volumen de Docker.
- **--memory [cantidad de memoria ram designada][g:gigas o:megas]:** Limita la cantidad de memoria ram que puede utilizar el contenedor, si no se limita la ram mediante este parámetro el contenedor utilizar toda la memoria ram que requiera.

**Nota**: al restringir la memoria ram que puede usar una aplicación es posible que este finaliza con el estatus **OOMKilled**, , el cual se puede ver con un **docker inspect** del contenedor, este estatus indica que el contenedor se detuvo debido a que la memoria con la que contaba le fue insuficiente para ejecutar todos sus procesos y por lo tanto colapsó y se detuvo.

<br>

## Cambiar nombres de los contenedores

```shell
docker rename [nombre o id del contenedor] [nuevo nombre]
```

Asigna un nuevo nombre al contenedor especificado.

<br>

## Revisar el estado de los contenedores

```shell
docker ps [parámetros]
```

Muestra todos los contenedores activos en la máquina anfitrión, junto con datos como su id, nombre, nombre de imagen, estatus, puertos expuestos, tiempo de creación y comando del proceso principal, algunos de los parámetros más útiles al visualizar datos de los contenedores con **docker ps** son:

- **-a:** Muestra los mismos datos que **docker ps** pero además incluye los contenedores que están actualmente inactivos.
- **-l:** Muestra los mismos datos que **docker ps** pero muestra solo los datos del último contenedor activo.

```shell
docker inspect [parámetros] [nombre o id del contenedor]
```

Muestra en un archivo JSON toda la información de la configuración de un contenedor en concreto.

<br>

## Mover archivos y directorio entre el anfitrión y los contenedores

```shell
docker cp [parámetros] [ruta host] [nombre o id del contenedor]:[ruta contenedor]
```

Copia un archivo o directorio desde la ruta de origen de la máquina anfitrión en la ruta de destino del contenedor designado.

```shell
docker cp [parámetros] [nombre o id del contenedor]:[ruta contenedor] [ruta host]
```

Copia un archivo o directorio desde la ruta de origen del contenedor designado en la ruta de destino de la máquina anfitrión.

<br>

## Visualizar los logs de los contenedores

```shell
docker logs [parámetros] [nombre o id del contenedor]
```

Sirve para ver los logs de un contenedor especificado, algunos de los parámetros más útiles al ver los logs de un contenedor con **docker logs** son:

- **-f:** Permite hacer follow de los logs del contenedor, es decir que se liga la consola de la máquina anfitrión a los logs para verlos en la medida en la que se imprimen.
- **--tail [número de logs]:** Imprime los últimos logs limitándose al número de logs indicado.

<br>

## Ejecutar tareas en contenedores

```shell
docker exec [parámetros] [nombre o id del contenedor] [comando]
```

Permite ejecutar un comando en un contenedor activo, algunos de los parámetros más útiles al ejecutar un comando un contenedor con **docker exec** son:

- **-d:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.

<br>

### Comando pré construído:

```shell
docker exec [nombre o id del contenedor] ps -ef
```

El comando anterior es una extensión de **docker exec** que muestra los procesos que se están ejecutando dentro del contenedor indicado.

<br>

## Apagar contenedores

```shell
docker stop [parámetros] [nombre o id del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigterm**, en caso de que la señal **sigterm** no logre apagar el contenedor se envía la señal **sigkill** 5 segundos después.

```shell
docker kill [parámetros] [nombre o id del contenedor]
```

Apaga manualmente un contenedor usando la señal **sigkill**.

<br>

## Eliminar contenedores

```shell
docker rm [parámetros] [nombre o id del contenedor]
```

Sirve para borrar contenedores, Docker por defecto no elimina ningún contenedor, al finalizar el proceso principal del contenedor simplemente lo detiene, por lo que es usual tener que borrar contenedores manualmente para mantener en espacio de trabajo ordenado y evitar llenar el almacenamiento con contenedores que no es están usando, algunos de los parámetros más útiles al borrar un contenedor con **docker rm** son:

- **-f:** Detiene un contenedor actualmente activo para así poder eliminarlo, la detención del contenedor se fuerza usando la señal **sigkill**.

```shell
docker container prune [parámetros]
```

Borra todos los contenedores inactivos.

<br>

### Comando pré construído:

```shell
docker rm -f $(docker ps -aq)
```

El comando anterior es una extensión de **docker rm** pero tiene la funcionalidad de eliminar todos los contenedores activos o inactivos y para eliminar los activos fuerza su detención antes de eliminarlos con la señal **sigkill**.

<br>

# Administración de imágenes

En términos de relevancia las imágenes en Docker podrían considerarse como el segundo tipo de entidad más relevantes después de los contenedores, estando casi a la par en relevancia, lo que hace a la administración de imágenes el segundo tipo de actividad más relevante al usar Docker, si bien los contenedores son la forma de virtualizar un ambiente aislado sobre el que se ejecutara nuestro proyecto, las imágenes se encargan de indicar la forma en la que el contenedor debe construir ese ambiente, además es gracias a las imágenes que es fácil mover, desplegar y replicar un proyecto las veces que haga falta, sin alterar el funcionamiento del mismo, es por esto que las imágenes son las que aportan a nuestros proyectos las tres características restantes principales de Docker, concretamente las imágenes aportan **escalabilidad**, **portabilidad** y **ligereza** a nuestros proyectos.
<br>
Algunos de los comandos más importantes provistos por Docker para administrar imágenes se listan en esta sección.

<br>

## Construir imágenes

```shell
docker build [parámetros] [ruta del contexto]
```

Crea y almacena una nueva imagen usando como contexto la ruta suministrada, el contexto es la ruta donde estan los archivos que se necesitan para construir la imagen, como los .dockerignore, Dockerfile y los archivos que se cargaran a la imagen, entre otros, si no se dan parámetros la imagen se crea solo con un id, sin guardar un nombre o un tag, algunos de los parámetros más útiles al crear una imagen con **docker build** son:

<br>

- **-t [nombre de la nueva imagen]:[tag de la nueva imagen]**: Permite personalizar el nombre y tag de la nueva imagen que será construida.
- **--f [ruta del Dockerfile]:** Permite cambiar o especificar la ruta al Dockerfile con el cual se construirá la imagen.

<br>

## Bajar imágenes

```shell
docker pull [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Baja la imagen con el nombre y el tag especificado, si no se especifica un tag se baja la versión más reciente o por defecto de la imagen.

<br>

## Subir imágenes

Antes de subir una imagen a nuestro repositorio es necesario iniciar sesión con nuestro usuario en el CLI de Docker, esto se hace con el siguiente comando.

```shell
docker login [parámetros]
```

Una vez iniciada la sesión ya podemos cargar nuestra imagen a nuestro repositorio con el siguiente comando.

```shell
docker push [parámetros] [repositorio o nombre de usuario de Docker Hub]/[nombre o id de la imagen]:[tag de la imagen]
```

Sube la imagen con el nombre y el tag especificado al repositorio indicado.

<br>

## Cambiar tags de imágenes

```shell
docker tag [nombre o id de la imagen de origen]:[tag de la imagen de origen] [repositorio o nombre de usuario de Docker Hub]/[nombre o id de la nueva imagen]:[tag de la nueva imagen]
```

Crea una nueva imagen que se hace referencia a una ya existente y que se puede publicar en nuestro repositorio.

<br>

## Listar imágenes

```shell
docker image ls [parámetros]
```

Lista todas las imágenes almacenadas localmente.

<br>

## Visualizar capas de imágenes

```shell
docker history [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Muestra las capas de una imagen de forma simplificada.

<br>

Otra herramienta muy útil para visualizar las capas de una imagen con más profundidad es [dive](https://github.com/wagoodman/dive), dive a diferencia de los comandos nativos de Docker da más información sobre las capas de cada imagen, algunos de los comandos básicos para ver información de las imágenes con dive son:

```shell
dive [nombre o id de la imagen]:[tag de la imagen]
```

Para abrir los detalles de la imagen con dive, luego de abrir una imagen con dive podemos usar las siguientes combinaciones de teclas para navegar por las secciones de dive:

- **tab**: Alternar entre el panel de capas y el panel de archivos.
- **flechas**: Navegar entre las capas y archivos.
- **ctrl + u**: Filtra los archivos que fueron cambiados en la capa actual.
- **ctrl + c**: Salir de dive.

<br>

## Eliminar imágenes

```shell
docker image rm [parámetros] [nombre o id de la imagen]:[tag de la imagen]
```

Elimina la imagen indicada.

<br>

```shell
docker image prune [parámetros]
```

Elimina todas las imágenes residuales o inactivas.

<br>

### Comando pré construído:

```shell
docker image rm -f $(docker image ls -q)
```

El comando anterior es una extensión de **docker image rm** pero tiene la funcionalidad de eliminar todos las imágenes independientemente de si son residuales o no.

<br>

# Administración de volúmenes

Los volúmenes son una parte fundamental al usar Docker para desarrollar una solución ya que son las unidades virtuales de almacenamiento que normalmente usan los contenedores para guardar y compartir datos entre ellos de forma sencilla, usar volúmenes garantiza que los datos almacenados persistirán incluso si se detiene o elimina el contenedor que hacía uso del volumen, cabe aclarar que los volúmenes son espacios de memoria del anfitrión que Docker usa para almacenar archivos de los contenedores, al igual que con los bind, pero a diferencia de los bind los volúmenes solo son administrados únicamente por Docker y no conceden al contenedor acceso al sistema de directorios del anfitrión, lo que los hace más seguros de usar que los bind, es por esto último que los volúmenes son la opción más recomendable al utilizar un medio de almacenamiento de datos del contenedor una solución desplegada para producción.
<br>
Los comandos provistos por Docker para administrar volúmenes se listan en esta sección.

<br>

## Crear volúmenes

```shell
docker volume create [parámetros] [nombre]
```

Crea un volúmen y le asigna el nombre indicado.

<br>

## Listar volúmenes

```shell
docker volume ls [parámetros]
```

Lista todos los volúmenes de Docker mostrando su driver y nombre.

<br>

## Eliminar volúmenes

```shell
docker volume rm [parámetros] [nombre]
```

Elimina el volumen indicado.

```shell
docker volume prune [parámetros]
```

Elimina todos los volúmenes residuales o inactivos almacenados localmente.

<br>

### Comando pré construído:

```shell
docker volume rm -f $(docker volume ls -q)
```

El comando anterior es una extensión de **docker volume rm** pero tiene la funcionalidad de eliminar todos los volúmenes independientemente de si son residuales o no.

<br>

# Administración de redes

Las redes son una parte fundamental al usar Docker para desarrollar una solución ya que usándolas se puede lograr que varios contenedores en la misma red se comunican, y cooperan generando un esquema de micro servicios, una de las principales ventajas de usar redes de Docker es que se puede usar directamente el nombre del contenedor para establecer las comunicaciones y a diferencia de el uso de conexiones directas por API usando redes de Docker no hace falta que un contenedor salga a internet para comunicarse con otro.
<br>
Los comandos provistos por Docker para administrar redes se listan en esta sección.

<br>

## Crear redes

```shell
docker network create [parámetros] [nombre]
```

Crea un nueva red de Docker, algunos de los parámetros más útiles al crear una red con **docker network create** son:

- **--attachable**: Habilita la opción de agregar contendores manualmente a la red.
- **--internal**: Restringe el acceso externo de la red.

<br>

## Listar redes

```shell
docker network ls [parámetros]
```

Lista todas las redes de Docker, mostrando su nombre, tipo de driver, id y alcance:

<br>

## Inspeccionar redes

```shell
docker network inspect [parámetros] [nombre o id de la red]
```

Muestra todas las configuración de una red en formato JSON, incluidos los contenedores conectados a ella.

<br>

## Conectar y desconectar redes con contenedores

```shell
docker network connect [parámetros] [id o nombre de la red] [id o nombre del contenedor]
```

Conecta un contenedor a una red.

```shell
docker network disconnect [parámetros] [id o nombre de la red] [id o nombre del contenedor]
```

Desconecta un contenedor de una red.

<br>

## Eliminar redes

```shell
docker network rm [parámetros] [nombre]
```

Elimina la red indicada.

```shell
docker network prune [parámetros]
```

Elimina todas las redes residuales o inactivas.

<br>

### Comando pré construído:

```shell
docker network rm $(docker network ls -q)
```

El comando anterior es una extensión de **docker network rm** pero tiene la funcionalidad de eliminar todos las redes independientemente de si son residuales o no.

<br>

# Comandos pre construidos de limpieza

Los siguientes comandos simplemente son una compilación de los comandos de las secciones anteriores, en conjunto y ejecutados en secuencia eliminan todos los contenedores, imágenes, volúmenes y redes que se hayan creado.

```shell
docker rm -f $(docker ps -aq)
docker image rm -f $(docker image ls -q)
docker volume rm -f $(docker volume ls -q)
docker network rm $(docker network ls -q)
```

<br>

# Docker compose

<br>

# Docker swarm

<br>
