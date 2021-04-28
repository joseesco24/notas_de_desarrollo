# MongoDB

[**MongoDB**](https://www.mongodb.com/2) es el motor base de datos no relacionales basado en documentos más usada en entornos de desarrollo profesionales, MongoDB es ampliamente usado como motor de base de datos gracias a su flexibilidad y facilidad de uso, la cual se debe a que cada documento dentro de MongoDB es almacenado como un documento BSON, que es la representación binaria de un documento JSON. MongoDB además permite almacenar documentos de forma distribuida, por lo que usando MongoDB como motor de bases de datos es totalmente factible tener un cluster de servidores dedicados al almacenamiento de los datos de una o varias bases de datos, esta característica además hace que escalar una base de datos MongoDB sea extremadamente fácil ya que solo hace falta agregar más nodos al cluster de MongoDB. Una de las mejores características de MongoDB es que es "Schema Less" por lo que los documentos dentro de una misma colección pueden tener estructuras totalmente diferentes sin afectar el funcionamiento de MongoDB y como si fuera poco las consultas de MongoDB también son extremadamente eficientes por el hecho de ser una base de datos no relacional basada en documentos, los componentes más importantes de MongoDB se listan a continuación.

- **Cluster:** En MongoDB un cluster es una agrupación de maquinas que comparten el acceso a las diferentes bases de datos.
- **Bases de datos:** Las bases de datos en MongoDB son espacios de almacenamiento en los que se guardan colecciones, cada base de datos tiene su propio archivo dentro del sistema de archivos de la máquina en la que se ejecuta el MongoDB Server y además en un cluster de MongoDB pueden haber múltiples bases de datos.
- **Colecciones:** Las colecciones en MongoDB son agrupaciones de documentos, son equivalentes a las tablas de las bases de datos relacionales y además no imponen un esquema.
- **Documentos:** Los documentos dentro de MongoDB son registros dentro de cada colección, son análogos a los documentos JSON, pero en realidad son BSON, que son la transformación a binario de un JSON, por lo que en un documento se pueden almacenar más tipos de datos y además son la unidad más Básica dentro de MongoDB.

Otra de las razones para que MongoDB sea tan usado como motor de base de datos es su ecosistema, el ecosistema de MongoDB se divide en varias partes las cuales se describen a continuación:

<p align="center">
<img src="imagenes/notas_de_mongodb/ecosistema_mongodb.png" width="74%" height="auto"/>
</p>

- **MongoDB Server:** Es el motor de base de datos como tal, por lo que es donde se guardan los datos, además el MongoDB Server tiene tres versiones.

  - Atlas: Es la versión en nube de una base de datos con MongoDB.
  - Community: Es la versión de código abierto de MongoDB.
  - Enterprise: Es la versión de pago de MongoDB.

- **MongoDB Shell:** Es la consola con la que se interactúa con el MongoDB Server.
- **MongoDB Compass:** Es una interfaz gráfica con la que se puede interactuar con el MongoDB Server.
- **Conectores:** Son las librerías dentro de cada lenguaje que se usan para interactuar con el MongoDB Server.
- **MongoDB Realm:** Es una versión lite de MongoDB que se puede instalar en dispositivos móviles.

<br>

## MongoDB shell

El shell de MongoDB o [**MongoDB shell**](https://docs.mongodb.com/manual/mongo/) es la forma mas sencilla de interactuar con el MongoDB Server, además de poder realizar acciones simples también se pueden crear script para MongoDB shell, por lo que se pueden automatizar varios tipos de tareas o consultas en concreto.

<br>

### Iniciar shell

```bash
mongo
```

<br>

### Limpiar shell

```bash
ctrl + l
```

<br>

### Ver bases de datos disponibles

```bash
show dbs
```

<br>

### Crear nueva base de datos

```bash
use [nombre de la nueva base de datos]
```

<br>

### Ver nombre de la base de datos a la que esta conectado el shell

```bash
db
```

<br>

### Ver collecciones disponibles en la base de datos

```bash
show collections
```

<br>
