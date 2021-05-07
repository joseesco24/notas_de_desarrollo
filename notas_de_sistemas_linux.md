# Notas de Sistemas Linux

Los sistemas operativos Linux son sistemas operativos de tipo Unix, que suelen ser de código abierto, multiplataforma, multiusuario y multitarea. Estos sistemas operativos están formados por la combinación de varios proyectos, dentro de los cuales destacan el entorno **GNU**, así como el núcleo del sistema o kernel **Linux**, de ahí la denominación técnica **GNU/Linux** que hace referencia a los dos componentes principales de este tipo de sistemas operativos, a pesar de que cotidianamente se les llame solo sistemas Linux estos sistemas también están formados en una enorme parte por componentes del proyecto GNU, sin embargo, por simple facilidad se les seguirá llamando sistemas Linux en el resto del documento.

<p align="center">
<img src="imagenes/notas_de_sistemas_linux/componentes_principales_de_linux.svg" width="40%" height="auto"/>
</p>

Los tres componentes principales de todos los sistemas Linux son:

- **Kernel:** El kernel es el núcleo de cualquier sistema operativo, en el caso de los sistemas Linux el nombre del kernel es Linux, el kernel es el componente del sistema que gestiona todos los recursos de hardware, el acceso seguro a estos y los periféricos conectados al computador.
- **Shell:** El Shell en cualquier sistema basado en Unix, como los sistemas Linux, es el intérprete de comandos del sistema operativo, de forma resumida el Shell es un programa que permite al usuario ejecutar comandos, mediante los cuales se pueden dar instrucciones de forma directa al kernel del sistema operativo, el Shell además permite que los comandos de aplicaciones que trabajan con lenguajes de alto nivel sean procesados y ejecutados en un lenguaje de bajo nivel, permitiendo así que estas aplicaciones interactúen con el kernel.
- **Aplicaciones:** Las aplicaciones son los programas con los que se interactúa para realizar alguna actividad en concreto, en los sistemas Linux toda aplicación por debajo estas ejecutan acciones directamente en el kernel.

En los sistemas Linux existen varios tipos de shell de las cuales el usuario puede decidir cual usar, algunos de estos son:

1. **CSH:** En una shell diseñada para que los usuarios puedan escribir programas de scripting de shell con una sintaxis muy similar a la de C. En muchos sistemas como Red Hat, csh es tcsh, una versión mejorada de csh.
1. **SH:** También conocida como Shell Bourne, fue la primera shell creada para un sistema operativo Linux, se puede utilizar actualmente, pero no tiene funcionalidades como autocompletar archivos o guardar un historial de comandos.
1. **BASH:** También conocida como Shell Bourne-Again, es una versión actualizada de SH creada por la Free Software Foundation, es una de las shell más utilizadas y conocidas en el mundo, sin mencionar que es la shell por defecto que usan muchos de los sistemas Linux. Bash Incorpora alguna de las funcionalidades más avanzadas de KSH, CSH, SH y TCSH. Una de la funcionalidades más destacables de esta shell es la opción de ejecutar múltiples programas en segundo plano a la vez.
1. **ZSH:** Es una de las shell más potentes actualmente, puede funcionar como shell interactiva y como intérprete de lenguaje de scripting. aún siendo compatible con Bash.

<br>

## Tabla de contenidos

