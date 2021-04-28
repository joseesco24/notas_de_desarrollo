# MongoDB

[**MongoDB**](https://www.mongodb.com/2) es el motor base de datos no relacionales basado en documentos más usada en entornos de desarrollo profesionales, MongoDB es ampliamente usado como motor de base de datos gracias a su flexibilidad y facilidad de uso, la cual se debe a que cada documento dentro de MongoDB es almacenado como un documento BSON, que es la representación binaria de un documento JSON. MongoDB además permite almacenar documentos de forma distribuida, por lo que usando MongoDB como motor de bases de datos es totalmente factible tener un cluster de servidores dedicados al almacenamiento de los datos de una o varias bases de datos, esta característica además hace que escalar una base de datos MongoDB sea extremadamente fácil ya que solo hace falta agregar más nodos al cluster de MongoDB. Una de las mejores características de MongoDB es que es "Schema Less" por lo que los documentos dentro de una misma colección pueden tener estructuras totalmente diferentes sin afectar el funcionamiento de MongoDB y como si fuera poco las consultas de MongoDB también son extremadamente eficientes por el hecho de ser una base de datos no relacional basada en documentos, los componentes más importantes de MongoDB se listan a continuación.

- **Cluster:** En MongoDB un cluster es una agrupación de máquinas que comparten el acceso a las diferentes bases de datos.
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

### Crear nueva base de datos o usar una ya creada

```bash
use [nombre de la nueva base de datos]
```

<br>

### Ver nombre de la base de datos a la que está conectado el shell

```bash
db
```

<br>

### Ver colecciones disponibles en la base de datos

```bash
show collections
```

<br>

### Ver comandos disponibles en una colección

```bash
[nombre de la base de datos].[nombre de la colección].help()
```

Ejemplo:

```bash
db.inventory.help()
```

<br>

### Insertar un documento en una colección

```bash
[nombre de la base de datos].[nombre de la colección].insertOne([documento en formato JSON])
```

Ejemplo:

```bash
db.inventory.insertOne({
    size: {h: 28, w: 35.5, uom: "cm"},
    tags: ["cotton"],
    item: "canvas",
    qty: 100,
})
```

MongoDB por defecto no crea bases de datos vacías, por lo que es necesario luego de crear una nueva base de datos crear al menos una colección y un documento, si la colección en la que se quiere insertar el documento no existe MongoDB crea una nueva colección con el nombre indicado.\
Al insertar un documento el id se puede especificar usando el tag **\_id**, si no se indica el id del documento usando este tag MongoDB asigna al documento un id por defecto, además el id no se puede repetir, por lo que si se ingresa un documento con un id que ya existe la operación fallará, por lo que es una buena práctica dejar que MongoDB genere el id de forma automática.

<br>

### Insertar varios documentos en una colección

```bash
[nombre de la base de datos].[nombre de la colección].insertMany([arreglo de documentos en formato JSON])
```

Ejemplo:

```bash
db.inventory.insertMany([
   {item: "sketch pad", qty: 95, size: {h: 22.85, w: 30.5, uom: "cm"}, status: "A"},
   {item: "postcard", qty: 45, size: {h: 10, w: 15.25, uom: "cm"}, status: "A"},
   {item: "sketchbook", qty: 80, size: {h: 14, w: 21, uom: "cm"}, status: "A"},
])
```

<br>

### Buscar documentos en una colección

#### Busqueda individual

```bash
[nombre de la base de datos].[nombre de la colección].findOne([documento de filtros en formato JSON])
```

Ejemplo:

```bash
db.inventory.findOne({status: "A"})
```

Retorna el primer documento segun el orden natural de MongoDB que cumpla con los filtros establecidos.

#### Busqueda grupal

```bash
[nombre de la base de datos].[nombre de la colección].find([documento de filtros en formato JSON])
```

Ejemplo:

```bash
db.inventory.find({item: "canvas"})
```

Retorna todos los documentos que cumplan con los filtros establecidos.

El metodo find ademas se puede combinar con otros metodos como:

- **pretty():** para imprimir de una forma mas legible los documentos resultantes de la busqueda.
- **count():** para contar el numero de documentos resultantes de la busqueda.

### Documentos JSON de filtros

Los documntos de filtors son la parte mas importante de las busquedas en MongoDB, ya que estos condicionan los parametros que debe tener un documento al momento de buscar en una colección, los documentos de filtros permiten varios tipos de operaciones, algunas de las mas importantes se listan a continuación.

#### equal

```bash
db.inventory.find(
    {item: "canvas"}
)
```

#### lower than

```bash
db.inventory.find(
    qty: {$lt: 30}
)
```

#### and

```bash
db.inventory.find({
    item: "canvas", 
    qty: {$lt:30}
})
```

#### or

```bash
db.inventory.find({
    $or:[
        {status: "A"}, 
        {qty: {$lt:30}} 
        ] 
})
```

<br>
