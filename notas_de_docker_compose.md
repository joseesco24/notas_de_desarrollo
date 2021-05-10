# Notas De Docker Compose

- [Introducción](#introducción)
- [Instalación De Docker Compose En Ubuntu](#instalación-de-docker-compose-en-ubuntu)
- [Archivos Docker Compose](#archivos-docker-compose)
  - [Tips De Docker Compose](#tips-de-docker-compose)
  - [Ejemplo De Un Docker Compose Con Dos Servicios Y Volúmenes](#ejemplo-de-un-docker-compose-con-dos-servicios-y-volúmenes)
  - [Ejemplo De Un Docker Compose Con Dos Servicios Y Un Bind Mount](#ejemplo-de-un-docker-compose-con-dos-servicios-y-un-bind-mount)
  - [Ejemplo De Un Docker Compose Override](#ejemplo-de-un-docker-compose-override)
- [Subcomandos De Docker Compose](#subcomandos-de-docker-compose)
  - [Comandos De Administración General De Una Aplicación Compose](#comandos-de-administración-general-de-una-aplicación-compose)
  - [Construir Las Imágenes Necesarias Para Una Aplicación Compose](#construir-las-imágenes-necesarias-para-una-aplicación-compose)
  - [Iniciar Una Aplicación Compose](#iniciar-una-aplicación-compose)
  - [Revisar El Estado De Los Contenedores Generados Por Una Aplicación Compose](#revisar-el-estado-de-los-contenedores-generados-por-una-aplicación-compose)
  - [Revisar Los Logs De Una Aplicación Compose](#revisar-los-logs-de-una-aplicación-compose)
  - [Ejecutar Comandos En Servicios De Una Aplicación Compose](#ejecutar-comandos-en-servicios-de-una-aplicación-compose)
  - [Detener Y Eliminar Todos Los Servicios De Una Aplicación Compose](#detener-y-eliminar-todos-los-servicios-de-una-aplicación-compose)

<br>

## Introducción

[**docker compose**](https://docs.docker.com/compose/) permite usar los 4 recursos principales de docker juntos fácilmente desde un solo archivo [**docker-compose.yml**](https://docs.docker.com/compose/compose-file/), usando este archivo también llamado compose file se pueden integrar fácilmente recursos de red, volúmenes, imagenes y contenedores sin necesidad de administrar uno a uno cada tipo de recurso, en síntesis lo que permite docker compose es describir de forma declarativa la arquitectura de servicios que la aplicación necesita, y docker se encargará de crear e integrar cada recursos declarado por detrás evitando que el desarrollador tenga que administraba uno a uno los recursos necesarios para levantar una aplicación basada en varios servicios contenerizados que interactúan entre sí.\
docker compose se basa en servicios, no en contenedores, un servicio en docker puede componerse de una o más aplicaciones contenerizadas creadas a partir de la misma imagen, es decir que pueden haber varias réplicas de un contenedor en un mismo servicio, en un esquema de servicios con réplicas además se distribuyen las diferentes peticiones entre las réplicas de la aplicación, lo que permite que la aplicación se más ágil atendiendo peticiones y además pueda atender más en simultáneo al mismo tiempo que aprovecha los recursos disponibles a nivel de hardware, en docker compose se manejan servicios en lugar de contenedores para así dar a los desarrolladores la posibilidad de escalar fácilmente el número de contenedores que realizan la misma tarea.

<br>

## Instalación De Docker Compose En Ubuntu

docker compose se instala junto a las versiones de escritorio de windows o mac, sin embargo, en la versión de ubuntu es necesario instalarlo manualmente con los siguientes comandos, los cuales son extraídos de la guia oficial de [**docker hub**](https://docs.docker.com/compose/install/):

```bash
sudo curl -l "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

<br>

## Archivos Docker Compose

algunos de los componentes que soporta docker compose en los archivos **docker-compose.yml** y sus funciones son:

- **version:** indica la versión del compose file, dependiendo de la versión de docker engine se soportan ciertas características y ciertas versiones de compose file.
- **services:** indica que servicios componen la aplicación, básicamente son las partes o componentes que interactúan entre sí o trabajan en simultáneo para formar una aplicación, un servicio no es un contenedor explícitamente ya que un servicio puede componerse de uno o muchos contenedores.
- **image:** establece la imagen que se va a utilizar para ejecutar los contenedores de cierto servicio.
- **environment:** permite definir variables de ambiente a las que pueden acceder los contenedores de un servicio.
- **depends_on:** establece las dependencias entre servicios, si un servicio declara dependencia de otro este no deberá ejecutarse si antes no se ejecuta el o los servicios de los que depende.
- **ports:** bindea un puerto o un rango de puertos de la máquina anfitrión con un puerto de uno o varios contenedores.
- **volumes:** indica los volúmenes y bind mounts de un servicio.
- **command:** cambia el comando o los argumentos del proceso principal por defecto de los contenedores de un servicio.
- **build:** indica el contexto con el que se debe construir una nueva imagen que se desplegará en todos los contenedores del servicio indicado, el nombre de la nueva imagen se construye en base al nombre del directorio de trabajo y el nombre del servicio en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_&lt;nombre del servicio&gt;**.
- **networks:** indica las redes a las que se deben conectar los contenedores de un servicio.

los archivos **docker-compose.yml** son sumamente sensibles a la indentación con la que se declara cada uno de sus componentes, por lo que es necesario tener especial cuidado con la indentación cuando se declaran esquemas de servicios basados en compose file.

<br>

### Tips De Docker Compose

- al usar docker compose docker por detrás crea una red dedicada a esa arquitectura a la que conecta todos los contenedores de todos los servicios declarados, el nombre de la red se asigna en base al nombre del directorio de trabajo en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_default**.
- al usar docker compose docker por detras trata de asignar nombres únicos a cada contenedor para evitar conflictos a causa de los nombres, los nombres de los contenedores se asigna en base del nombre del directorio de trabajo, el nombre del servicio y un número que diferencia los diferentes contenedores de un servicio en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_&lt;nombre del servicio&gt;\_&lt;número de contenedor&gt;**.
- al usar docker compose docker por detrás se asegura que a pesar de los nuevos nombres asignados a los contenedores estos sigan siendo alcanzables por los demás contenedores solo con el nombre del servicio que ejecutan.
- junto a **docker-compose.yml** se puede utilizar **docker-compose.override.yml**, la ventaja de utilizar docker compose.override es que se puede personalizar el compose file sin cambiarlo directamente, lo que evita alterar el compose file de producción pero nos permite probar pequeños cambios en él sin alterarlo directamente, además docker por defecto trata de unir y conservar las definiciones de ambos archivos.
- las variables de entorno son sencillas de manejar con los archivos **compose** y **compose.override** ya que simplemente se unen las definiciones de ambas y en caso de redefinición en **compose.override** simplemente se sobreescribe el valor de la variable.
- para el manejo de los puertos lo recomendable es no utilizar definiciones de puertos fuera de **compose** y en caso de hacerse la definición de los puertos debe estar solo en un archivo.
- las dependencias de servicios se usan siempre desde el **compose.override**.
- para usar un **compose.override** solo hace falta construir la imagen de forma normal, docker por defecto detecta el archivo de sobre escritura y lo utiliza.
- al poner **image** y **build** en un mismo compose la imagen se construye pero se le asigna el nombre de imagen en lugar del nombre por defecto.

<br>

### Ejemplo De Un Docker Compose Con Dos Servicios Y Volúmenes

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      mongo_url: "mongodb://db:27017/test"
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

el compose anterior utiliza un volumen en app, además de una variable de ambiente, un puerto vinculado, un cambio en el comando por defecto y construye una imagen para los contenedores del servicio app.

<br>

### Ejemplo De Un Docker Compose Con Dos Servicios Y Un Bind Mount

```yml
version: "3.8"

services:
  app:
    image: alpine
    environment:
      mongo_url: "mongodb://db:27017/test"
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

el compose anterior utiliza un bind mount, indica una ruta que no debe ser alterada por el bind, además, utiliza una variable de ambiente y un rango de puertos del anfitrión que pueden ser vinculados a los contenedores del servicio app.

<br>

### Ejemplo De Un Docker Compose Override

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      nueva_variable: "mongodb://db:27017/test"
```

al declarar un **docker-compose.override.yml** como el anterior junto a cualquiera de los **docker-compose.yml** se logra que se construya la imagen y se agregue la variable de ambiente nueva a la imagen.

<br>

## Subcomandos De Docker Compose

docker compose tiene varios subcomandos similares a los usados en la administración regular de docker, algunos de los más relevantes para utilizar aplicaciones basadas en docker compose son:

<br>

### Comandos De Administración General De Una Aplicación Compose

```unknown
docker-compose <comando> --help
```

muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Construir Las Imágenes Necesarias Para Una Aplicación Compose

```unknown
docker-compose build <parámetros> <nombre del servicio>
```

construye las imágenes que requieren ser construidas según el compose file, al especificarse uno o varios servicios solo se construirán las imágenes de los servicios indicados.

<br>

### Iniciar Una Aplicación Compose

```unknown
docker-compose up <parámetros> <nombre del servicio>
```

levanta la arquitectura descrita por el compose file en caso de no indicarse un servicio en concreto, si se indica un servicio solo ese servicio será ejecutado, algunos de los parámetros más útiles al utilizar **docker-compose up** para levantar una arquitectura son:

- **--detach:** evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su id para poder manipularlo posteriormente en caso de que haga falta.
- **--scale &lt;nombre o id del servicio&gt;=&lt;número de contenedores&gt;:** escala un determinado servicio al número de contenedores indicado.

<br>

### Revisar El Estado De Los Contenedores Generados Por Una Aplicación Compose

```unknown
docker-compose ps <parámetros> <nombre del servicio>
```

muestra el estado de los contenedores creados por el compose file en caso de no indicarse un servicio en concreto, si se indica un servicio solo se mostrará el estado de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose ps** para ver el estado de los contenedores pertenecientes a una arquitectura son:

- **--all:** muestra todos los contenedores de la aplicación independientemente de si están o no ejecutados.

<br>

### Revisar Los Logs De Una Aplicación Compose

```unknown
docker-compose logs <parámetros> <nombre del servicio>
```

muestra los logs de todos los contenedores usados por la aplicación en caso de no indicarse un servicio en concreto, si se indica un servicio sólo se mostrarán solo los logs de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose logs** para ver los logs de una arquitectura son:

- **--follow:** sirve para hacer follow a los logs de toda la aplicación o de cierto servicio si se indica el servicio.
- **--tail &lt;número de logs&gt;:** imprime los últimos logs limitándose al número de logs indicado de toda la aplicación o de cierto servicio si se indica el servicio.

<br>

### Ejecutar Comandos En Servicios De Una Aplicación Compose

```unknown
docker-compose exec <parámetros> <nombre del servicio> <comando>
```

ejecuta un comando dentro del o los contenedores pertenecientes a un servicio de una aplicación compose.

<br>

### Detener Y Eliminar Todos Los Servicios De Una Aplicación Compose

```unknown
docker-compose down <parámetros>
```

detiene y elimina todos los recursos usados por una aplicación compose.

<br>
