# Notas De Go

- [Introducción](#introducción)
- [Compilar](#compilar)
- [Compilar y ejecutar](#compilar-y-ejecutar)

<br>

## Introducción

[**Go tambien conocido como golang**](https://golang.org/) es un lenguaje compilado y estáticamente tipado, fue creado en Google con la intención de manejar procesos pesados con la potencia de C pero conservando la sintaxis amigable de Python, por lo que Go se sitúa en un punto intermedio entre ambos, haciendo fácil el desarrollo, como en Python pero conservando en gran medida la potencia de C, además el proceso de compilación es bastante rápido y las tareas pesadas son más rápidas ya que nativamente Go maneja concurrencia y utiliza todos los cores disponibles del host.

Antes de empezar a desarrollar un proyecto de Go es necesario crear los siguientes directorios:

- go/bin: contiene los binarios de las dependencias necesarias para el proyecto.
- go/src: contiene el código fuente del proyecto.
- go/pkg: contiene los paquetes necesarios para el proyecto.

El nombre del directorio de la raíz puede ser reemplazado por cualquier otro nombre, sin embargo los subdirectorios siempre deben estar presentes con los nombres bin, src y pkg para que el desarrollo del proyecto funcione bien.

Una vez preparados los directorios de desarrollo se deben además instanciar varias variables de entorno que indicarán a Go a donde debe dirigirse según el proyecto:

- GOPATH: es el directorio raíz del proyecto.
- GOBIN: es el directorio en el que se guardaran los binarios del proyecto.
- GOROOT: es la ruta en la que está instalado Go (usualmente /usr/local/go en Linux).

Adicionalmente se deben incluir estas variables de entorno el el Path del sistema en el caso de Linux con:

```bash
PATH=$PATH:$GOBIN:$GOROOT/bin
```

Los comandos anteriores usados de forma estandar son:

```bash
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export GOROOT=/usr/local/go

export PATH=$PATH:$GOBIN:$GOROOT/bin
```

<br>

## Compilar

Al compilar cualquier proyecto en Go el resultado de la compilación se guarda en el directorio src, para compilar un main.go por ejemplo se usa el comando **go build**:

```bash
go build main.go
```

<br>

## Compilar y ejecutar

Go también permite compilar y ejecutar un proyecto almacenando temporalmente las compilaciones de tal modo que la carpeta src no se llene de archivos compilados, para esto se usa el comando **go run**:

```bash
go build main.go
```