- [**Comandos Bash**](#comandos-bash)
  - [Comandos básicos](#comandos-básicos)
  - [Comandos de compresión de archivos](#comandos-de-compresión-de-archivos)
- [**Scripts Bash**](#scripts-bash)
  - [Crear un script Bash](#crear-un-script-bash)
  - [Otorgar permisos de ejecución al script](#otorgar-permisos-de-ejecución-al-script)
  - [Establecer Bash como intérprete del script](#establecer-bash-como-intérprete-del-script)
  - [Declaración de variables en Bash](#declaración-de-variables-en-bash)
  - [Lectura de variables en Bash](#lectura-de-variables-en-bash)
  - [Sustitución de comandos en variables en Bash](#sustitución-de-comandos-en-variables-en-bash)
  - [Capturar entradas del usuario en Bash](#capturar-entradas-del-usuario-en-bash)
  - [Operadores aritméticos en Bash](#operadores-aritméticos-en-bash)
  - [Operadores relacionales en Bash](#operadores-relacionales-en-bash)
  - [Operadores de asignación en Bash](#operadores-de-asignación-en-bash)
  - [Manejo de secuencias en Bash](#manejo-de-secuencias-en-bash)
  - [Manejo de arreglos en Bash](#manejo-de-arreglos-en-bash)
  - [Manejo de tablas en Bash](#manejo-de-tablas-en-bash)
  - [Condicionales con if y else en Bash](#condicionales-con-if-y-else-en-bash)
  - [Validación de entradas del usuario con condicionales if y regex en Bash](#validación-de-entradas-del-usuario-con-condicionales-if-y-regex-en-bash)
  - [Condicionales con case en Bash](#condicionales-con-case-en-bash)
  - [Ciclos while en Bash](#ciclos-while-en-bash)
  - [Ciclos for en Bash](#ciclos-for-en-bash)
  - [Sentencias break y continue en Bash](#sentencias-break-y-continue-en-bash)
  - [Ejecutar un script Bash](#ejecutar-un-script-bash)
  - [Manejo de argumentos en Bash](#manejo-de-argumentos-en-bash)
  - [Creación de funciones en Bash](#creación-de-funciones-en-bash)
  - [Manejo de opciones en Bash](#manejo-de-opciones-en-bash)
  - [Depuración en Bash](#depuración-en-bash)
  - [Lectura de archivos con Bash](#lectura-de-archivos-con-bash)
  - [Escritura de archivos con Bash](#escritura-de-archivos-con-bash)

<br>

## Comandos Bash

Los comandos Bash son un conjunto de instrucciones y parámetros utilizados para la administración y configuración de los sistemas Linux, además de para realizar otras tareas específicas relacionadas con el sistema operativo.

<br>

### Comandos básicos

<br>

### Comandos de compresión de archivos

<br>

## Scripts Bash

Bash no es solamente un shell o intérprete de comandos con el que se interactúa mediante una terminal y que permite dar instrucciones al kernel del sistema operativo, Bash también es un lenguaje de de programación interpretado completo que permite crear programas que ejecutan múltiples comandos de forma secuencial para automatizar tareas específicas dentro del sistema operativo, Bash como lenguaje de programación tiene la ventaja de ser compatible con casi cualquier sistema operativo basado en Linux, ya que es el shell por defecto de la gran mayoría de este tipo de sistemas, lo que lo hace un lenguaje de programación extremadamente útil para crear programas de automatización de tareas en sistemas operativos con kernel Linux, la principal característica de este lenguaje es que al programar con el se puede usar cualquier comando que normalmente se ingresaría en una terminal, lo que le da una gran potencia y usabilidad, agregando a esto la sintaxis propia de Bash, que es muy similar a la de otros lenguajes de programación, los programas en Bash llegan a ser fáciles de escribir y pueden ser muy útiles y polivalentes.

<br>

### Crear un script Bash

Los scripts Bash al igual que cualquier otro tipo de script se crean como archivos de texto plano, la unica condicion que deben respetar los scripts Bash al igual que los scripts de los demás lenguajes de programacion es la extensión del archivo, que en el caso de Bash debe ser **sh**.

```bash
touch nuevo_script.sh
```

<br>

### Otorgar permisos de ejecución al script

Para poder ejecutar un script Bash es necesario darle al script permisos de ejecución, al igual que con cualquier otro tipo de script, ya que de otra forma el script no podrá ejecutarse, algunas de las formas más sencillas de dar permiso de ejecución a un script se listan a continuación.

Otorgacion de permisos de ejecución usando el sistema octal.

```bash
chmod 755 nuevo_script.sh
```

Otorgación de permisos de ejecución usando sintaxis simplificada.

```bash
chmod +x nuevo_script.sh
```

<br>

### Establecer Bash como intérprete del script

Antes de empezar a escribir cualquier programa interpretado ejecutabe en un sistema Linux es necesario establecer el intérprete del programa, la forma más sencilla de establecerlo es mediante la secuancia de caracteres **#!** también conocida como **Shebang** seguida por la ruta del intérprete del programa, en el caso de los scripts Bash se puede establecer que el script es será interpretado por Bash de la siguiente forma.

```bash
# !/bin/bash
```

Luego de declarar el intérprete en el **Shebang** se puede incluir el siguiente comando para que el programa se detenga si cualquier operación que realice falla.

```bash
set -e
```

<br>

### Declaración de variables en Bash

Las variables que puede usar un script Bash pueden ser de dos tipos, **variables de usuario** y **variables de entorno**. Las variables de usuario son variables que son accesibles sólo dentro de un programa específico, mientras que las de entorno son variables que son accesibles en todo el sistema, por todos los usuarios del sistema. En ambos casos las variables se definen iniciando con el nombre de la variable y no hace falta definir el tipo de dato de la variable, con la diferencia de que las variables de usuario por lo general se definen con todas las letras del nombre de la variable en minúsculas mientras que las de entorno se definen por lo general con todas las letras del nombre en mayúsculas.\
Para declarar que una variable dentro de un script será una variable de entorno hace falta, además, de definir la variable y su valor usar el comando **export**, con esta instrucción la variable pasa de ser de usuario a ser de entorno, por lo que inmediatamente después del comando **export** la variable ya es accesible por todo el sistema y por todos los usuarios del sistema.

Declaración de una variable de usuario en un script Bash.

```bash
variable_de_usuario="Hola Mundo"
```

Declaración de una variable de entorno en un script Bash.

```bash
VARIABLE_DE_ENTORNO="Hola Mundo"
export VARIABLE_DE_ENTORNO
```

<br>

### Lectura de variables en Bash

Tras definir cualquier variable de usuario o de entorno lo normal es querer leer ese valor posteriormente ya que por lo general se usa para afectar la ejecución del script, en ambos casos para leer el valor de una variable se usa el signo **$** antes del nombre de la variable que se quiere leer, las variables de usuario solo serán accesibles dentro del script en el que se declararon, mientras que las variables de entorno que fueron definidas con el comando **export** serán accesibles también por otros scripts o mediante la terminal, independientemente del usuario del sistema que la quiera leer.

Lectura de una variable de usuario.

```bash
echo $variable_de_usuario
Hola Mundo
```

Lectura de una variable de entorno.

```bash
echo $VARIABLE_DE_ENTORNO
Hola Mundo
```

<br>

### Sustitución de comandos en variables en Bash

La sustitución de comandos en variables es uno de los mecanismos más útiles de Bash ya que permite ejecutar un comando y almacenar el resultado de la ejecución de forma textual en una variable o incluso reemplazarlo e imprimirlo en un texto. Las dos formas de sustituir comandos en variables se muestran a continuación.

Sustitución de comandos usando comillas.

```bash
ubicacionActual=`pwd`
```

Sustitución de comandos usando parentesis.

```bash
ubicacionActual=$(pwd)
```

<br>

### Capturar entradas del usuario en Bash

La captura de entradas del usuario es un proceso fundamental para desarrollar programas Bash interactivos, es decir, programas que cambian su ejecución o sus procesos en función de cierta información que es suministrada al programa por el usuario mediante la línea de comandos durante su ejecución, para capturar entradas del usuario en un script Bash se usa el comando **read**, las entradas capturadas por read se almacenen en la variable **REPLY** por defecto, este comportamiento se puede modificar con el parámetro **-p** de read, el cual emite una frase para pedir al usuario la entrada y además guardar la entrada suministrada en una variable específica. Las dos formas de capturar entradas del usuario con read se muestra a continuación.

Captura con read sin usar parámetros adicionales.

```bash
echo -n "Ingrese el valor 1:"
read
valor_1=$REPLY
echo -n "Ingrese el valor 2:"
read
valor_2=$REPLY
```

Captura con read usando el parámetro -p.

```bash
read -p "Ingrese el valor 1:" valor_1
read -p "Ingrese el valor 2:" valor_1
```

Algunos de los parámetros más utilizados junto a read son:

- **-p:** Permite ingresar una frase o prompt antes de pedir una entrada.
- **-s:** Modo Sigiloso. No muestra ningún carácter en la terminal, útil para contraseñas o información sensible.
- **-n [número de caracteres]:** Permite leer como máximo cierto número de caracteres.
- **-r:** Toma el botón de retroceso o backspace como un carácter y no borra ningún otro carácter previamente escrito.

<br>

### Operadores aritméticos en Bash

Asumiendo que se definen dos variables numA y numB las operaciones aritméticas básicas en Bash se definen de la siguiente forma.

```bash
numA=4
numB=10
```

Suma.

```bash
resultado=$((numA+numB))
```

Resta.

```bash
resultado=$((numA-numB))
```

Multiplicación.

```bash
resultado=$((numA*numB))
```

División.

```bash
resultado=$((numA/numB))
```

Residuo.

```bash
resultado=$((numA%numB))
```

<br>

### Operadores relacionales en Bash

Asumiendo que se definen dos variables numA y numB las operaciones relacionales básicas en Bash se definen de la siguiente forma.

```bash
numA=4
numB=10
```

Operador mayor.

```bash
resultado=$((numA>numB))
resultado=$((numA -gt numB))
```

Operador menor.

```bash
resultado=$((numA<numB))
resultado=$((numA -lt numB))
```

Operador mayor o igual.

```bash
resultado=$((numA>=numB))
resultado=$((numA -ge numB))
```

Operador menor o igual.

```bash
resultado=$((numA<=numB))
resultado=$((numA -le numB))
```

Operador igual.

```bash
resultado=$((numA==numB))
resultado=$((numA -eq numB))
```

Operador diferente.

```bash
resultado=$((numA!=numB))
resultado=$((numA -ne numB))
```

<br>

### Operadores de asignación en Bash

Asumiendo que se definen dos variables numA y numB las operaciones de asignación básicas en Bash se definen de la siguiente forma.

```bash
numA=4
numB=10
```

Sumar a numA numB.

```bash
resultado=$((numA+=numB))
```

Restar a numA numB.

```bash
resultado=$((numA-=numB))
```

Multiplicar a numA por numB.

```bash
resultado=$((numA*=numB))
```

Dividir a numA entre numB.

```bash
resultado=$((numA/=numB))
```

Residuo de numA entre numB.

```bash
resultado=$((numA%=numB))
```

<br>

### Manejo de secuencias en Bash

Las secuencias en Bash son listas en las que todos los elementos de la lista sigue un cierto patrón, como por ejemplo en un conteo del 1 al 10, en el que los valores incrementan de 1 en 1, la forma más sencilla de declarar una secuencia es usando la notación basada en llaves, las secuencias con notación de llaves pueden ser reemplazadas en cadenas usando expansión de llaves para generar cadenas nuevas y además adicionando un tercer elemento en el caso de las secuencias numéricas puede agregarse un paso. Usando notación de llaves también se pueden generar secuencias alfabéticas con la notación de llaves.

Generación de una secuencia simple del 1 al 10.

```bash
echo {1..10}
1 2 3 4 5 6 7 8 9 10
```

Generación de una secuencia con paso 2 del 1 al 10.

```bash
echo {1..10..2}
1 3 5 7 9
```

Generación de una secuencia de nombres usando reemplazo por expansión de llaves.

```bash
echo archivo_{1..4}.sh
archivo_1.sh archivo_2.sh archivo_3.sh archivo_4.sh
```

Generación de una secuencia simple de caracteres alfabeticos.

```bash
echo {a..f}
a b c d e f
```

<br>

### Manejo de arreglos en Bash

En Bash los arreglos pueden contener cualquier tipo de dato y además puede haber más de un tipo de dato por arreglo, los arreglos en Bash también tienen la característica de ser dinámicos, es decir que incluso luego de establecer ciertos datos dentro del arreglo este puede seguir aumentando o disminuyendo sin ningún inconveniente.

Declarar valores de un arreglo.

```bash
arreglo_numeros=(1 2 3 4 5 6 7 8)
arreglo_cadenas=(perro, gato)
arreglo_rangos=({A…Z} {10…20})
```

Imprimir valores de un arreglo.

```bash
echo -e "arreglo de números: ${arreglo_numeros[*]}"
echo -e "arreglo de cadenas: ${arreglo_cadenas[*]}"
echo -e "arreglo mixto generado con rangos: ${arreglo_rangos[*]}"
```

Imprimir tamaño de un arreglo.

```bash
echo -e "tamaño del arreglo de números: ${#arreglo_numeros[*]}"
echo -e "tamaño del arreglo de cadenas: ${#arreglo_cadenas[*]}"
echo -e "tamaño del arreglo mixto generado con rangos: ${#arreglo_rangos[*]}"
```

Imprimir índices de un arreglo.

```bash
echo -e "posición 0  del arreglo de números: ${arreglo_numeros[0]}"
echo -e "posición 1  del arreglo de cadenas: ${arreglo_cadenas[1]}"
echo -e "posición 2  del arreglo mixto generado con rangos: ${arreglo_rangos[2]}"
```

Agregar valores a un arreglo.

```bash
arreglo_numeros[0]=9
arreglo_cadenas[0]=cabra
arreglo_rangos[0]=11
```

Eliminar valores de un arreglo.

```bash
unset arreglo_numeros[0]
unset arreglo_cadenas[0]
unset arreglo_rangos[0]
```

<br>

### Manejo de tablas en Bash

En sus versiones más recientes Bash soporta el uso de tablas o diccionarios, los cuales se basan en usar una llave para acceder a un valor, la forma de declarar un diccionario en Bash es la siguiente.

```bash
declare -A ppa_instalations=(
    ["indicator-sysmonitor"]="ppa:fossfreedom/indicator-sysmonitor"
    ["timeshift"]="ppa:teejee2008/timeshift"
    ["neofetch"]="ppa:dawidd0811/neofetch"
    ["tilix"]="ppa:ubuntuhandbook1/tilix"
    ["python3.7"]="ppa:deadsnakes/ppa"
)
```

Imprimir todas las llaves de la tabla.

```bash
echo -e "Llaves en la tabla ${!ppa_instalations[*]}"
```

Imprimir todos los ítems de la tabla.

```bash
echo -e "Ítems en la tabla ${ppa_instalations[*]}"
```

Imprimir un ítem de la tabla basándose en su llave.

```bash
echo -e "Ítems basado en la llave ${ppa_instalations[llave]}"
```

<br>

### Condicionales con if y else en Bash

Los condicionales if else en Bash tienen la particularidad de que al usar **if** o **elif** siempre la sentencia del condicional debe ir entre corchetes y además debe haber un espacio entre los corchetes y la sentencia del condicional al iniciar y finalizar.

```bash
if [ condicion_1 ]; then
    echo -e "Se cumplio condicion_1"
elif [ condicion_2 ]; then
    echo -e "Se cumplio condicion_2"
elif [ condicion_3 ] && [ condicion_4 ]; then
    echo -e "Se cumplieron condicion_3 y condicion_4"
else
    echo -e "No se cumplieron ni condicion_1 ni condicion_2"
fi
```

**Nota:** Cuando se comparan dos números se utiliza el operador relacional **==**, cuando se comparan cadenas se utiliza **=**.

<br>

### Validación de entradas del usuario con condicionales if y regex en Bash

Para validar que los datos ingresados por el usuario sean datos de cierto tipo en Bash es necesario hacer una comprobación de datos usando expresiones regulares, además, para comparar la entrada con la expresión regular se debe utilizar el siguiente formato especial **if [[$variable =~ $expresionRegular]]**.

```bash
id_regex='^[0-9]{10}$'
read -p "ID: " u_id

if [[ $u_id =~ $id_regex ]]; then
    echo -e "Id válida"
else
    echo -e "Id no válida"
fi
```

<br>

### Condicionales con case en Bash

Las sentencias case en Bash son muy similares a la sentencia switch de otros lenguajes de programación, permite evaluar varios casos para un valor simple o un rango de valores.

```bash
case "$var" in
"A")
    echo "opción A"
    echo "linea dos de la opción A"
    ;;
"B") echo "opción B";;
"C") echo "opción C";;
"D") echo "opción D";;
{E..G}) echo "la opción aún no está implementada"
*) echo "opcion no encontrada";;
esac
```

<br>

### Ciclos while en Bash

Los ciclos while en Bash al igual que en otros lenguajes de programación permiten ejecutar una secuencia de comandos mientras no se cumpla una condición dada.

```bash
numero=1
while [ $numero -le 20 ]
do
      numero=$(( numero + 1 ))
done
```

<br>

### Ciclos for en Bash

Los ciclos for en Bash al igual que en otros lenguajes de programación permiten iterar sobre una listas de valores o ejecutar una secuencia de comandos cierto número de veces.

Iteración de ciclo for sobre lista de valores.

```bash
arreglo_numeros=(1 2 3 4 5 6 7 8)
for i in ${arreglo_numeros[*]}
do
    echo "Número: $i"
done
```

Iteración de ciclo for n veces.

```bash
for ((i=1; i<10; i++))
do
    echo "Número: $i"
done
```

<br>

### Sentencias break y continue en Bash

En Bash las sentencias **break** rompen los ciclos, mientras que las sentencias **continue** hacen que los ciclos pasen a la siguiente iteración omitiendo el resto de instrucciones en la secuencia que hay por ejecutar en la iteración actual.

```bash
break;
```

```bash
continue;
```

<br>

### Ejecutar un script Bash

Las dos formas de ejecutar un Script Bash en Linux son:

```bash
bash script.sh
```

```bash
./script.sh
```

<br>

### Manejo de argumentos en Bash

Los argumentos que son enviados a un script Bash se almacenan en una lista, donde cada argumento puede ser referenciado mediante su posición, para enviar argumentos basta con escribir cada argumento luego de la instrucción de ejecución del script con un espacio, cuando se quieren enviar cadenas como parámetros es necesario enviar la cadena entre comillas ya que si la cadena tiene espacios y no es enviada entre comillas será interpretada por el script como varios parámetros.

```bash
bash script.sh "primer argumento" 2
```

```bash
./script.sh "primer argumento" 2
```

Para acceder a un argumento de la lista de argumentos se debe usar el signo **$** y el número del argumento, el cual debe ser mayor a cero y menor a diez, si el número del argumento es de un solo dígito (0<n<10) no hace falta usar llaves, si el número del argumento es de más de un dígito (n>=10) es necesario usar llaves antes de indicar el número del argumento.

```bash
$1
```

```bash
${10}
```

Además de poder acceder por número de argumento se pueden usar ciertas instrucciones para obtener más información respecto a los parámetros recibidos por el script.

Obtener el nombre del script.

```bash
$0
```

Obtener el conteo de los argumentos.

```bash
$#
```

Obtener todos los argumentos

```bash
$*
```

<br>

### Creación de funciones en Bash

En Bash como en cualquier lenguaje de programación interpretado es necesario que las funciones se definen antes de llamarlas, ya que de otra forma la función no existirá en memoria al momento de llamarla.

```bash
nueva_funcion () {
    echo -e "Hola desde la nueva función"
    ...
}
```

```bash
nueva_funcion
```

Al enviar parámetros a una función ésta accede a los parámetros por índices, como si se tratara del listado de parametros que recibe un script Bash al iniciar su ejecución.

```bash
nueva_funcion_a () {
    echo -e "Hola desde la nueva función, el argumento recibido es $1"
    ...
}
```

```bash
nueva_funcion_a "argumento_1"
```

<br>

### Manejo de opciones en Bash

Las opciones en los scripts Bash se usan para modificar el funcionamiento del script, por lo que son sumamente importantes. Las opciones en Bash son antecedidas por un **-**, también se puede usar la notación **--** pero en este caso Bash lo interpretará como una cadena. Para validar opciones en scripts Bash es necesario que los scripts internamente iteren sobre el listado de todos los argumentos que reciben en busca de las opciones definidas.

```bash
for var in "$*"; do
    case "$var" in
    "--all") echo "opción --all";;
    -a) echo "opción -a";;
    -b) echo "opción -b";;
    -c) echo "opción -c";;
    *) echo "opcion no encontrada";;
    esac
    shift
done
```

<br>

### Depuración en Bash

La depuración es el proceso de identificar y corregir errores de programación. Bash provee ciertos comandos que permiten ejecutar un script al tiempo que emite los resultados del mismo en la línea de comandos separando los comandos de sus salidas.

Las dos formas de hacer depuración en Bash son:

```bash
bash -v script.sh
```

```bash
bash -x script.sh
```

<br>

### Lectura de archivos con Bash

La lectura de archivos suele ser algo normal al programar en Bash, normalmente se emplea el comando cat para leer archivos, pero en caso de necesitar leer line a línea se usa la palabra reservada **IFS** con un while para iterar sobre las líneas del archivo.

Lectura normal con cat.

```bash
cat archivo.txt
```

Lectura normal con cat y sustitución de variable.

```bash
contenido = $(cat archivo.txt)
```

Lectura linea a linea con IFS y while.

```bash
while IFS= read linea
do
    echo "$linea"
done < archivo.txt
```

<br>

### Escritura de archivos con Bash

Para escribir en archivos desde Bash se puede usar dos opciones, el operador **>** junto a echo o **EOM**: End Of Message y **EOF**: End Of File junto a cat, la principal ventaja de usar EOM o EOF respecto al operador >> es que tanto EOM como EOF permiten escribir múltiples líneas directamente, mientras que con el operador >> sería necesario iterar para escribir múltiples líneas.

```bash
echo "valores escritos con echo" > archivo.txt
```

```bash
cat <<EOM > archivo.txt
valores escritos
con cat
EOM
```

<br>
