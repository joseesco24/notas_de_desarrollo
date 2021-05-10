# Notas De Docker Stacks

- [Introducción](#introducción)
- [Archivos Stack File](#archivos-stack-file)
  - [Tips De Docker Stacks](#tips-de-docker-stacks)
  - [Ejemplo De Un Stack File](#ejemplo-de-un-stack-file)
- [Subcomandos De Docker Stacks](#subcomandos-de-docker-stacks)
  - [Inspeccionar Comandos De Administración De Stacks](#inspeccionar-comandos-de-administración-de-stacks)
  - [Iniciar O Actualizar Un Stack](#iniciar-o-actualizar-un-stack)
  - [Listar Stacks](#listar-stacks)
  - [Listar Tareas De Un Stack](#listar-tareas-de-un-stack)
  - [Listar Servicios De Un Stack](#listar-servicios-de-un-stack)
  - [Eliminar Stacks](#eliminar-stacks)

<br>

## Introducción

[**docker stack**](https://docs.docker.com/engine/reference/commandline/stack/) es la solucion que da docker a situaciones en las que se se quieren desplegar varias aplicaciones como servicios en un cluster basado en docker swarm sin configurar cada servicio uno a uno. al igual que docker compose, docker stack permite que se integren los 4 recursos principales de docker en una sola aplicacion basada en varios servicios que se pueden comunicar o no entre si y ademas se ejecutan sobre un cluster, todo usando un archivo llamado [**stack-file.yml**](https://docs.docker.com/compose/compose-file/), estos archivos son en realidad compose files "enriquecidos", utilizan la misma sintaxis y los mismos componentes de un compose file normal, por lo que permiten declarar de forma declarativa la arquitectura de servicios que la aplicación necesita y por detrás docker se encargará de e integrar cada recurso, pero los stack file utilizan configuraciones adicionales a las de los compose file dedicadas a los [**stacks**](https://docs.docker.com/compose/compose-file/compose-file-v3/#deploy), la principal diferencia es que los stack file sirven para generar esquemas de servicios basados en docker swarm sobre más de una máquina en un cluster, a diferencia de los compose file, que cumplen la misma función, pero solo en una máquina, los stack file además soportan componentes que docker compose ignora y de la misma forma los compose files regulares utilizan ciertos componentes que los stack files ignoran.

<br>

## Archivos Stack File

algunos de los componentes adicionales que soporta docker stack en los archivos **stack-file.yml** respecto a docker compose y sus funciones son:

- **delpoy:** establece la sección de las configuraciones del compose file que corresponde al despliegue de un stack, todas las demás configuraciones dirigidas al stack tiene que estar debajo de esta etiqueta.
- **placement:** establece las restricciones del despliegue de las tareas del servicio.
- **réplicas:** establece el número de tareas replicadas para ese servicio.

<br>

### Tips De Docker Stacks

- los stacks a diferencia de compose son agrupaciones de servicios, en lugar de ser objetos propios de docker como en compose, donde cada compose es un objeto de docker.
- al tener desplegados varios servicios con uno o varios stacks sobre un cluster se debe utilizar un servicio de reverse proxy como [**traefik**](https://traefik.io/) para lograr que usando un solo dominio se puedan redireccionar todas las peticiones a los diferentes servicios disponibles en el cluster, para esto, además, es necesario es que el servicio de reverse proxy este contenerizado, desplegado sobre un manager y que esté en la misma red de los servicios a los que debe redireccionar las peticiones, además para balancear la carga entre los servicios traefik necesita un socket daemon para ver los eventos de docker swarm, por lo que debemos compartir la ruta usando un bind (--mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock) y adicionalmente al ser un proxy http público debe exponerse en el puerto 80.
- la principal diferencia entre un stack y un servicio es que un stack está por encima de un servicio, de tal modo que al igual que un servicio tiene tareas un stack puede tener diferentes servicios.

<br>

### Ejemplo De Un Stack File

```yml
version: "3"

services:
  app:
    image: alpine
    environment:
      mongo_url: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    deploy:
      replicas: 6
      placement:
        constraints: [node.role==worker]

  db:
    image: mongo
```

<br>

## Subcomandos De Docker Stacks

para utilizar stack files como origen de una arquitectura basada en docker swarm hay varios subcomandos similares a los usados en la administración regular de docker swarm y docker compose, algunos de los más relevantes para utilizar aplicaciones basadas en docker swarm con stack files son:

<br>

### Inspeccionar Comandos De Administración De Stacks

```unknown
docker stack <comando> --help
```

muestra a grandes rasgos los comandos disponibles para administrar docker stacks y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Iniciar O Actualizar Un Stack

```unknown
docker stack deploy <parámetros> <nombre del nuevo stack>
```

inicia o actualiza un stack, algunos de los parámetros más útiles al utilizar **docker stack deploy** para iniciar un stack son:

- **--compose-file &lt;ruta al stack file&gt;:** establece el compose file que se utilizará para generar el nuevo stack.
- **--orchestrator &lt;swarm|kubernetes|all&gt;:** establece el orquestador del stack, por defecto se usa swarm.

<br>

### Listar Stacks

```unknown
docker stack ls <parámetros>
```

<br>

### Listar Tareas De Un Stack

```unknown
docker stack ps <parámetros> <nombre del stack>
```

lista todas las tareas pertenecientes a un stack.

<br>

### Listar Servicios De Un Stack

```unknown
docker stack services <parámetros> <nombre del stack>
```

lista todos los servicios pertenecientes a un stack.

<br>

### Eliminar Stacks

```unknown
docker stack rm <parámetros> <nombre del stack>
```

elimina un stack junto con todas sus tareas, contenedores, redes y volúmenes.

<br>
