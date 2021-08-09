# Notas De Go

[**Go**](https://golang.org/) también conocido como Golang es un lenguaje compilado y estáticamente tipado, fue creado en Google con la intención de manejar procesos pesados con la potencia de C pero conservando la sintaxis amigable de Python, por lo que Go se sitúa en un punto intermedio entre ambos, haciendo fácil el desarrollo, como en Python pero conservando en gran medida la potencia de C, además el proceso de compilación es bastante rápido y las tareas pesadas son más rápidas ya que nativamente Go maneja concurrencia y utiliza todos los cores disponibles del host.

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

Los comandos anteriores usados de forma estándar son:

```bash
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export GOROOT=/usr/local/go

export PATH=$PATH:$GOBIN:$GOROOT/bin
```

<br>

## Compilar

Al compilar cualquier proyecto en Go el resultado de la compilación se guarda en el directorio raíz del proyecto (GOPATH), para compilar un main.go por ejemplo se usa el comando **go build**:

```bash
go build main.go
```

<br>

## Compilar y ejecutar

Go también permite compilar y ejecutar un proyecto almacenando temporalmente las compilaciones de tal modo que el directorio raíz del proyecto (GOPATH) no se llene de archivos compilados, para esto se usa el comando **go run**:

```bash
go run main.go
```

<br>

## Variables, constantes y zero values

Go permite declarar constantes, que son variables cuyo valor no cambiará durante la ejecución del programa, para declarar una constante en Go se usa la palabra reservada **const**, al declarar la nueva constante además se puede incluir el tipo de dato de la constante, no incluir el valor de la constante no afecta la ejecución del programa, pero si reduce un poco el desempeño del programa y el uso de memoria del mismo, a continuación se muestran ejemplos de ambos casos:

```go
// Declaración de constantes con tipo de dato.
const pi_1 float64 = 3.14

// Declaración de constantes sin ningún tipo de dato.
const pi_2 = 3.1415
```

Al igual que con las declaraciones de las constantes donde se usa **const** con las variables también se usa la palabra reservada **var** por lo general, la forma correcta de declarar variables en Go para conservar el desempeño del programa y para gestionar bien la memoria es declarando las variables con **var** e indicando su tipo de dato, adicionalmente el valor se puede asignar de forma inmediata o se puede asignar de forma posterior. Go también soporta declarar y asignar variables sin tipo de dato, pero usar este tipo de variables reduce el desempeño del programa y no gestiona bien la memoria, a continuación se muestran ejemplos del uso de variables en Go:

```go
// Crea la variable, le asigna un tipo de dato y el valor.
var altura int = 14

// Crea la variable y le asigna un tipo de dato sin asignar el valor.
var area int

// Crea la variable y se le asigna un valor sin asignar un tipo de dato.
base := 14


// Asigna un valor a la variable área.
area = 18
```

Algo que cabe destacar es que Go a diferencia de otros lenguajes que usan null asigna valores por defecto a las variables que se declaran, pero que no se asignan.

**Nota**: Go no permite que se compile o ejecute el código a no ser que todas las variables y constantes previamente declaradas se utilicen, algunos de los tipos primitivos de datos que acepta Go se muestran en el siguiente [link](https://www.tutorialspoint.com/go/go_data_types.htm).

<br>

## Operadores aritméticos

Los operadores aritméticos en Go son bastante similares a los usados en la mayoría de los lenguajes de programación, algunas de las operaciones aritméticas más básicas se listan y ejemplifican a continuación usando la siguiente declaración de variables como punto de partida para todas las operaciones.

```go
x := 10
y := 50
```

### Suma

```go
result := x + y
```

### Resta

```go
result := x - y
```

### Multiplicación

```go
result := x * y
```

### División

```go
result := x / y
```

### Módulo

```go
result := x % y
```

### Incremental

```go
x++
```

### Decremental

```go
x--
```

<br>

## Uso básico del paquete fmt

El paquete fmt permite realizar varias funciones, como imprimir strings.

```go
fmt.Println("Hola Mundo")
```

Formatear strings.

```go
mensaje_3 := "platzi"
decimal_1 := 500

string_formateado := fmt.Sprintf("%v tiene mas de %v cursos", mensaje_3, decimal_1)
```

Imprimir strings con formato.

```go
mensaje_3 := "platzi"
decimal_1 := 500

fmt.Printf("%s tiene mas de %d cursos \n", mensaje_3, decimal_1)
```

O imprimir el tipo de dato dentro de una variable.

```go
message_1 := "message 1"

fmt.Printf("tipo de variable de message_1: %T \n", message_1)
```

Cuando se usan strings formateados con fmt lo más adecuado es usar el tipo de dato concreto, pero se puede usar %v cuando no se conoce el tipo de dato o %T para saber el tipo de dato, además el paquete fmt acepta varios tipos de [datos](https://pkg.go.dev/fmt) más usando las claves correctas.

<br>