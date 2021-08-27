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

## Structs

En la mayoría de lenguajes existen estructuras llamadas clases, las cuales pueden poseer atributos y métodos, en Go no este tipo de estructuras son reemplazadas por **Structs**, a continuación se muestra el uso de un Struct con Go.

```go

// Instanciamiento del struct.

type car struct {
 brand string
 year  int
}

func main() {

 // Creacion del Struct.

 my_car := car{brand: "hyundai", year: 2020}

 // Impresion del Struct.

 fmt.Println(my_car)

 // Creacion del struct.

 var other_car car
 other_car.brand = "Ferrari"

 // Impresion del Struct.

 fmt.Println(other_car)

}

```

Al momento de crear un nuevo objeto usando structs existen tres posibles formas de instanciar un nuevo objeto, a continuación se ejemplifican las tres formas.

```go

type car struct {
 brand string
 year  int
}

func main() {

 // Metodo 1 (zero values)

 car1 := car{}

 // Metodo 2 (instanciamiento en la creacion)

 car2 := car{brand: "mazda", year: 2021}

 // Metodo 3 (creacion con new, retorna un apuntador)

 car3 := new(car)

 fmt.Println(car1, car2, *car3)

}

```

### Simulación de constructores con structs y apuntadores

Adicionalmente a los tres métodos mostrados anteriormente en Go se puede simular el comportamiento de un constructor usando apuntadores y structs, a continuación se muestra un ejemplo de esto usando de nuevo el struct de car, es importante resaltar que se deben usar apuntadores para retornar la referencia de memoria del nuevo struct, para así poder modificarlo en caso de ser necesario, ya que de otra forma Go tratara los nuevos structs como copias.

```go

type car struct {
 brand string
 year  int
}

func newCar(brand string, year int) *car {
 return &car{brand: brand, year: year}
}

func main() {

 // Metodo 4 (simulacion de contructor)

 car4 := newCar("Mazda", 2024)

 fmt.Println(*car4)

}

```

### Composición usando structs

La herencia en los diferentes lenguajes de programación permite que una clase determinada obtenga propiedades y métodos de otra, de esta forma se ahorra código aplicando polimorfismo, en Go se aplica composición, de tal modo que cada struct es independiente de los demás, por lo que para obtener un funcionamiento similar al de la herencia en Go un struct se compone de otros structs, de tal modo que un struct pueda contener otros structs, como por ejemplo, el struct de empleado de tiempo completo contiene dos struct, persona y empleado.

```go

// Instanciamiento del struct persona.

type Person struct {
 name     string
 birdYear int
}

// Intanciamiento del struct empleado.

type Employee struct {
 id int
}

// Intanciamiento del struct empleado de tiempo completo.

type FullTimeEmployee struct {
 Person
 Employee
}

func main() {

 // Creacion del objeto de empleado de tiempo completo.

 newFullTimeEmployee := FullTimeEmployee{}

 // Llenando los atributos del empleado.

 newFullTimeEmployee.name = "Jose"
 newFullTimeEmployee.birdYear = 1998
 newFullTimeEmployee.id = 14

 // Imprimiendo la estructura del empleado.

 fmt.Println(newFullTimeEmployee)

}

```

<br>

## Modificadores de acceso

En Go la forma de permitir que un recurso sea público y accesible desde diferentes módulos o paquetes es declarando la primera letra del tipo de dato en mayúscula, al declararlo en minúscula se restringe el acceso a solo el módulo actual, es decir que el recurso es privado.

```go

// Paquete (un directrio por debajo del directorio donde esta el main).

package my_package

// Instanciamiento del struct publico.

type Car struct {
 Brand string
 Year  int
}

// Main (un directrio por encima del directorio donde esta el paquete).

package main

import (
 pk "access_modificators/my_package"
 "fmt"
)

func main() {

 var my_car pk.Car

 my_car.Brand = "Hyundai"
 my_car.Year = 2018

 fmt.Println(my_car)
}

```

<br>

## Punteros

Los punteros en Go permiten acceder a las direcciones de memoria en las que se guardan los valores de una variable, para obtener la dirección de memoria de una variable se usa el **ampersand (&)** y para acceder a su valor se usa el **asterisco (\*)**, a continuación se muestra un ejemplo de uso de punteros en Go.

