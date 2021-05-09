# Notas de Docker Compose

[**Docker Compose**](https://docs.docker.com/compose/) permite usar los 4 recursos principales de Docker juntos fácilmente desde un solo archivo [**docker-compose.yml**](https://docs.docker.com/compose/compose-file/), usando este archivo también llamado Compose File se pueden integrar fácilmente recursos de red, volúmenes, imagenes y contenedores sin necesidad de administrar uno a uno cada tipo de recurso, en síntesis lo que permite Docker Compose es describir de forma declarativa la arquitectura de servicios que la aplicación necesita, y Docker se encargará de crear e integrar cada recursos declarado por detrás evitando que el desarrollador tenga que administraba uno a uno los recursos necesarios para levantar una aplicación basada en varios servicios contenerizados que interactúan entre sí.\
Docker Compose se basa en servicios, no en contenedores, un servicio en Docker puede componerse de una o más aplicaciones contenerizadas creadas a partir de la misma imagen, es decir que pueden haber varias réplicas de un contenedor en un mismo servicio, en un esquema de servicios con réplicas además se distribuyen las diferentes peticiones entre las réplicas de la aplicación, lo que permite que la aplicación se más ágil atendiendo peticiones y además pueda atender más en simultáneo al mismo tiempo que aprovecha los recursos disponibles a nivel de hardware, en Docker compose se manejan servicios en lugar de contenedores para así dar a los desarrolladores la posibilidad de escalar fácilmente el número de contenedores que realizan la misma tarea.

<br>

- [Instalación de Docker Compose en Ubuntu](#instalación-de-docker-compose-en-ubuntu)
- [Archivos docker-compose.yml](#archivos-docker-composeyml)
  - [Tips de Docker Compose](#tips-de-docker-compose)
  - [Ejemplo de un Docker Compose con dos servicios y volúmenes](#ejemplo-de-un-docker-compose-con-dos-servicios-y-volúmenes)
  - [Ejemplo de un Docker Compose con dos servicios y un bind mount](#ejemplo-de-un-docker-compose-con-dos-servicios-y-un-bind-mount)
  - [Ejemplo de un docker-compose.override](#ejemplo-de-un-docker-composeoverride)
- [Subcomandos de Docker Compose](#subcomandos-de-docker-compose)
  - [Comandos de administración general de una aplicación compose](#comandos-de-administración-general-de-una-aplicación-compose)
  - [Construir las imágenes necesarias para una aplicación compose](#construir-las-imágenes-necesarias-para-una-aplicación-compose)
  - [Iniciar una aplicación compose](#iniciar-una-aplicación-compose)
  - [Revisar el estado de los contenedores generados por una aplicación compose](#revisar-el-estado-de-los-contenedores-generados-por-una-aplicación-compose)
  - [Revisar los logs de una aplicación compose](#revisar-los-logs-de-una-aplicación-compose)
  - [Ejecutar comandos en servicios de una aplicación compose](#ejecutar-comandos-en-servicios-de-una-aplicación-compose)
  - [Detener y eliminar todos los servicios de una aplicación compose](#detener-y-eliminar-todos-los-servicios-de-una-aplicación-compose)

<br>

## Instalación de Docker Compose en Ubuntu

Docker Compose se instala junto a las versiones de escritorio de Windows o Mac, sin embargo, en la versión de Ubuntu es necesario instalarlo manualmente con los siguientes comandos, los cuales son extraídos de la guia oficial de [**Docker Hub**](https://docs.docker.com/compose/install/):

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

<br>

## Archivos docker-compose.yml

Algunos de los componentes que soporta Docker Compose en los archivos **docker-compose.yml** y sus funciones son:

- **version:** Indica la versión del Compose File, dependiendo de la versión de Docker Engine se soportan ciertas características y ciertas versiones de Compose File.
- **services:** Indica que servicios componen la aplicación, básicamente son las partes o componentes que interactúan entre sí o trabajan en simultáneo para formar una aplicación, un servicio no es un contenedor explícitamente ya que un servicio puede componerse de uno o muchos contenedores.
- **image:** Establece la imagen que se va a utilizar para ejecutar los contenedores de cierto servicio.
- **environment:** Permite definir variables de ambiente a las que pueden acceder los contenedores de un servicio.
- **depends_on:** Establece las dependencias entre servicios, si un servicio declara dependencia de otro este no deberá ejecutarse si antes no se ejecuta el o los servicios de los que depende.
- **ports:** Bindea un puerto o un rango de puertos de la máquina anfitrión con un puerto de uno o varios contenedores.
- **volumes:** Indica los volúmenes y bind mounts de un servicio.
- **command:** Cambia el comando o los argumentos del proceso principal por defecto de los contenedores de un servicio.
- **build:** Indica el contexto con el que se debe construir una nueva imagen que se desplegará en todos los contenedores del servicio indicado, el nombre de la nueva imagen se construye en base al nombre del directorio de trabajo y el nombre del servicio en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_&lt;nombre del servicio&gt;**.
- **networks:** Indica las redes a las que se deben conectar los contenedores de un servicio.

Los archivos **docker-compose.yml** son sumamente sensibles a la indentación con la que se declara cada uno de sus componentes, por lo que es necesario tener especial cuidado con la indentación cuando se declaran esquemas de servicios basados en Compose File.

<br>

### Tips de Docker Compose

- Al usar Docker Compose Docker por detrás crea una red dedicada a esa arquitectura a la que conecta todos los contenedores de todos los servicios declarados, el nombre de la red se asigna en base al nombre del directorio de trabajo en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_default**.
- Al usar Docker Compose Docker por detras trata de asignar nombres únicos a cada contenedor para evitar conflictos a causa de los nombres, los nombres de los contenedores se asigna en base del nombre del directorio de trabajo, el nombre del servicio y un número que diferencia los diferentes contenedores de un servicio en el siguiente formato **&lt;nombre del directorio de trabajo&gt;\_&lt;nombre del servicio&gt;\_&lt;número de contenedor&gt;**.
- Al usar Docker Compose Docker por detrás se asegura que a pesar de los nuevos nombres asignados a los contenedores estos sigan siendo alcanzables por los demás contenedores solo con el nombre del servicio que ejecutan.
- Junto a **docker-compose.yml** se puede utilizar **docker-compose.override.yml**, la ventaja de utilizar Docker Compose.override es que se puede personalizar el Compose File sin cambiarlo directamente, lo que evita alterar el Compose File de producción pero nos permite probar pequeños cambios en él sin alterarlo directamente, además Docker por defecto trata de unir y conservar las definiciones de ambos archivos.
- Las variables de entorno son sencillas de manejar con los archivos **compose** y **compose.override** ya que simplemente se unen las definiciones de ambas y en caso de redefinición en **compose.override** simplemente se sobreescribe el valor de la variable.
- Para el manejo de los puertos lo recomendable es no utilizar definiciones de puertos fuera de **compose** y en caso de hacerse la definición de los puertos debe estar solo en un archivo.
- Las dependencias de servicios se usan siempre desde el **compose.override**.
- Para usar un **compose.override** solo hace falta construir la imagen de forma normal, Docker por defecto detecta el archivo de sobre escritura y lo utiliza.
- Al poner **image** y **build** en un mismo compose la imagen se construye pero se le asigna el nombre de imagen en lugar del nombre por defecto.

<br>

### Ejemplo de un Docker Compose con dos servicios y volúmenes

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

<br>

### Ejemplo de un Docker Compose con dos servicios y un bind mount

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

<br>

### Ejemplo de un docker-compose.override

```yml
version: "3.8"

services:
  app:
    build: .
    environment:
      NUEVA_VARIABLE: "mongodb://db:27017/test"
```

Al declarar un **docker-compose.override.yml** como el anterior junto a cualquiera de los **docker-compose.yml** se logra que se construya la imagen y se agregue la variable de ambiente nueva a la imagen.

<br>

## Subcomandos de Docker Compose

Docker Compose tiene varios subcomandos similares a los usados en la administración regular de Docker, algunos de los más relevantes para utilizar aplicaciones basadas en Docker Compose son:

<br>

### Comandos de administración general de una aplicación compose

```unknown
docker-compose <comando> --help
```

Muestra a grandes rasgos los comandos disponibles y sus usos al no especificar un comando en concreto, al especificar un comando se puede profundizar más en el uso del comando y los parámetros adicionales que acepta para alterar su funcionamiento.

<br>

### Construir las imágenes necesarias para una aplicación compose

```unknown
docker-compose build <parámetros> <nombre del servicio>
```

Construye las imágenes que requieren ser construidas según el Compose File, al especificarse uno o varios servicios solo se construirán las imágenes de los servicios indicados.

<br>

### Iniciar una aplicación compose

```unknown
docker-compose up <parámetros> <nombre del servicio>
```

Levanta la arquitectura descrita por el Compose File en caso de no indicarse un servicio en concreto, si se indica un servicio solo ese servicio será ejecutado, algunos de los parámetros más útiles al utilizar **docker-compose up** para levantar una arquitectura son:

- **--detach:** Evita que la terminal del anfitrión quede atada a la ejecución del contenedor ejecutando en background e imprimiendo su ID para poder manipularlo posteriormente en caso de que haga falta.
- **--scale &lt;nombre o id del servicio&gt;=&lt;número de contenedores&gt;:** Escala un determinado servicio al número de contenedores indicado.

<br>

### Revisar el estado de los contenedores generados por una aplicación compose

```unknown
docker-compose ps <parámetros> <nombre del servicio>
```

Muestra el estado de los contenedores creados por el Compose File en caso de no indicarse un servicio en concreto, si se indica un servicio solo se mostrará el estado de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose ps** para ver el estado de los contenedores pertenecientes a una arquitectura son:

- **--all:** Muestra todos los contenedores de la aplicación independientemente de si están o no ejecutados.

<br>

### Revisar los logs de una aplicación compose

```unknown
docker-compose logs <parámetros> <nombre del servicio>
```

Muestra los logs de todos los contenedores usados por la aplicación en caso de no indicarse un servicio en concreto, si se indica un servicio sólo se mostrarán solo los logs de los contenedores pertenecientes a ese servicio, algunos de los parámetros más útiles al utilizar **docker-compose logs** para ver los logs de una arquitectura son:

- **--follow:** Sirve para hacer follow a los logs de toda la aplicación o de cierto servicio si se indica el servicio.
- **--tail &lt;número de logs&gt;:** Imprime los últimos logs limitándose al número de logs indicado de toda la aplicación o de cierto servicio si se indica el servicio.

<br>

### Ejecutar comandos en servicios de una aplicación compose

```unknown
docker-compose exec <parámetros> <nombre del servicio> <comando>
```

Ejecuta un comando dentro del o los contenedores pertenecientes a un servicio de una aplicación compose.

<br>

### Detener y eliminar todos los servicios de una aplicación compose

```unknown
docker-compose down <parámetros>
```

Detiene y elimina todos los recursos usados por una aplicación compose.

<br>
