# Git y GitHub

[**Git**](https://git-scm.com/) es el sistema de control de versiones más popular actualmente, Git permite guardar el historial de cambios y el crecimiento de los archivos de un proyecto de forma atómica e incremental, por lo que cada cambio se escribe sobre el anterior y así sucesivamente desde la versión inicial hasta la final, lo que hace posible ver la evolución de los archivos con cada actualización sin almacenar cada versión completa, GitHub por su parte permite que este versionamiento además se haga en una nube dedicada al versionamiento de archivos, y además permite trabajo colaborativo sobre los archivos de un proyecto.\
Git soporta versionamiento de archivos binarios, pero el versionamiento no es tan preciso como con archivos basados en texto plano, por lo que normalmente se utilizan Git y GitHub solo para archivos de texto plano, como el código.

## Comandos básicos Git

Cuando se versionan archivos con Git estos pueden estar almacenados en tres posibles áreas, la primera es el **directorio de trabajo**, que simplemente es el directorio dentro de la máquina local en el que se inició el repositorio, la segunda área es el **área de staging**, que es un área de almacenamiento en la ram de la máquina local donde se preparan los cambios para ser agregados al repositorio y por ultimo esta el **repositorio**, que es un área de almacenamiento local o remota donde se guardan los archivos y se registran sus respectivos cambios a través de cada versión, dependiendo del nivel en el que esté un cambio este se puede considerar como **no rastreado** cuando solo está presente en el **directorio de trabajo**, **en espera** cuando está presente en el **directorio de trabajo** y el **área de staging** y **rastreado** cuando pasa a estar en **las tres áreas** luego de ser subido al **repositorio**, algunos de los conceptos más útiles al trabajar con Git de forma básica son:

- **commit:** Un commit es lo que sucede cuando un cambio pasa del área de staging al repositorio, es decir que pasa de estra **en espera** a estar **rastreado**, al ser aceptado un cambio como una nueva versión, a la cual se le asigna un numero de version o Id que identifica esa nueva versión basada en los últimos cambios, y además se registran otros metadatos como la fecha, hora y el usuario que hizo el commit, por lo que cada cambio en Git es rastreable por su Id y por los otros metadatos como la fecha o la hora, que son almacenados al hacer el commit.
- **HEAD:** Los archivos del HEAD corresponden con los últimos cambios rastreados por el repositorio mediante un commit.

### Mostrar comandos populares de git

```bash
git
```

Muestra algunos de los comandos más comunes usados en git junto con sus respectivas descripciones.

### Mostrar ayuda de un comando

```bash
git [comando] --help
```

Muestra los parámetros que acepta un comando, además de una breve descripción de la función del comando, si no se incluye un comando antes de **--help** es equivalente a **git**.

### Configuración de Git

```bash
git config [parámetros] [configuraciones]
```

Permite aplicar ciertas configuraciones a un repositorio, algunos de los parámetros más útiles al utilizar **git config** para configurar un repositorio son:

- **--global:** Indica a Git que esa configuración será aplicada a todos los repositorios de la máquina.
- **--list:** Muestra la configuración actual del repositorio.

Algunos de los parámetros configurables más importantes de un repositorio son:

- **user.email=[correo del usuario]:** Cambia el correo electrónico del usuario.
- **user.name=[nombre del usuario]:** Cambia el nombre del usuario.

### Iniciar un repositorio

```bash
git init [parámetros]
```

Inicia un repositorio git en el directorio actual.

### Agregar archivos al área de staging del repositorio

```bash
git add [parámetros] [ruta del archivo o directorio]
```

Inicia el rastreo de uno o varios archivos agregandolos al área de staging del repositorio. Lo más normal es usar **.** como ruta para rastrear y agregar todos los archivos de la carpeta actual al área de staging.

### Registrar cambios en el repositorio

```bash
git commit [parámetros]
```

Envía los últimos cambios desde el área de staging al repositorio para que este los registre en su base de datos de cambios, creando así una nueva versión de uno o varios archivos basándose en los últimos cambios realizados, solo cuando se realiza un commit se asigna al cambio un número de commit y los cambios realizados en un archivo son visibles para todos en el repositorio, y por defecto el commit se realiza sobre la rama **master** si no se indica otra rama, algunos de los parámetros más útiles al utilizar **git commit** para enviar los cambios del área de staging al repositorio son:

- **--message "[comentario]":** Permite agregar un mensaje al commit, idealmente todos los commits deben tener un mensaje que describa los cambios que se realizan en el commit para facilitar la compresión del versionamiento y los cambios hechos.

### Comprobar el estatus de cambios del repositorio

```bash
git status
```

Muestra el estatus de la base de datos de cambios del repositorio.

### Mostrar los cambios de un archivo o repositorio

```bash
git show [archivo]
```

Muestra todos los cambios históricos hechos en el repositorio o en un archivo, centrándose en las líneas en las que se hicieron cambios, cuando se hicieron y quién los hizo.

### Mostrar los logs de un archivo o repositorio

```bash
git log [archivo]
```

Muestra todos los cambios históricos hechos en el repositorio o en un archivo, centrándose en el histórico de los cambios, sus fechas y comentarios.

### Comparación de versiones

```bash
git diff [parámetros] [commit antiguo] [commit nuevo]
```

Muestra los cambios entre una versión y otra de un archivo usando los Id de los diferentes commit.

### Eliminar archivos del repositorio

```bash
git rm [parámetros] [archivo]
```

Elimina uno o varios archivos del área de staging o del repositorio, **git rm** necesita alguno de los siguientes parámetros para ejecutarse correctamente:

- **--force:** Elimina los archivos del repositorio y del disco duro. el repositorio guarda el registro de la existencia de los archivos, por lo que pueden ser recuperados de ser necesario.
- **--cached:** Elimina uno o varios archivos del área de staging, por lo que para pasarlos al repositorio hará falta volver a moverlos al área de staging antes.

Algunos de los parámetros opcionales más útiles al utilizar **git rm** para eliminar archivos del área de staging o del repositorio son:

- **-r:** Habilita la remoción recursiva cuando le es dado el nombre de un directorio.

## Comandos para administrar ramas y versiones de Git

Las ramas permiten dividir el código de una aplicación en diferentes líneas separadas cronológicamente que luego se unen para formar una sola aplicación, por defecto Git trabaja sobre la rama **master** pero normalmente cuando se trabaja en un equipo de desarrollo se utilizan diferentes ramas para que diferentes miembros del equipo trabajen en simultáneo en diferentes partes o funcionalidades de una misma aplicación, algunos de los conceptos más útiles al trabajar con ramas de Git son:

- **merge:** Un merge es una operación que se realiza cuando se une el código de dos ramas diferentes para generar una nueva versión.
- **conflicto:** Un conflicto es lo que sucede cuando al realizar un merge los cambios de una rama dañan el funcionamiento de la otra rama, por lo que la nueva versión no funciona correctamente, o simplemente los cambios son incompatibles, por lo que no se puede realizar el merge correctamente.

### Moverse entre ramas y versiones

```bash
git checkout [parametros] [rama|commit]
```

Permite traer temporalmente los cambios de una rama, commit o archivo de una versión específica al directorio de trabajo.
