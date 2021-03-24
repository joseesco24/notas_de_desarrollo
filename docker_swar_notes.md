# Docker Swarm

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
