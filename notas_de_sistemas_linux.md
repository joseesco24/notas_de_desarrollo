# Sistemas Linux

Los sistemas operativos Linux son sistemas operativos de tipo Unix, que suelen ser de código abierto, multiplataforma, multiusuario y multitarea. Estos sistemas operativos están formados por la combinación de varios proyectos, dentro de los cuales destacan el entorno **GNU**, así como el núcleo del sistema o kernel **Linux**, de ahí la denominación técnica **GNU/Linux** que hace referencia a los dos componentes principales de este tipo de sistemas operativos, a pesar de que cotidianamente se les llame solo sistemas Linux estos sistemas también están formados en una enorme parte por componentes del proyecto GNU, sin embargo, por simple facilidad se les seguirá llamando sistemas Linux en el resto del documento.

<p align="center">
<img src="imagenes/notas_de_sistemas_linux/componentes_principales_de_linux.png" width="40%" height="auto"/>
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

<br><br>

## Comandos Bash

<br><br>

## Scripts Bash

Crear programas en Bash permite ejecutar múltiples comandos de forma secuencial para automatizar tareas específicas. Los comandos de un script Bash son colocados en un archivo de textos de manera secuencial para poder ejecutarlos a posterioridad.

<br>

### Crear un script Bash

Los scripts Bash al igual que cualquier otro tipo de script se crean como archivos de texto plano, sin embargo, al crear un script Bash este debe cumplir dos condiciones, el archivo en el que se guarda el script debe tener la extensión **.sh** y el nombre del script debe ser único para evitar conflictos entre el script nuevo y alguno otro que ya esté presente en el sistema, para garantizar que el nombre del archivo sea único se puede usar el comando **type** como se muestra a continuación, suponiendo que el nombre del script será **script**.

```bash
type script.sh
```

Usando el parámetro -a se pueden ver todos los archivos encontrados.

```bash
type -a script.sh
```

Usando el parámetro -t se puede verificar el tipo de archivo.

```bash
type -t script.sh
```

<br>

### Dar permisos de ejecución a un script Bash

Luego de crear el script es necesario darle al script permisos de ejecución, ya que de otra forma el script no podrá ejecutarse, hay varias formas de dar permisos de ejecución a un script, algunas de estas se listan a continuación.

```bash
# !/bin/bash
```

<br>

### Establecer Bash como intérprete de comandos del script

Antes de empezar a escribir un script Bash en cualquier sistema Linux es necesario indicar que el intérprete del script será Bash, la forma correcta de indicar que el intérprete del script en Bash es agregando la ruta hacia Bash en la primera línea del script, como se muestra a continuación.

```bash
# !/bin/bash
```

<br>

### Declarar variables en scripts Bash

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

### Recuperar variables en scripts Bash

Tras definir cualquier variable de usuario o de entorno lo normal es querer recuperar ese valor posteriormente ya que por lo general se usa para afectar la ejecución del script, en ambos casos para recuperar el valor de una variable se usa el signo "$" antes del nombre de la variable que se quiere recuperar, las variables de usuario solo serán accesibles dentro del script en el que se declararon, mientras que las variables de entorno que fueron definidas con el comando **export** serán accesibles también por otros scripts o mediante la terminal independientemente del usuario del sistema.

Recuperación de una variable de usuario.

```bash
echo $variable_de_usuario
Hola Mundo
```

Recuperación de una variable de entorno.

```bash
echo $VARIABLE_DE_ENTORNO
Hola Mundo
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
