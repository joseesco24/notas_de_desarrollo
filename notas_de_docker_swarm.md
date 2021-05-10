# Notas De Docker Swarm

- [Introducción](#introducción)
- [Administración De Un Cluster](#administración-de-un-cluster)
  - [Inspeccionar Un Comando De Administración Del Cluster De Docker Swarm](#inspeccionar-un-comando-de-administración-del-cluster-de-docker-swarm)
  - [Iniciar Un Cluster](#iniciar-un-cluster)
  - [Conectar Máquinas Al Cluster](#conectar-máquinas-al-cluster)
  - [Desconectar Máquinas Del Cluster](#desconectar-máquinas-del-cluster)
- [Administración De Nodos Pertenecientes A Un Cluster](#administración-de-nodos-pertenecientes-a-un-cluster)
  - [Inspeccionar Un Comando De Administración De Nodos De Docker Swarm](#inspeccionar-un-comando-de-administración-de-nodos-de-docker-swarm)
  - [Listar Los Nodos Conectados Al Cluster](#listar-los-nodos-conectados-al-cluster)
  - [Inspeccionar Un Nodo](#inspeccionar-un-nodo)
  - [Actualizar Las Configuraciones De Un Nodo](#actualizar-las-configuraciones-de-un-nodo)
- [Administración De Servicios Basados En Docker Swarm](#administración-de-servicios-basados-en-docker-swarm)
  - [Inspeccionar Un Comando De Administración De Servicios De Docker Swarm](#inspeccionar-un-comando-de-administración-de-servicios-de-docker-swarm)
  - [Iniciar Un Servicio](#iniciar-un-servicio)
  - [Listar Servicios](#listar-servicios)
  - [Inspeccionar Tareas De Un Servicio](#inspeccionar-tareas-de-un-servicio)
  - [Inspeccionar Un Servicio](#inspeccionar-un-servicio)
  - [Modificar La Configuración De Un Servicio](#modificar-la-configuración-de-un-servicio)
  - [Inspeccionar Los Logs De Un Servicio](#inspeccionar-los-logs-de-un-servicio)
  - [Escalar Un Servicio](#escalar-un-servicio)
  - [Restaurar Un Servicio A Su Estado Anterior](#restaurar-un-servicio-a-su-estado-anterior)
  - [Eliminar Un Servicio](#eliminar-un-servicio)
- [Administración De Redes De Docker Swarm](#administración-de-redes-de-docker-swarm)
  - [Crear Una Red Overlay](#crear-una-red-overlay)

<br>

## Introducción

[**docker swarm**](https://docs.docker.com/engine/swarm/) es la solución nativa que ofrece docker para montar aplicaciones basadas en cómputo distribuido y en contenedores, lo que propone docker swarm es que al montar un cluster en el que se quieren desplegar aplicaciones contenerizadas bajo el esquema de servicios el cluster debe ser fácilmente administrable, bajo esta premisa docker swarm ha llegado hasta el punto en el que un desarrollador puede tratar la totalidad del cluster como si se tratase de un solo entorno de docker que atraviesan muchas máquinas, gracias a esto es que usando docker swarm es posible administrar un cluster casi con la facilidad con la que se administra una sola máquina con un solo docker daemon, cuando en realidad son varias máquinas cada uno con su propio docker daemon. para conseguir este funcionamiento docker swarm se basa en tres conceptos fundamentales, estos tres conceptos son **swarm**, **nodos** y **servicios**, cada uno de estos conceptos corresponde a un tipo de entidad que compone una aplicación basada en docker swarm, las definiciones resumidas de cada uno de estos conceptos se listan a continuación:

- **swarm:** swarm, cluster o enjambre son referencias del mismo concepto, una agrupación de varias máquinas que cooperan para realizar la misma tarea, en el caso de docker swarm, desplegar contenedores de una aplicación para aumentar su disponibilidad y escalabilidad.
- **nodos:** los nodos son todas las máquinas que componen el swarm, cluster o enjambre, entre los nodos se reparten las tareas que deben ser ejecutadas, en el caso de docker swarm, los contenedores que deben ser ejecutados y la gestión de recursos necesaria para mantener el correcto funcionamiento del cluster.
- **servicios:** los servicios son uno o varios contendores que ejecutan la misma aplicación en diferentes nodos en un mismo cluster, con el objetivo de que ese servicio tenga una muy alta disponibilidad y además sea altamente escalable.

es gracias a la división de las labores de administración de la aplicación en estas tres entidades que las aplicaciones desplegadas con docker swarm son muy fáciles de administrar, ya que se pueden administrar como entidades separadas a pesar de que forman parte de una misma aplicación, siempre tomando en cuenta la forma en la cual alterar una entidad afectará el comportamiento de la aplicación y de las demás entidades.\
al utilizar docker swarm las máquinas que componen el cluster o nodos se divide en dos tipos, **managers** y **workers**, siendo los managers los encargados de gestionar los recursos el cluster, mientras que los workers se encargaran de ejecutar las tareas que les son asignadas por los managers, las funciones específicas de los dos tipos de nodo se lista a continuación:

- **managers:** gestiona las comunicaciones, distribuyen las tareas, gestionan los recursos y se encargan de re posicionar contenedores y tareas en caso de caídas de algún nodo del cluster, el número de managers siempre debe ser impar, ya que de los manager solo uno es el líder del cluster y además el manager líder se rota periódicamente utilizando el algoritmo [**raft**](https://www.freecodecamp.org/news/in-search-of-an-understandable-consensus-algorithm-a-summary-4bc294c97e0d/), debe haber solo un líder ya que así se evita conflictos en la administración del cluster, por esto en un cluster productivo deben haber minimo 3 maquinas asumiendo el rol de manager.
- **workers:** ejecutan los contenedores de la aplicación, además los workers se pueden dividir en diferentes grupos según ciertas características de los servicios y de la máquina que los va a ejecutar, como la capacidad de la cpu.

por lo general en una aplicación basado en docker swarm hay más nodos worker que manager, ya que los worker son el núcleo de la aplicación al ser los que ejecutan la aplicacion como tal, mientras que los manager están dedicados exclusivamente a gestionar el cluster, si bien los manager también pueden ejecutar contendores de la aplicación no es recomendable, ya que esto generaría una competencia de recursos entre las tareas de gestión del cluster y de ejecución de contenedores de la aplicación, lo que podría generar errores en la gestión del cluster y en consecuencia en la totalidad de la aplicación.\
las únicas restricciones al momento de crear una aplicación usando docker swarm es que todos los nodos deben estar en la misma red o subred y deben ser visibles entre ellos, además todos tiene que tener instalado el docker daemon, idealmente de la misma versión.\
antes de desplegar una aplicación basada en docker swarm lo adecuado es revisar que la aplicación cumpla ciertos factores para poder sacarle todo el provecho al cluster, si bien hay muchos factores a considerar, hay consenso en [**12 factores clave**](https://12factor.net/) que deben ser tomados en cuenta antes de decidir si una aplicación está lista o no para ser desplegada con docker swarm, muy resumidamente los 12 factores son:

1. el código fuente de la aplicación debe estar en un repositorio versionado y además debe haber una paridad de 1 a 1 entre el repositorio y la aplicación, por lo que no puede haber código de varias aplicaciones diferentes en el repositorio.

1. las dependencias deben estar declaradas explícitamente en un archivo de dependencias, el cual debe estar empaquetado junto al código fuente de la aplicación, siempre debe asumirse que las dependencias no están instaladas por lo que es necesario instalarlas con su archivo de dependencias correspondiente.

1. las definiciones de configuración de la aplicación deben estar empaquetadas junto a la aplicación y la aplicación debe estar diseñada para que bajo ninguna circunstancia la configuración cambie en función del servidor.

1. los servicios de apoyo con los que interactúa la aplicación se tratan como aplicaciones externas a las que la aplicación se conecta, no como componentes o complementos de la aplicación como tal.

1. se deben separar estrictamente las etapas de construcción, liberación y ejecución, no debe haber procesos en etapas que no les corresponden, por ejemplo, un proceso de construcción jamás debe ocurrir en una etapa de ejecución, máximo en una etapa de ejecución se pueden hacer configuraciones.

1. la aplicación tiene que poder ejecutarse como un proceso stateless, es decir que no debe depender de ciertos estados de memoria o archivos que ya están en la máquina y en caso de necesitar archivos deben ser capaces de generarlos.

1. las aplicaciones deben exponerse a sí mismas mediante puertos vinculados entre el host y la aplicación, siempre evitando utilizar intermediarios.

1. la aplicación debe poder ejecutarse con múltiples instancias en paralelo.

1. la aplicación debe poder apagarse, destruirse y levantarse muy rápidamente.

1. el entorno de desarrollo y el entorno de producción deben ser lo más parecidos posibles.

1. todos los logs de la aplicación deben emitirse por la salida estándar, de tal modo que si se necesitan simplemente se puedan inspeccionar y recolectar.

1. todas las labores de administración deben poder realizarse sin alterar la ejecución de la aplicación, es decir que no debe ser necesario reiniciar la aplicación en cierto modo o con cierto estado para poder administrar.

docker swarm además viene instalado con docker engine, por lo que no hace falta instalarlo una vez ya está instalado docker engine, docker swarm además admite instalar plugins y clientes para administrar los contenedores y demás recursos de forma gráfica como [**portainer**](https://www.portainer.io/), ademas de agragar servicios para relizar monitoreo como [**swarmprom**](https://github.com/stefanprodan/swarmprom) o gestionar recursos como [**docker-cleanup**](https://github.com/meltwater/docker-cleanup).\
al gestionar una solución productiva basada en docker swarm es sumamente importante mantener los nodos limpios, es decir sin imágenes, contenedores o demás recursos residuales que ocupen disco, gestionar los logs de los servicios para que no llenen los discos de los nodos y poder visualizar el estado del cluster.

<br>

## Administración De Un Cluster

el cluster, enjambre o swarm es lo que permite que una aplicación basada en docker swarm escale sobre un hardware virtualmente infinito, es por esto que si bien el cluster no es muy difícil de administrar y no hay muchos comandos con los cuales administrarlo, es importante tener en cuenta los comandos necesarios para administrar y escalar el cluster, ya que del cluster depende que tanto puede escalar la aplicación a nivel de hardware.

<br>

### Inspeccionar Un Comando De Administración Del Cluster De Docker Swarm

```unknown
docker swarm <comando> --help
```

muestra a grandes rasgos los comandos disponibles para administrar el cluster y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Iniciar Un Cluster

```unknown
docker swarm init <parámetros>
```

inicia un cluster utilizando la máquina actual como el primer manager del cluster, algunos de los parámetros más útiles al utilizar **docker swarm init** para iniciar un cluster son:

- **--advertise-addr &lt;ip&gt;:** al iniciar un cluster en una máquina con múltiples interfaces de red se utiliza para indicar al manager cuál de estas debe utilizar para las comunicaciones del cluster.

<br>

### Conectar Máquinas Al Cluster

```unknown
docker swarm join-token <parametros> <worker|manager>
```

genera un token que es utilizado para agregar una nueva máquina al cluster, hay dos tipos de tokens, uno para agregar managers y otro para agregar workers, al utilizar este comando además de imprimir el token se imprime el comando que permitirá utilizarlo para unir una máquina nueva al cluster.

<br>

### Desconectar Máquinas Del Cluster

```unknown
docker swarm leave <parametros>
```

permite a la máquina actual abandonar el cluster, para dejar el cluster con **docker swarm leave** solo puede utilizarse un parámetro adicional, éste es:

- **--force:** permite forzar a la máquina actual a abandonar el cluster, cuando se requiere que un manager abandone el cluster suele ser necesario utilizar este parámetro, ya que docker swarm no permite que los manager abandonen el cluster fácilmente por seguridad.

<br>

## Administración De Nodos Pertenecientes A Un Cluster

los nodos son las maquinas que estan conectadas al cluster, no hay muchas opciones para administrar nodos, pero varios de estos comandos son muy útiles y es bueno tomarlos en cuenta, además, la administración de nodos sólo puede hacerse desde un manager, ya que los workers no suelen tener acceso a estas acciones.

<br>

### Inspeccionar Un Comando De Administración De Nodos De Docker Swarm

```unknown
docker node <comando> --help
```

muestra a grandes rasgos los comandos disponibles para administrar los nodos de un cluster y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Listar Los Nodos Conectados Al Cluster

```unknown
docker node ls <parámetros>
```

lista los nodos pertenecientes a un cluster, mostrando su id, nombre, estatus, disponibilidad, su versión de docker engine y si es manager o worker, además, se indica con \* el nodo en el que se está actualmente.

<br>

### Inspeccionar Un Nodo

```unknown
docker node inspect <parámetros> <id o nombre del nodo>
```

muestra en detalle la configuración de un nodo en un archivo json, algunos de los parámetros más útiles al inspeccionar un nodo con **docker node inspect** son:

- **--pretty:** cambia el formato json con el que se muestran los datos por un formato clásico de consola que es más fácil de leer, pero omite ciertas partes de la configuración al cambiar el formato del texto.

<br>

### Actualizar Las Configuraciones De Un Nodo

```unknown
docker node update <parámetros> <id o nombre del nodo>
```

permite actualizar ciertas configuraciones de un nodo, algunos de los parámetros más útiles al actualizar la configuración de un nodo con **docker node update** son:

- **--availability &lt;active|pause|drain&gt;:** permite cambiar la disponibilidad de un nodo, en estado activo se le pueden asignar tareas al nodo sin problema, en estado pausado el nodo no recibe tareas y en estado de drenado se sacan del nodo todas las tareas y se envían a otros nodos antes de ser puesto el nodo en estado pausado.

<br>

## Administración De Servicios Basados En Docker Swarm

los servicios son la base de docker swarm, al igual que en docker compose un servicio es una aplicación contenerizada que está desplegada en uno o más contenedores, en docker swarm la ventaja es que estos contenedores pueden estar ejecutándose en cualquier nodo del cluster y además pueden moverse entre nodos fácilmente, es debido a esto que los servicios son altamente disponibles y escalables, al trabajar con servicios se trabaja implícitamente con contenedores ya que docker swarm se encarga de gestionar los contenedores en función de la declaración del servicio.

<br>

### Inspeccionar Un Comando De Administración De Servicios De Docker Swarm

```unknown
docker service <comando> --help
```

muestra a grandes rasgos los comandos disponibles para administrar servicios y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Iniciar Un Servicio

```unknown
docker service create <parámetros> <nombre o id de la imagen> <comando>
```

permite iniciar un servicio basado en docker swarm especificando la imagen y el comando del proceso principal, si no se especifica el comando del proceso principal se usa el proceso principal por defecto, algunos de los parámetros más útiles al iniciar un servicio con **docker service create** son:

- **--name &lt;nombre del servicio&gt;:** establece el nombre indicado como nombre del servicio.
- **--publish &lt;puerto del anfitrión&gt;:&lt;puerto del contenedor&gt;:** utiliza la red ingress y el routing mesh de docker swarm para exponer la aplicación.
- **--replicas &lt;número de réplicas&gt;:** establece el número de réplicas o contenedores que deben ejecutarse de cierto servicio.
- **--constraint node.role==&lt;worker|manager&gt;:** limita los contenedores del servicio para que solo se ejecuten en los nodos con cierto rol.
- **--network:** conecta los servicios a cierta red que tenga un driver overlay, si no se indica una red docker conectara los servicios a la red ingress por defecto.
- **--label &lt;metadatos&gt;:** permite agregar un listado de metadatos útiles para los otros servicios que necesitan encontrar el nuevo servicio.
- **--mode &lt;replicated|global|replicated-job|global-job&gt;:** cambia el modo en el que se ejecuta un servicio.

<br>

### Listar Servicios

```unknown
docker service ls <parámetros>
```

lista todos los servicios del cluster junto con su id, nombre, modo, número de réplicas, imagen y puertos.

<br>

### Inspeccionar Tareas De Un Servicio

```unknown
docker service ps <parámetros> <id o nombre del servicio>
```

muestra las tareas de uno o más servicios, además de su id, nombre, imagen, nodo de ejecución, estado actual y deseado, errores y puertos.

<br>

### Inspeccionar Un Servicio

```unknown
docker service inspect <parámetros> <id o nombre del servicio>
```

muestra en detalle la configuración de un servicio en un archivo json, algunos de los parámetros más útiles al inspeccionar un servicio con **docker service inspect** son:

- **--pretty:** cambia el formato json con el que se muestran los datos por un formato clásico de consola que es más fácil de leer, pero omite ciertas partes de la configuración al cambiar el formato del texto.

<br>

### Modificar La Configuración De Un Servicio

```unknown
docker service update <parámetros> <id o nombre del servicio>
```

actualiza la configuración de un servicio, algunos de los parámetros más útiles al actualizar las configuraciones de un servicio con **docker service update** son:

- **--args &lt;comando&gt;:** cambia el comando o los parámetros de la tarea principal según la configuración de la imagen del servicio.
- **--replicas &lt;número de réplicas&gt;:** actualiza el número de réplicas de servicio.
- **--update-parallelism &lt;número de tareas en paralelo&gt;:** cambia el número de tareas que se actualizan en paralelo, 0 actualiza todo en paralelo.
- **--update-order &lt;start-first|stop-first&gt;:** cambia el orden en el que se actualizan las tareas, con stop-first las tareas se finalizan antes de iniciar las nuevas tareas, con start-first las tareas viejas no se apagan hasta que las nuevas están arriba.
- **--update-failure-action &lt;pause|continue|rollback&gt;:** cambia la acción por defecto que se debe realizar en caso de fallar una tarea.
- **--update-max-failure-ratio &lt;porcentaje de fallo&gt;:** indica el porcentaje de tareas que pueden fallar antes de realizar la acción en caso de fallo.
- **--rollback-parallelism &lt;número de tareas de restauración paralelo&gt;:** cambia el número de tareas que se restauran en paralelo, 0 actualiza todo en paralelo.
- **--constraint-add node.role==&lt;worker|manager&gt;:** modifica las restricciones de carga de un servicio a nodos con cierto rol.
- **--env-add &lt;nombre de la variable de entorno&gt;=&lt;valor de la variable de entorno&gt;:** agrega o actualiza el valor de una o varias variables de entorno.
- **--image &lt;nombre o id de la imagen&gt;:** cambia en tiempo de ejecución la imagen que ejecutan los contenedores de un servicio.

<br>

### Inspeccionar Los Logs De Un Servicio

```unknown
docker service logs <parámetros> <id o nombre del servicio|id o nombre de la tarea>
```

muestra los logs de los de un servicio o tarea, algunos de los parámetros más útiles al visualizar los logs de un servicio o tarea con **docker service logs** son:

- **--follow:** permite hacer follow de los logs del servicio o tarea, es decir que se liga la consola de la máquina anfitrión a los logs para verlos en la medida en la que se imprimen.

<br>

### Escalar Un Servicio

```unknown
docker service scale <parámetros> <id o nombre del servicio>=<número de réplicas>
```

permite escalar uno o varios servicios estableciendo el número de réplicas necesarias por cada servicio.

<br>

### Restaurar Un Servicio A Su Estado Anterior

```unknown
docker service rollback <parámetros> <id o nombre del servicio>
```

permite restaurar un servicio a su estado anterior.

<br>

### Eliminar Un Servicio

```unknown
docker service rm <id o nombre del servicio>
```

elimina un servicio junto con todos sus contenedores y tareas.

<br>

## Administración De Redes De Docker Swarm

al utilizar docker en modo swarm docker necesita dos tipos de redes adicionales a las que se usan normalmente, las cuales se usan para comunicar las diferentes tareas o contenedores de un servicio a nivel de nodo y cluster, estas redes son: **docker_gwbridge** e **ingress**, la red docker_gwbrigde por su parte se encarga de comunicar los contenedores del nodo entre ellos y la red ingress, ingress por su parte se encarga de la comunicación de todas las redes docker_gwbrigde a través de todos los nodos del cluster, formando así una red que comunica todos los contenedores de un servicio cuyos contenedores están distribuidos en diferentes nodos, también se diferencian en el alcance y driver, docker_gwbridge está disponible sólo dentro de un nodo y utiliza un driver **bridge** estándar, mientras que ingress está disponible en todos los nodos y utiliza un driver **overlay**, al crear un cluster basado en docker swarm las redes docker_gwbridge se crean automáticamente y se conectan a ingress (que es una red creada por defecto), pero también es posible crear redes con funcionalidades similares a la red ingress a las cuales conectar varios servicios para lograr comunicación entre los contenedores de diferentes servicios sin sobrecargar ingress, esto se logra simplemente creando una red con un driver **overlay**.

<br>

### Crear Una Red Overlay

```unknown
docker network create --driver overlay <nombre de la red>
```

crea una red con un driver overlay la cual tiene conectividad con todo el cluster y funciona de forma similar a la red ingress, por lo que uno o varios servicios se pueden conectar a la nueva red.

<br>
