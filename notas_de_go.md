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

## Funciones

Las funciones en Go al igual que en Python permiten retornar y recibir varios argumentos, con la ventaja de que los tipos de datos se deben declarar en la definición de la función de forma obligatoria, lo que mejora la lectura del código, las funciones en Go se declaran con la palabra reservada **func**.

```go

// Función regular sin valor de retorno.

func regular_function(message string) {
 fmt.Println(message)
}

// Función con tres valores de retorno.

func function_with_three_returns(a, b int, c string) {
 fmt.Println(a, b, c)
}

// Función con un solo valor de retorno.

func regular_function_with_return(a int) int {
 return a * 2
}

// Función con dos valores de retorno.

func function_with_two_returns(a int) (c, d int) {
 return a, a * 2
}

func main() {

 value_1, value_2 := function_with_two_returns(4)
 fmt.Println(value_1, value_2)

 value_4, _ := function_with_two_returns(4)
 fmt.Println(value_4)

 fmt.Println(function_with_two_returns(4))

 value_3 := regular_function_with_return(4)
 fmt.Println(value_3)

 fmt.Println(regular_function_with_return(4))

 regular_function("Hola Mundo")

 function_with_three_returns(1, 2, "Hola")

}

```

<br>

## Ciclos

En Go a diferencia de otros lenguajes solo existen los ciclos for, que se inician con la palabra reservada **for**, a continuación se muestran algunos ejemplos de cómo usar ciclos for sencillos en Go.

```go

 // For condicional clásico.

 for i := 0; i < 10; i++ {
  fmt.Println(i)
 }

 // For while.

 counter := 0

 for counter < 10 {
  fmt.Println(counter)
  counter++
 }

 // For forever.

 counter_forever := 0

 for {
  fmt.Println(counter_forever)
  counter_forever++
 }

```

<br>

## Condicionales

Los condicionales en Go usan una sintaxis similar a la de la mayoría de los lenguajes de programación usando **if**, **else** y **else if**, a continuación se muestran algunos ejemplos de condicionales en Go.

```go

 // Declaración de variables.

 valor_1 := 1
 valor_2 := 2

 // If clasico.

 if valor_1 == 0 {
  fmt.Println("Si es 1")
 } else if valor_2 == 2 {
  fmt.Println("Val 2 == 2")
 } else {
  fmt.Println("No es 1")
 }

 // If con and.

 if valor_1 == 1 && valor_2 == 2 {
  fmt.Println("Val 1 = 1 y Val 2 = 2")
 }

 // If con or.

 if valor_1 == 0 || valor_2 == 2 {
  fmt.Println("Val 1 = 0 o Val 2 = 2")
 }

```

<br>

## Switch

Los switch en Go permiten simplificar la sintaxis en casos en los que se deben usar varios condicionales if consecutivos y se crean usando la palabra reservada **switch**, a continuación se muestran algunos ejemplos de cómo usar switches en Go.

```go

 // Switch clásico.

 switch valor_1 {
 case 0:
  fmt.Println("Si es par")
 default:
  fmt.Println("No es par")
 }

 // Switch declarado en la misma línea.

 switch valor_2 := 4 % 2; valor_2 {
 case 0:
  fmt.Println("Si es par")
 default:
  fmt.Println("No es par")
 }

 // Switch condicional.

 valor_3 := 100

 switch {
 case valor_3 > 100:
  fmt.Println("Mayor")
 case valor_3 < 100:
  fmt.Println("Menor")
 default:
  fmt.Println("Igual")
 }

```

<br>

## Defer, break y continue

La palabra reservada **defer** en Go permite indicar al lenguaje que la función que se indica debe ejecutarse luego de finalizar la ejecución del main, en el siguiente ejemplo se imprime primero mundo y luego hola, ya que la función de imprimir hola es precedida por la instrucción **defer**, **defer** es especialmente útil para cerrar conexiones o archivos al finalizar la ejecución del programa.

```go

// Ejemplo de defer.

defer fmt.Println("hola")
fmt.Println("mundo")

```

