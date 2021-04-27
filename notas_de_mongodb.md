# MongoDB

[**MongoDB**](https://www.mongodb.com/2) es la base de datos no relacional basada en documentos más usada en el desarrollo profesional, MongoDB es ampliamente usado como motor de base de datos gracias a su flexibilidad y facilidad de uso, la cual se debe a que cada documento dentro de MongoDB es almacenado como un documento BSON, que es la representación binaria de un documento JSON. MongoDB además permite almacenar documentos de forma distribuida, por lo que usando MongoDB como motor de bases de datos es totalmente factible tener un cluster de servidores dedicados al almacenamiento de los datos de una sola base de datos, esta característica además hace que escalar una base de datos MongoDB sea extremadamente fácil ya que solo hace falta agregar más nodos al cluster. Una de las mejores características de MongoDB es que es "Schema Less" por lo que los documentos pueden tener estructuras totalmente diferentes sin afectar el funcionamiento de MongoDB y como si fuera poco las consultas de MongoDB también son extremadamente eficientes por el hecho de ser una base de datos no relacional basada en documentos.

<br>

## Ecosistema de MongoDB

<p align="center">
<img src="imagenes/notas_de_mongodb/ecosistema_mongodb.png" width="76%" height="auto"/>
</p>

El ecosistema de MongoDB se divide en varias partes las cuales se describen a continuación:

- **MongoDB Server**: Es el motor de base de datos como tal, por lo que es donde se guardan los datos, además el MongoDB Server se divide en tres versiones.

  - Atlas: Es la versión en nube de una base de datos con MongoDB.
  - Community: Es la versión de código abierto de MongoDB.
  - Enterprise: Es la versión de pago de MongoDB.

- **MongoDB Shell**: Es la consola con la que se interactúa con el MongoDB Server.
- **MongoDB Compass**: Es una interfaz gráfica con la que se puede interactuar con el MongoDB Server.
- **Conectores**: Son las librerías dentro de cada lenguaje que se usan para interactuar con el MongoDB Server.
- **MongoDB Realm**: Es una versión lite de MongoDB que se puede instalar en dispositivos móviles.

<br>

## MongoDB shell

```bash
mongo
```