```go

 // Se crea la variable a y se le asigna un valor.

 a := 50

 // Se crea la variable b y se apunta a la direccion de memoria de a.

 b := &a

 fmt.Println(a, b)

 // Se usa el asterisco para acceder al valor de la memoria en lugar de usar su direccion.

 fmt.Println(a, *b)

 // Modificando el valor de b en la memoria.

 *b = 100

 // a y b imprimen 100 ya que ambas variables apuntan a la misma direccion de memoria.

 fmt.Println(&a, &b)
 fmt.Println(*b)
 fmt.Println(a)

```

<br>

## Punteros y structs

Una de las principales ventajas de usar punteros en Go es que permiten alterar también los structs, en esta sección se muestra como crear funciones para acceder a los valores de los structs y cómo modificarlos mediante punteros.

```go

type pc struct {
 ram   int
 disk  int
 brand string
}

func (myPc pc) ping() {
 fmt.Println(myPc.brand, "pong")
}

// Se usa el asterisco para indicar que se van a acceder los valores del struct.

func (myPc *pc) duplicateRam() {
 myPc.ram *= 2
}

func main() {

 // Se instancia el struct.

 myPc := pc{ram: 16, disk: 240, brand: "MSI"}
 fmt.Println(myPc)

 // Se llama la funcion ping.

 myPc.ping()

 // Se llama a la funcion duplicate dos veces.

 myPc.duplicateRam()
 fmt.Println(myPc.ram)

 myPc.duplicateRam()
 fmt.Println(myPc.ram)

}

```

<br>

## Personalización de outputs de structs con stringers

Los structs en Go poseen un método llamado String, este método puede ser sobreescrito para personalizar así la impresión de los datos del struct.

```go

type pc struct {
 ram   int
 disk  int
 brand string
}

// Sobre escritura del metodo String del struct.

func (myPc pc) String() string {
 return fmt.Sprintf("El pc tiene %dGB ram, %dGB disco y es un %s", myPc.ram, myPc.disk, myPc.brand)
}

func main() {

 // Se instancia el struct.

 myPc := pc{ram: 16, disk: 240, brand: "MSI"}
 fmt.Println(myPc)

}

```

<br>

## Interfaces

Las interfaces permiten usar fácilmente el mismo método cuando varios structs lo comparten, por ejemplo en el caso que se muestra a continuación se ve como usando una interfaz es más sencillo llamar a los métodos de calcular área para un cuadrado y un rectángulo, tomando en cuenta que el cálculo para ambos casos es diferente, gracias a las interfaces y a la composición Go consigue un comportamiento polimórfico equivalente al que se puede ver en otros lenguajes como Java o Python.

```go

// Intanciamiento de la inerfaz.

type figuras2D interface {
 area() float32
}

// Intanciamiento de los structs.

type cuadrado struct {
 base float32
}

type rectangulo struct {
 base   float32
 altura float32
}

// Intanciamiento de los metodos compartidos.

func (c cuadrado) area() float32 {
 return c.base * c.base
}

func (r rectangulo) area() float32 {
 return r.base * r.altura
}

// Intanciamiento de la funcion que usa la interfaz para usar los metodos comprtidos.

func calculate(f figuras2D) {
 fmt.Println("Area ", f.area())
}

func main() {

 // Intanciamiento de los structs.

 var myCuadrado = cuadrado{base: 4}
 var myRectnagulo = rectangulo{base: 4, altura: 2}

 // Uso de la fucncion con metodos copartidos.

 calculate(myCuadrado)
 calculate(myRectnagulo)

}

```

<br>

## Listas de interfaces

Las listas de interfaces en Go permiten simular el comportamiento de arrays en lenguajes más flexibles como Python o JavaScript, donde es posible guardar diferentes tipos de datos en una lista, a continuación se muestra un ejemplo de cómo conseguir esta funcionalidad en Go.

```go

 // Intanciamiento de la lista de interfaces.

 myInterface := []interface{}{"Hola 1", 12, 4.9}

 // gregando un nuevo elemento al slice.

 myInterface = append(myInterface, "Hola 2")

 fmt.Println(myInterface...)

```

<br>

## Concurrencia con goroutines

Las goroutines se ejecutan usando la palabra reservada **go** y permiten ejecutar tareas de forma concurrente usando Go, a continuación se muestra un ejemplo de cómo implementar una goroutine simple junto con un wait group para así esperar a que todas las goroutines terminen.

```go

func say(text string, wg *sync.WaitGroup) {

 // Se usa defer para indicar al wait group que todo esta listo una vez finalice la funcion.

 defer wg.Done()

 fmt.Println(text)

}

func main() {

 // Configuracion del wait group.

 var wg sync.WaitGroup

 fmt.Println("Hola")

 // Se agrega una go routine al wait group.

 wg.Add(1)

 // Se ejecuta la funcion say y se envia el texto junto con el puntero del wait group.

 go say("Mundo", &wg)

 // Se indica a la funcion principal que espere hasta que todas las tareas del wait group finalicen.

 wg.Wait()

}

```

