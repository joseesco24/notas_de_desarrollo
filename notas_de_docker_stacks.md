# Notas de Docker Stacks

[**Docker Stack**](https://docs.docker.com/engine/reference/commandline/stack/) es la solucion que da Docker a situaciones en las que se se quieren desplegar varias aplicaciones como servicios en un cluster basado en Docker Swarm, sin configurar cada servicio uno a uno, al igual que Docker Compose, Docker Stack permite que se integren los 4 recursos principales de Docker en una sola aplicacion basada en varios servicios que se pueden comunicar o no entre si y ademas se ejecutan sobre un cluster, todo usando un archivo llamado [**stack-file.yml**](https://docs.docker.com/compose/compose-file/), estos archivos son en realidad Compose Files "enriquecidos", utilizan la misma sintaxis y los mismos componentes de un Compose File normal, por lo que permiten describir de forma declarativa la arquitectura de servicios que la aplicación necesita y por detrás Docker se encargará de e integrar cada recurso, pero los Stack File utilizan configuraciones adicionales a las de los Compose File dedicadas a los [**Stacks**](https://docs.docker.com/compose/compose-file/compose-file-v3/#deploy), la principal diferencia es que los Stack File sirven para generar esquemas de servicios basados en Docker Swarm sobre más de una máquina en un cluster, a diferencia de los Compose File, que cumplen la misma función, pero solo en una máquina, los Stack File además soportan componentes que Docker Compose ignora y de la misma forma los Compose Files regulares utilizan ciertos componentes que los Stack Files ignoran.

## Archivos stack-file.yml

Algunos de los componentes adicionales que soporta Docker Stack en los archivos **stack-file.yml** respecto a Docker Compose y sus funciones son:

- **delpoy:** Establece la sección de las configuraciones del Compose File que corresponde al despliegue de un stack, todas las demás configuraciones dirigidas al stack tiene que estar debajo de esta etiqueta.
- **placement:** Establece las restricciones del despliegue de las tareas del servicio.
- **réplicas:** Establece el número de tareas replicadas para ese servicio.

### Tips de Docker Stacks

- Los stacks a diferencia de Compose son agrupaciones de servicios, en lugar de ser objetos propios de Docker como en Compose, donde cada Compose es un objeto de Docker.
- Al tener desplegados varios servicios con uno o varios stacks sobre un cluster se debe utilizar un servicio de reverse proxy como [**traefik**](https://traefik.io/) para lograr que usando un solo dominio se puedan redireccionar todas las peticiones a los diferentes servicios disponibles en el cluster, para esto, además, es necesario es que el servicio de reverse proxy este contenerizado, desplegado sobre un manager y que esté en la misma red de los servicios a los que debe redireccionar las peticiones, además para balancear la carga entre los servicios traefik necesita un socket daemon para ver los eventos de Docker Swarm, por lo que debemos compartir la ruta usando un bind (--mount type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock) y adicionalmente al ser un proxy http público debe exponerse en el puerto 80.
- La principal diferencia entre un stack y un servicio es que un stack está por encima de un servicio, de tal modo que al igual que un servicio tiene tareas un stack puede tener diferentes servicios.

#### Ejemplo de un Stack File

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
      replicas: 6
      placement:
        constraints: [node.role==worker]

  db:
    image: mongo
```

## Subcomandos de Docker Stacks

Para utilizar Stack Files como origen de una arquitectura basada en Docker Swarm hay varios subcomandos similares a los usados en la administración regular de Docker Swarm y Docker Compose, algunos de los más relevantes para utilizar aplicaciones basadas en Docker Swarm con Stack Files son:

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

- **--compose-file [ruta al Stack File]:** Establece el Compose File que se utilizará para generar el nuevo stack.
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
