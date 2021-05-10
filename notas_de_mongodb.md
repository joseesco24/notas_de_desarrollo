# Notas De Mongodb

- [Introducción](#introducción)
- [Componentes Principales De Mongodb](#componentes-principales-de-mongodb)
  - [Bases De Datos](#bases-de-datos)
  - [Colecciones](#colecciones)
  - [Documentos](#documentos)
- [Ecosistema De Mongodb](#ecosistema-de-mongodb)
  - [Mongodb Server](#mongodb-server)
  - [Mongodb Shell](#mongodb-shell)
  - [Conectores De Mongodb](#conectores-de-mongodb)
- [Relaciones Entre Documentos En Mongodb](#relaciones-entre-documentos-en-mongodb)
- [Conexión Con Mongodb Server](#conexión-con-mongodb-server)
- [Operaciones Básicas Con Mongodb Shell](#operaciones-básicas-con-mongodb-shell)
  - [Iniciar Shell](#iniciar-shell)
  - [Limpiar Shell](#limpiar-shell)
  - [Ver Bases De Datos Disponibles](#ver-bases-de-datos-disponibles)
  - [Ver Colecciones Disponibles](#ver-colecciones-disponibles)
  - [Crear Nueva Base De Datos O Usar Una Ya Creada](#crear-nueva-base-de-datos-o-usar-una-ya-creada)
  - [Ver Nombre De La Base De Datos A La Que Está Conectado El Shell](#ver-nombre-de-la-base-de-datos-a-la-que-está-conectado-el-shell)
  - [Ver Funciones Disponibles](#ver-funciones-disponibles)
    - [En Una Base De Datos](#en-una-base-de-datos)
    - [En Una Colección](#en-una-colección)
- [Operaciones Con Bases De Datos En Mongodb Shell](#operaciones-con-bases-de-datos-en-mongodb-shell)
- [Operaciones Con Colecciones Y Documentos En Mongodb Shell](#operaciones-con-colecciones-y-documentos-en-mongodb-shell)
  - [Documentos De Filtros](#documentos-de-filtros)
    - [Operador Equal](#operador-equal)
    - [Operador Lower Than](#operador-lower-than)
    - [Operador And](#operador-and)
    - [Operador Or](#operador-or)
  - [Insertar Documentos En Una Colección](#insertar-documentos-en-una-colección)
    - [Inserción Individual](#inserción-individual)
    - [Inserción Grupal](#inserción-grupal)
  - [Buscar Documentos En Una Colección](#buscar-documentos-en-una-colección)
    - [Búsqueda Individual](#búsqueda-individual)
    - [Búsqueda Grupal](#búsqueda-grupal)
  - [Actualizar Documentos De Una Colección](#actualizar-documentos-de-una-colección)
    - [Actualización Individual](#actualización-individual)
    - [Actualización Grupal](#actualización-grupal)
  - [Eliminar Documentos De Una Colección](#eliminar-documentos-de-una-colección)
    - [Eliminación Individual](#eliminación-individual)
    - [Eliminación Grupal](#eliminación-grupal)
  - [Operaciones De Agregación](#operaciones-de-agregación)
  - [Manejo De Índices](#manejo-de-índices)
    - [Listar Índices](#listar-índices)
    - [Crear Nuevo Índice](#crear-nuevo-índice)

<br>

## Introducción

[**mongodb**](https://docs.mongodb.com/) es uno de los sistemas de bases de datos no relacionales más usados en el desarrollo profesional, es ampliamente usado en todo tipo de entornos de desarrollo gracias a su flexibilidad y facilidad de uso, que se deben en gran medida al hecho de que mongodb se basa en documentos similares a los documentos json. una de las mejores características de mongodb es que permite crear sistemas distribuidos de bases de datos, por lo que usando mongodb es totalmente factible tener un cluster de máquinas dedicadas al almacenamiento de los datos de una o varias bases de datos, esta característica hace que escalar un sistema de bases de datos basado en mongodb sea extremadamente fácil ya que solo hace falta agregar más nodos al cluster. otra de las principales características clave de mongodb es que es "schema less" en todas sus versiones, por lo que los documentos dentro de una misma colección pueden tener estructuras totalmente diferentes sin afectar el funcionamiento o el rendimiento de mongodb, y como si fuera poco las consultas de mongodb también son extremadamente eficientes por el hecho de ser una base de datos no relacional basada en documentos que además permite indexación, por lo que se puede optimizar incluso más su rendimiento mediante índices.

<br>

## Componentes Principales De Mongodb

<p align="center">
<img src="imagenes/notas_de_mongodb/componentes_de_mongodb.svg" width="80%" height="auto"/>
</p>

<br>

### Bases De Datos

las [**bases de datos**](https://docs.mongodb.com/manual/core/databases-and-collections/#databases) en mongodb son los espacios de almacenamiento como tal en los que se guardan las colecciones, cada base de datos tiene su propio archivo dentro del sistema de archivos del host en el que se ejecuta mongodb, además en un cluster de mongodb atlas pueden haber múltiples bases de datos distribuidas o replicadas entre los diferentes nodos del cluster.

<br>

### Colecciones

las [**colecciones**](https://docs.mongodb.com/manual/core/databases-and-collections/#collections) en mongodb son agrupaciones de documentos, son equivalentes a las tablas de las bases de datos relacionales y además en el caso de mongodb no se imponen esquemas fijos que deban seguir los documentos una misma colección.

<br>

### Documentos

los [**documentos**](https://docs.mongodb.com/manual/core/document/) en mongodb son registros dentro de cada colección, la estructura de los documentos de mongodb es similar a la de los documentos json, pero en realidad son documentos bson, que son documentos json binarios, usar bson hace fácil entender la estructura de cada documento y además permite almacenar una gran variedad de tipos de datos gracias a la cantidad de formatos que soporta bson. los documentos además son la unidad más básica dentro de mongodb y no pueden ser mayores a 16 megabytes.

<br>

## Ecosistema De Mongodb

<p align="center">
<img src="imagenes/notas_de_mongodb/ecosistema_mongodb.svg" width="80%" height="auto"/>
</p>

<br>

### Mongodb Server

el servidor de mongodb es el servidor encargado de gestionar las bases de datos como tal, sus principales funciones son almacenar las bases de datos en el sistema de archivos del host, mantener disponibles las bases de datos y realizar el cruce de datos y la entrega de resultados de todas las peticiones que se le hagan. al igual que la gran mayoría del software de código abierto el servidor de mongodb tiene dos versiones, una versión community y una enterprise, con la diferencia de que la versión enterprise gana algunas características adicionales respecto a la versión community.

<br>

### Mongodb Shell

es shell de mongodb es el shell con la que se interactúa de forma directa con el servidor de mongodb.

<br>

### Conectores De Mongodb

los conectores de mongodb son todas las [**bibliotecas**](https://docs.mongodb.com/drivers/) dentro de los diferentes lenguajes de programación que se usan para interactuar con el servidor de mongodb.

<br>

## Relaciones Entre Documentos En Mongodb

en mongodb y en el resto de sistemas de bases de datos no relacionales basadas en documentos suele haber solo dos formas para expresar las relaciones entre documentos, usando documentos anidados o usando referencias dentro de un documento a otro documento. los documentos anidados suelen usarse en relaciones **uno a uno**, ya que se aprovecha más la estructura de las bases de datos no relacionales para hacer solo un scan. si la relación es de **uno a muchos** lo adecuado es usar referencias si el documento que se va a relacionar va a estar actualizándose constantemente, ya que de esta forma las actualizaciones pueden hacerse en un solo documento y los cambios se verán reflejados en todos los documentos con los que está relacionado, usar referencias hace más lentas las búsquedas ya que no se aprovecha la estructura no relacional de mongodb, razón por la cual hace falta hacer más de un scan a cambio de facilitar la actualización de los documentos relacionados y optimizar el almacenamiento, sin embargo es lo ideal en este tipo de escenarios. si por el contrario el documento que se va a relacionar en una relación **uno a muchos** no se va a actualizar de forma constante se puede anidar simplemente como una copia dentro de cada documento con el que se relaciona sí no importa el almacenamiento, ya que de nuevo, de esta forma se aprovecha más la estructura de las bases de datos no relacionales para hacer un solo scan.

ejemplo de documento anidado:

```json
{
    "nombre": "pedro",
    "apellido": "perez",
    "lugar_residencia": {
        "ciudad": "bogotá",
        "departamento": "cundinamarca",
        "direccion": "calle 175 #64-11"
    },
    "edad": 36
}
```

ejemplo de múltiples documentos anidados:

```json
{
    "nombre": "pedro",
    "apellido": "perez",
    "lugar_residencia": [
        {
            "ciudad": "bogotá",
            "departamento": "cundinamarca",
            "direccion": "calle 175 #64-11"
        },
        {
            "ciudad": "neiva",
            "departamento": "huila",
            "direccion": "calle 4 #17-11"
        }
    ],
    "edad": 36
}
```

ejemplo de documento referenciado:

```json
{
    "id": "62a873996f6aaaa78dac39c0d5c36a39",
    "nombre": "perez",
    "apellido": "perez",
    "edad": 36
}
```

```json
{
    "autor": "62a873996f6aaaa78dac39c0d5c36a39",
    "nombre": "perez",
    "ano_publicacion": 2021
}
```

ejemplo de múltiples documentos referenciados:

```json
{
    "id": "62a873996f6aaaa78dac39c0d5c36a39",
    "nombre": "perez",
    "apellido": "perez",
    "edad": 36
}
```

```json
{
    "id": "a85ba64adf6bf75e64b221a3171b0269",
    "nombre": "felipe",
    "apellido": "perez",
    "edad": 32
}
```

```json
{
    "autor": ["62a873996f6aaaa78dac39c0d5c36a39", "a85ba64adf6bf75e64b221a3171b0269"],
    "nombre": "perez",
    "ano_publicacion": 2021
}
```

<br>

## Conexión Con Mongodb Server

para establecer una conexión entre mongodb con cualquier aplicación o driver, independientemente de la versión de mongodb server, es necesario usar un [**string de conexión en formato uri**](https://docs.mongodb.com/manual/reference/connection-string/#connection-string-uri-format), a continuación se muestra el formato estándar para establecer una conexión entre una aplicación y un mongodb server ambos dentro del mismo host.

```unknown
mongodb://<ip de la máquina que tiene mongodb server>:<puerto en el que está expuesto mongo, normalmente 27017>
```

ejemplo:

```unknown
mongodb://127.0.0.1:27017
```

<br>

## Operaciones Básicas Con Mongodb Shell

el shell de mongodb o [**mongodb shell**](https://docs.mongodb.com/manual/mongo/) es una interfaz interactiva basada en javascript que se usa para interactuar de forma directa con el mongodb server mediante la terminal, al ser un shell basado en javascript el shell de mongodb permite usar comandos con sintaxis de [**shell**](https://docs.mongodb.com/manual/reference/program/mongo/#mongodb-binary-bin.mongo) o comandos con sintaxis de [**javascript**](https://docs.mongodb.com/manual/reference/method/), sin embargo la mayoría de las operaciones sólo están disponibles usando la sintaxis de javascript, además de poder realizar acciones simples en mongodb shell también se pueden crear [**scripts**](https://docs.mongodb.com/manual/tutorial/write-scripts-for-the-mongo-shell/) basados en javascript que se ejecuten sobre el shell de mongodb, por lo que se pueden automatizar varios tipos de tareas o consultas en usando javascript.

<br>

### Iniciar Shell

```unknown
mongo
```

<br>

### Limpiar Shell

```unknown
ctrl + l
```

```unknown
cls
```

<br>

### Ver Bases De Datos Disponibles

```unknown
show databases
```

```unknown
show dbs
```

<br>

### Ver Colecciones Disponibles

```unknown
show collections
```

<br>

### Crear Nueva Base De Datos O Usar Una Ya Creada

```unknown
use <nombre de la nueva base de datos>
```

ejemplo:

```unknown
use db
```

<br>

### Ver Nombre De La Base De Datos A La Que Está Conectado El Shell

```unknown
db
```

<br>

### Ver Funciones Disponibles

#### En Una Base De Datos

```unknown
<nombre de la base de datos>.help()
```

ejemplo:

```javascript
db.help()
```

#### En Una Colección

```unknown
<nombre de la base de datos>.<nombre de la colección>.help()
```

ejemplo:

```javascript
db.inventory.help()
```

<br>

## Operaciones Con Bases De Datos En Mongodb Shell

<br>

## Operaciones Con Colecciones Y Documentos En Mongodb Shell

<br>

### Documentos De Filtros

los documentos de filtros son parte fundamental de la mayoría de las operaciones [**crud**](https://docs.mongodb.com/manual/crud/) com mongodb, ya que permiten, como su nombre indica, filtrar los documentos resultantes de una búsqueda, para esto mongodb dispone de varios [**operadores**](https://docs.mongodb.com/manual/reference/operator/) que se usan en el mongodb shell para realizar todo tipo de operaciones necesarias para filtrar datos, a continuación se muestran algunos ejemplos de la sintaxis de algunos de los operadores más comunes.

#### Operador Equal

```javascript
db.inventory.find(
    {item: "canvas"}
)
```

#### Operador Lower Than

```javascript
db.inventory.find(
    qty: {$lt:30}
)
```

#### Operador And

```javascript
db.inventory.find(
    {
        item: "canvas",
        qty: {$lt:30}
    }
)
```

#### Operador Or

```javascript
db.inventory.find(
    {
        $or:[
            {status: "a"},
            {qty: {$lt:30}}
            ]
    }
)
```

<br>

### Insertar Documentos En Una Colección

mongodb por defecto no crea bases de datos vacías, por lo que es necesario luego de crear una nueva base de datos crear al menos una colección y un documento, si la colección en la que se quiere insertar el documento no existe mongodb crea una nueva colección con el nombre indicado.\
al insertar un documento el id se puede especificar usando el tag **\_id**, si no se indica el id del documento usando este tag mongodb asigna al documento un id por defecto, además el id no se puede repetir, por lo que si se ingresa un documento con un id que ya existe la operación fallará, por lo que es una buena práctica dejar que mongodb genere el id de forma automática.

#### Inserción Individual

```unknown
<nombre de la base de datos>.<nombre de la colección>.insertone(<documento en formato json>)
```

ejemplo:

```javascript
db.inventory.insertone(
    {size: {h: 28, w: 35.5, uom: "cm"}, tags: ["cotton"], item: "canvas", qty: 100}
)
```

#### Inserción Grupal

```unknown
<nombre de la base de datos>.<nombre de la colección>.insertmany(<arreglo de documentos en formato json>)
```

ejemplo:

```javascript
db.inventory.insertmany(
    [
        {item: "sketch pad", qty: 95, size: {h: 22.85, w: 30.5, uom: "cm"}, status: "a"},
        {item: "postcard", qty: 45, size: {h: 10, w: 15.25, uom: "cm"}, status: "a"},
        {item: "sketchbook", qty: 80, size: {h: 14, w: 21, uom: "cm"}, status: "a"}
    ]
)
```

<br>

### Buscar Documentos En Una Colección

#### Búsqueda Individual

```unknown
<nombre de la base de datos>.<nombre de la colección>.findone(<documento de filtros en formato json>, <proyección en formato json>)
```

ejemplo:

```javascript
db.inventory.findone(
    {item: "canvas"},
    {_id:0, item:1, status:1}
)
```

en el ejemplo anterior se usa una proyección y un filtro, el filtro **({item: "canvas"})** se usa para retornar solamente los documentos que cumplan con ciertos parámetros y la proyección **({\_id:0, item:1, status:1})** asegura que se muestren solo ciertos campos de los documentos retornados, los filtros son parte fundamental de cualquier operación de búsqueda, mientras que las proyecciones pueden facilitar en gran medida la lectura de los resultados omitiendo la información innecesaria.\
al usar el método **findone** solamente se retorna el primer documento que cumpla con las condiciones de la búsqueda según el orden natural de los documentos de mongodb.

#### Búsqueda Grupal

```unknown
<nombre de la base de datos>.<nombre de la colección>.find(<documento de filtros en formato json>, <proyección en formato json>)
```

ejemplo:

```javascript
db.inventory.find(
    {item: "canvas"},
    {_id:0, item:1, status:1}
)
```

al usar el método **find** se retornan todos los documento que cumpla con las condiciones de la búsqueda, el método **find** al igual que el método **findone** y la gran mayoría de los métodos de búsqueda en mongodb admite el uso de filtros y proyecciones.

el método find además se puede combinar con otros métodos como:

- **pretty():** para imprimir de una forma más legible los documentos resultantes de la búsqueda.
- **count():** para contar el número de documentos resultantes de la búsqueda.
- **explain('executionstats'):** muestra las estadísticas de la ejecución del query.

<br>

### Actualizar Documentos De Una Colección

#### Actualización Individual

```unknown
<nombre de la base de datos>.<nombre de la colección>.updateone(<documento de filtros en formato json>, <json>)
```

ejemplo:

```javascript
db.inventory.updateone(
    {
        status: "a"
    },
    {
        $set: {status: "b"},
    }
)
```

#### Actualización Grupal

```unknown
<nombre de la base de datos>.<nombre de la colección>.updatemany(<documento de filtros en formato json>, <json>)
```

ejemplo:

```javascript
db.inventory.updatemany(
    {
        status: "a"
    },
    {
        $set: {status: "b"},
    }
)
```

<br>

### Eliminar Documentos De Una Colección

#### Eliminación Individual

```unknown
<nombre de la base de datos>.<nombre de la colección>.deleteone(<documento de filtros en formato json>)
```

ejemplo:

```javascript
db.inventory.deleteone(
    {status: "b"}
)
```

el documento eliminado con deleteone siempre es el primer documento que cumple con las condiciones del json de filtros según el orden natural de mongodb.

#### Eliminación Grupal

```unknown
<nombre de la base de datos>.<nombre de la colección>.deletemany(<documento de filtros en formato json>)
```

ejemplo:

```javascript
db.inventory.deletemany(
    {status: "b"}
)
```

<br>

### Operaciones De Agregación

las [**agregaciones**](https://docs.mongodb.com/manual/aggregation/) en mongodb son operaciones avanzadas que se pueden realizar en mongodb.

<br>

### Manejo De Índices

los [**índices**](https://docs.mongodb.com/manual/indexes/) en mongodb se usan para evitar que mongodb tenga que hacer un escaneo completo de toda una colección en búsqueda de un elemento, facilitando así los querys, los tipos de índices disponibles en mongodb se listan a continuación.

- **de un solo campo:**
- **multi llave:**
- **compuestos:**
- **geoespaciales:**
- **de texto:**
- **hashed:**

#### Listar Índices

```unknown
<nombre de la base de datos>.<nombre de la colección>.getindexes()
```

ejemplo:

```javascript
db.inventory.getindexes()
```

#### Crear Nuevo Índice

```unknown
<nombre de la base de datos>.<nombre de la colección>.createindex({<nombre del campo que se usará como índice>:<tipo de índice>})
```

ejemplo:

```javascript
db.inventory.createindex({nombre: "text"})
```

<br>