Dentro de los ciclos **for** se pueden utilizar los comandos **continue** y **break**, **continue**, por su parte, permite, por ejemplo, que la ejecución de un ciclo continuo ante ciertos errores que han sido controlados, **break** por otra parte permite detener la ejecución de un ciclo.

```go

 // Continue y break.

 for i := 0; i < 10; i++ {

  fmt.Println(i)

  // Continue.

  if i == 4 {
   fmt.Println("i es 4")
   continue
  }

  // Break.

  if i == 8 {
   fmt.Println("break")
   break
  }
 }

```

<br>

## Arrays y slices

Los arrays en Go se declaran usando la palabra reservada **var** al igual que las variables, con la diferencia de que además se deben usar **llaves** para indicar que la variable es un arreglo y se debe indicar la cantidad de **valores máximos** que podrá almacenar el array y además, se debe indicar también el tipo de datos que almacenará el array en cada posición, a continuación se muestra un ejemplo de la declaración de un array, la forma en la que se cambian sus valores y la forma como se imprimen algunos de sus valores más importantes, como la cantidad de valores que tiene y la cantidad de valores que soporta el array.

```go

 // Declaración de un array.

 var array [4]int

 // Cambio de los valores del array.

 array[0] = 1
 array[1] = 2

 // Impresión de los valores del array.

 fmt.Println(array)

 // Impresión de las especificaciones del array.

 // Número de elementos en el array.

 fmt.Println(len(array))

 // Capacidad máxima del array.

 fmt.Println(cap(array))

```

La principal diferencia entre un slice y un array es que los slices no tienen una longitud fija, a diferencia de los arrays, cuya longitud se fija desde el momento en el que se crean.

```go

 // Declaración de un slice.

 slice := []int{0, 1, 2}

 // Agregar elementos al slice.

 slice = append(slice, 3, 4, 5)

 // Impresión de los valores del slice.

 fmt.Println(slice)

 // Número de elementos en el slice.

 fmt.Println(len(slice))

 // Capacidad máxima del slice.

 fmt.Println(cap(slice))

  // Métodos de un slice.

 fmt.Println(slice[0])
 fmt.Println(slice[:3])
 fmt.Println(slice[2:4])
 fmt.Println(slice[4:])

 // Append de un nuevo slice.

 new_slice := []int{6, 7, 8}
 slice = append(slice, new_slice...)

 fmt.Println(slice)

```

Para recorrer los slice o arrays se puede utilizar la función **range**, range itera a través de los elementos de la mayoría de las estructuras de datos en Go retornando un índice y un valor, a continuación se muestra un ejemplo de como usar range para recorrer un slice.

```go

 // Declarando el slice.

 slice := []string{"hola", "que", "hace"}

 // Recorriendo el slice usando indice y valor.

 for indice, valor := range slice {
  fmt.Println(indice, valor)
 }

 // Recorriendo el slice usando solo el valor.

 for _, valor := range slice {
  fmt.Println(valor)
 }

 // Recorriendo el slice usando solo el indice.

 for indice := range slice {
  fmt.Println(indice)
 }

 // Recorriendo un string.

 for indice, valor := range strings.ToLower("hOla") {
  fmt.Println(indice, string(valor))
 }

```

<br>

## Estructuras llave valor con maps

Las estructuras llave valor son estructuras indexadas en las que para acceder a un valor en específico se necesita una llave, que además es única en la estructura, en Go este tipo de estructuras son llamadas **map** y sin el equivalente de los diccionarios en otros lenguajes como Python o Java. Algo que cabe destacar es que en Go al acceder a una llave no especificada se imprime el zero value de ese tipo de dato. A continuación se muestra un ejemplo de cómo usar un map en Go.

```go

 // Declarando el map.

 mapa := make(map[string]int)

 // Agregra valores al map.

 mapa["pepito"] = 20
 mapa["jose"] = 14

 // Imprimiendo el map.

 fmt.Println(mapa)

 // Recorriendo el map con range.

 for llave, valor := range mapa {
  fmt.Println(llave, valor)
 }

 // Econtrar un valor del map y confirmas si la llave existe.

 value, ok := mapa["jose"]
 fmt.Println(value, ok)

```

<br>