Adicionalmente al usar goroutines Go permite definir funciones anónimas, a continuación se muestra un ejemplo de funciones anónimas con Go.

```go

 go func() {
  fmt.Println("Hola")
 }()

 go func(text string) {
  fmt.Println(text)
 }("Mundo")

 time.Sleep(time.Second * 2)

```

<br>

## Canales

Los canales en Go permiten que las Go routines concurrentes se sincronicen y compartan datos, a continuación se muestra un ejemplo de como crear un canal y como ingresar y extraer datos del canal, algo importante que cabe resaltar es que al extraer un dato de un canal en alguna Go routine, como la que ejecuta main, esta se bloquea hasta que hay un nuevo dato en el canal para ser extraído, de esta forma se logra por ejemplo, que la Go routine de main espera a la Go routine de say.

```go

// Al usar channels en funciones se puede especificar si el canal es de entrada o salida con canal<- o <-canal, respectivamente.

func say(text string, c chan<- string) {

 // Se ingresa el dato al canal.
 c <- text

}

func main() {

 // Creacion del canal, si no se indican el numero de datos que recivira el canal recivira de forma dinamica los datos.

 c := make(chan string, 1)

 fmt.Println("Hello")

 go say("Bye", c)

 // Extrae el dato del canal.

 fmt.Println(<-c)

}

```

Cuando se usan canales se pueden realizar varias acciones, como cerrar el canal con **close** para que no reciba más datos, recorrer los datos del canal con **range** o seleccionar el primer canal en responder con **select**, a continuación se muestra un ejemplo de cómo cerrar y recorrer un canal y de cómo seleccionar el primer canal en responder con select.

```go

func message(text string, c chan<- string) {
 c <- text
}

func main() {

 // Creacion del canal, si no se indican el numero de datos que recivira el canal recivira de forma dinamica los datos.

 c := make(chan string, 2)

 // Insertando datos al canal.

 c <- "Mensaje 1"
 c <- "Mensaje 2"

 // Imprimiendo datos del canal.

 fmt.Println(len(c), cap(c))

 // Close cierra el canal para que no reciva mas datos, lo adecuado es cerrar el canal solo cuando se sepa que no van a insertarse mas datos.

 close(c)

 // Recorriendo canal con range.

 for message := range c {
  fmt.Println(message)
 }

 // Ejemplo de select.

 email1 := make(chan string)
 email2 := make(chan string)

 // Insertando datos a los dos canales.

 go message("mensaje 2", email2)
 go message("mensaje 1", email1)

 // Revisando los canales.

 for i := 0; i < 2; i++ {
  select {
  case m1 := <-email1:
   fmt.Println("Recivido de email1", m1)
  case m2 := <-email2:
   fmt.Println("Recivideo de email2", m2)
  }
 }

}

```

<br>

## Go get

Go al igual que otros lenguajes como Python o JavaScript también cuenta con un manejador de paquetes **go get** el cual permite instalar fácilmente las dependencias necesarias para el proyecto.

```bash

go get -v -u <paquete>

```

<br>

## Modificando módulos con Go

Go posee una interfaz dedicada a la creación y edición de módulos, algunas de las funciones más útiles de esta interfaz se muestran a continuación.

### Iniciar módulos

```bash

go mod init <nombre del módulo>

```

### Editar módulos

```bash

go mod edit --replace <dependencia vieja>=<dependencia nueva>

```

```bash

go mod edit --dropreplace <dependencia vieja>

```

### Verificar módulos

```bash

go mod verify

```

### Empacar módulos

```bash

go mod vendor

```

### Limpiar módulos

```bash

go mod tidy

```

<br>

## Control de errores

Go a diferencia de otros lenguajes de programación no permite la captura de excepciones mediante bloques **try** y **catch** en cambio la captura debe hacerse de forma explícita, lo que hace más difícil la labor de capturar errores, pero da un mayor control sobre el manejo de cada uno de los errores que se puedan presentar durante el runtime de Go, a continuación se muestra un ejemplo sencillo de como capturar un error al realizar un parseo de string a int.

```go

 // Captura del error.

 number, error := strconv.ParseInt("8", 0, 64)

 // Control del error.

 if error != nil {
  fmt.Println(error)
 } else {
  fmt.Println(number)
 }

```

<br>
