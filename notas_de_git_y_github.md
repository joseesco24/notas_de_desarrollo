# Notas De Git Y Github

- [Introducción](#introducción)
- [Flujo De Trabajo Básico Con Git](#flujo-de-trabajo-básico-con-git)
  - [Mostrar Comandos Populares De Git](#mostrar-comandos-populares-de-git)
  - [Inspeccionar Un Comando De Git](#inspeccionar-un-comando-de-git)
  - [Configuración De Git](#configuración-de-git)
  - [Iniciar O Finalizar Un Repositorio](#iniciar-o-finalizar-un-repositorio)
  - [Agregar Archivos Al Área De Staging Del Repositorio](#agregar-archivos-al-área-de-staging-del-repositorio)
  - [Registrar Cambios En El Repositorio](#registrar-cambios-en-el-repositorio)
  - [Comprobar El Estatus De La Base De Datos De Cambios Del Repositorio](#comprobar-el-estatus-de-la-base-de-datos-de-cambios-del-repositorio)
  - [Comparar Cambios Entre Versiones Del Repositorio](#comparar-cambios-entre-versiones-del-repositorio)
  - [Mostrar Los Logs Del Repositorio](#mostrar-los-logs-del-repositorio)
  - [Mostrar Los Logs Completos Del Repositorio](#mostrar-los-logs-completos-del-repositorio)
  - [Mostrar Los Cambios Del Repositorio](#mostrar-los-cambios-del-repositorio)
  - [Limpiar El Directorio De Trabajo](#limpiar-el-directorio-de-trabajo)
  - [Eliminar Archivos Del Repositorio](#eliminar-archivos-del-repositorio)
- [Administración De Ramas Y Versiones Con Git](#administración-de-ramas-y-versiones-con-git)
  - [Administrar Ramas](#administrar-ramas)
    - [Crear Ramas](#crear-ramas)
    - [Listar Ramas](#listar-ramas)
    - [Eliminar Ramas](#eliminar-ramas)
    - [Parámetros Adicionales](#parámetros-adicionales)
  - [Fusionar Ramas](#fusionar-ramas)
  - [Moverse Entre Ramas Y Versiones](#moverse-entre-ramas-y-versiones)
    - [Moverse Entre Versiones](#moverse-entre-versiones)
    - [Moverse Entre Ramas](#moverse-entre-ramas)
  - [Hacer Rebase A Una Rama](#hacer-rebase-a-una-rama)
  - [Administrar La Reserva De Cambios De Git](#administrar-la-reserva-de-cambios-de-git)
  - [Administrar Tags](#administrar-tags)
    - [Crear Tags](#crear-tags)
    - [Listar Tags](#listar-tags)
    - [Eliminar Tags](#eliminar-tags)
  - [Traer A Una Rama Cambios Viejos De Otra](#traer-a-una-rama-cambios-viejos-de-otra)
  - [Regresar A Versiones Anteriores Del Repositorio](#regresar-a-versiones-anteriores-del-repositorio)
- [Administración De Repositorios Remotos Con Git Y Github](#administración-de-repositorios-remotos-con-git-y-github)
  - [Administrar Repositorios Remotos](#administrar-repositorios-remotos)
    - [Agregar Repositorio Remoto Al Repositorio Local](#agregar-repositorio-remoto-al-repositorio-local)
  - [Cambiar La Url De Un Repositorio Remoto](#cambiar-la-url-de-un-repositorio-remoto)
  - [Clonar Un Repositorio Remoto](#clonar-un-repositorio-remoto)
  - [Traer Los Cambios Del Repositorio Remoto Al Repositorio Local](#traer-los-cambios-del-repositorio-remoto-al-repositorio-local)
  - [Traer Los Cambios Repositorio Remoto Al Repositorio Local Y Al Directorio De Trabajo](#traer-los-cambios-repositorio-remoto-al-repositorio-local-y-al-directorio-de-trabajo)
  - [Subir Cambios Del Repositorio Local Al Repositorio Remoto](#subir-cambios-del-repositorio-local-al-repositorio-remoto)
- [Conexión Con Github Usando Protocolo Ssh](#conexión-con-github-usando-protocolo-ssh)
  - [Crear El Par De Llaves](#crear-el-par-de-llaves)
  - [Comprobar Funcionamiento Del Servidor Ssh](#comprobar-funcionamiento-del-servidor-ssh)
  - [Agregar Llave Al Servidor Ssh](#agregar-llave-al-servidor-ssh)
  - [Agregar A Github La Llave Pública](#agregar-a-github-la-llave-pública)
  - [Cambiar La Url Del Repositorio Remoto Para Usar La Conexión Ssh](#cambiar-la-url-del-repositorio-remoto-para-usar-la-conexión-ssh)
- [Pull Requests Con Github](#pull-requests-con-github)
- [Forks Con Github](#forks-con-github)
- [Uso De Archivos Gitignore Con Git Y Github](#uso-de-archivos-gitignore-con-git-y-github)

<br>

## Introducción

[**git**](https://git-scm.com/doc) es el sistema de versionamiento más usado en la industria del desarrollo de software en general, git permite guardar el historial de cambios y el crecimiento de los archivos de un proyecto de forma atómica e incremental, por lo que cada cambio se escribe sobre el anterior y así sucesivamente desde la versión inicial hasta la más reciente, lo que hace posible registrar la evolución de los archivos con cada actualización sin almacenar los archivos de cada versión en su totalidad, para esto git emplea al interior de cada repositorio una base de datos que guarda los cambios de forma incremental, la cual se actualiza con cada versión nueva que llega al repositorio.\
[**github**](https://docs.github.com/es) por su parte es el sistema de versionamiento remoto más usado en la industria del desarrollo de software en general, github permite trabajo colaborativo sobre los archivos de un repositorio remoto, además de permitir publicar proyectos y su progreso, entre otras de sus funciones.\
git y github soportan versionamiento de archivos binarios, pero el versionamiento de archivos binarios no es tan preciso como con archivos basados en texto plano, por lo que normalmente se utilizan git y github solo para archivos de texto plano, como el código.

<br>

## Flujo De Trabajo Básico Con Git

<p align="center">
<img src="imagenes/notas_de_git_y_github/flujo_basico_con_repositorios_locales_git.svg" width="100%" height="auto"/>
</p>

cuando se versionan archivos con repositorios git locales los cambios pueden estar almacenados en tres posibles áreas, la primera es el **directorio de trabajo**, que simplemente es el directorio dentro de la máquina local en el que se inició el repositorio, la segunda área es el **área de staging**, que es un área de almacenamiento en la ram de la máquina local donde se preparan los cambios para ser agregados al repositorio y por ultimo esta el **repositorio**, que es un área de almacenamiento local o remota donde se guardan los archivos y se registran sus respectivos cambios a través de cada versión, dependiendo del nivel en el que esté un cambio este se puede considerar como **no rastreado** cuando solo está presente en el **directorio de trabajo**, **en espera** cuando está presente en el **directorio de trabajo** y el **área de staging** y **rastreado** cuando pasa a estar en **las tres áreas** luego de ser enviado del **área de staging** al **repositorio**, algunos de los conceptos más útiles al trabajar con git de forma básica son:

- **commit:** un commit es lo que sucede cuando un cambio pasa del área de staging al repositorio, es decir que pasa de estra **en espera** a estar **rastreado** por la base de datos de cambios del repositorio, al ser aceptado un cambio como una nueva versión con un commit, git le asigna un número de versión o id que identifica esa nueva versión, y además se registran otros metadatos como la fecha, hora y el usuario que hizo el commit, por lo que cada cambio en git es rastreable por su id y por los otros metadatos que son almacenados al hacer el commit.
- **HEAD:** es la última versión rastreada por el repositorio mediante un commit en la rama actual, la referencia HEAD puede usarse para reemplazar el id del commit más reciente.

<br>

### Mostrar Comandos Populares De Git

```unknown
git
```

muestra algunos de los comandos más comunes usados en git junto con una breve descripción de sus funciones.

<br>

### Inspeccionar Un Comando De Git

```unknown
git <comando> --help
```

muestra todos los parámetros que acepta un comando, además de una descripción muy detallada de la función del comando, si no se incluye un comando antes de **--help** es equivalente a usar solo git.

<br>

### Configuración De Git

```unknown
git config <parámetros> <configuraciones>
```

permite aplicar ciertas configuraciones a un repositorio, algunos de los parámetros más útiles al utilizar **git config** para configurar un repositorio son:

- **--global:** indica a git que esa configuración será aplicada a todos los repositorios de la máquina.
- **-l, --list:** muestra la configuración actual del repositorio.

algunos de los parámetros configurables más importantes de un repositorio son:

- **user.email=&lt;correo del usuario&gt;:** cambia el correo electrónico del usuario.
- **user.name=&lt;nombre del usuario&gt;:** cambia el nombre del usuario.
- **alias.&lt;nombre del alias&gt; "&lt;comando&gt;":** permite agregar a git alias para nuevos comandos.

<br>

### Iniciar O Finalizar Un Repositorio

```unknown
git init <parámetros>
```

inicia un repositorio git en el directorio actual o lo elimina si el repositorio ya está creado, en caso de iniciarse el repositorio git internamente crea el área de staging y el repositorio, sin tocar el directorio de trabajo, el repositorio se crea dentro del directorio de trabajo en una carpeta oculta llamada **.git** y el área de staging se crea en la ram, si se utiliza git init para finalizar el repositorio git elimina el área de staging y el repositorio, sin tocar el directorio de trabajo.

<br>

### Agregar Archivos Al Área De Staging Del Repositorio

```unknown
git add <parámetros> <ruta del archivo o directorio>
```

inicia el rastreo de uno o varios archivos agregandolos al área de staging del repositorio. lo más normal es usar **.** como ruta para rastrear y agregar todos los archivos de la carpeta actual al área de staging.

<br>

### Registrar Cambios En El Repositorio

```unknown
git commit <parámetros>
```

envía los últimos cambios desde el área de staging al repositorio para que este los registre en su base de datos de cambios, creando así una nueva versión basándose en los cambios realizados sobre uno o varios archivos, al crear una nueva versión a esta se le asigna un id de versión y los cambios realizados en los archivo que son visibles para todos en el repositorio, por defecto los commit se realizan sobre la rama **master** si no se cambia la rama de trabajo actual, algunos de los parámetros más útiles al utilizar **git commit** para enviar los cambios del área de staging al repositorio son:

- **-m, --message "&lt;mensaje&gt;":** permite agregar un mensaje al commit, idealmente todos los commits deben tener un mensaje que describa los cambios que se realizaron en la última versión subida al repositorio para facilitar la comprensión de los cambios hechos.
- **-a, --all:** indica a git que al hacer el commit pase al área de staging todos los cambios en los archivos que han sido previamente rastreados antes de hacer el commit, es equivalente a realizar un **git add** solo sobre los archivos que ya han sido registrados y luego un **git commit** estándar, por lo que sí se han agregado nuevos archivos desde el último commit si es necesario utilizar un **git add** primero, incluso usando este parámetro.
- **--amend:** permite "remendar" el último commit pegando los últimos cambios al último commit.

<br>

### Comprobar El Estatus De La Base De Datos De Cambios Del Repositorio

```unknown
git status
```

muestra el estatus de la base de datos de cambios del repositorio.

<br>

### Comparar Cambios Entre Versiones Del Repositorio

```unknown
git diff <parámetros> <id del commit antiguo> <id del commit nuevo>
```

muestra los cambios entre una versión y otra del repositorio basadas en la misma rama usando dos id de los diferentes commits, si no se indican los commits con los que se quiere hacer el diff, usando su id, por defecto el diff se realiza entre el directorio de trabajo y el área de staging.

<br>

### Mostrar Los Logs Del Repositorio

```unknown
git log <parámetros>
```

muestra todos los cambios históricos hechos en el repositorio al no incluir parámetros, log se centra en mostrar los id de cada commit, pero también muestra la fecha, el autor y el comentario del commit, además de mostrar cual es el commit HEAD actualmente, algunos de los parámetros más útiles al usar **git log** son:

- **--stat:** muestra los archivos en los que se hicieron cambios en cada log, además del número de bytes que se cambiaron.
- **--all:** muestra todos los cambios que han ocurrido.
- **--graph:** muestra las ramas de las que ha salido cada commit.
- **--oneline:** muestra una sola línea de texto de cada log.
- **--decorate:** decora las líneas del grafo.
- **-s:** permite buscar una secuencia de caracteres en la historia del repositorio.

<br>

### Mostrar Los Logs Completos Del Repositorio

```unknown
git reflog <parámetros>
```

muestra todos los cambios históricos hechos en el repositorio al no incluir parámetros, incluso los que se eliminaron en la historia mediante un rebase o un reset, reflog se centra en mostrar los id de cada commit, pero también muestra el comentario del commit.

- **--all:** muestra todos los cambios que han ocurrido en el repositorio, no sólo los generados por commits.

<br>

### Mostrar Los Cambios Del Repositorio

```unknown
git show <parámetros>
```

muestra todos los cambios históricos hechos en el repositorio al no incluir parámetros, show se centra en los cambios de las líneas realizados en los archivos, por lo que siempre muestra un diff entre el commit actual y el anterior de los archivos modificados en el último commit, ademas show muestra también toda la información que muestra log.

<br>

### Limpiar El Directorio De Trabajo

```unknown
git clean <parámetros>
```

elimina todos los archivos no rastreados por el repositorio del directorio de trabajo, **git clean** no funciona sin ciertos parámetros que se usan para confirmar la limpieza, además, **git clean** ignora los archivos filtrados en el .gitignore, algunos de los parámetros más útiles al usar **git clean** son:

- **-n, --dry-run:** no elimina nada, solo muestra que se borraría en caso de ejecutarse el comando.
- **-d:** permite incluir directorios no rastreados en el repositorio dentro de los criterios de la limpieza.
- **-f, --force:** es uno de los parámetros que habilita a **git clean** para eliminar archivos.
- **-i, --interactive:** es el segundo parámetro que permite a **git clean** para eliminar archivos, además de eliminar archivos los elimina de forma interactiva demostrando y confirmando que se va a borrar.

<br>

### Eliminar Archivos Del Repositorio

```unknown
git rm <parámetros> <nombre del archivo>
```

elimina uno o varios archivos del área de staging o del repositorio, **git rm** necesita alguno de los siguientes parámetros para ejecutarse correctamente:

- **-f, --force:** elimina uno o varios archivos del repositorio, del área de staging y del directorio de trabajo.
- **--cached:** elimina uno o varios archivos del repositorio y del área de staging.

algunos de los parámetros opcionales más útiles al utilizar **git rm** para eliminar archivos del área de staging o del repositorio son:

- **-r:** habilita la remoción recursiva cuando le es dado el nombre de un directorio.

<br>

## Administración De Ramas Y Versiones Con Git

<p align="center">
<img src="imagenes/notas_de_git_y_github/sistema_de_ramas_de_git.svg" width="100%" height="auto"/>
</p>

las ramas permiten dividir el código fuente de una aplicación en diferentes líneas separadas cronológicamente que luego se unen para formar una solo código fuente, por defecto git trabaja sobre la rama **master** pero normalmente cuando se trabaja en un equipo de desarrollo se utilizan diferentes ramas para que varios miembros del equipo trabajen en simultáneo en partes o funcionalidades distintas de una misma aplicación. cuando se crea una rama nueva basicamente lo que se hace es crear una copia de la última versión de la rama master de una nueva rama separada, y los cambios que se realicen en esta nueva rama no serán visibles en master hasta que no se fusionan las dos ramas con una operación llamada **merge**.\
algunos de los conceptos más útiles al trabajar con ramas en git son:

- **merge:** un merge es una operación que se realiza cuando se une el código de dos ramas diferentes para generar una nueva versión.
- **conflicto:** un conflicto es lo que sucede cuando al realizar un merge los cambios de una rama dañan el funcionamiento de la otra rama, por lo que la nueva versión no funciona correctamente, o simplemente los cambios son incompatibles, por lo que no se puede realizar el merge correctamente.

<br>

### Administrar Ramas

el comando **git branch** se emplea para realizar las principales acciones que realiza git en relación con ramas, como crear, listar y eliminar ramas, además de otras adicionales, como crear copias de ramas o renombrar ramas.

#### Crear Ramas

```unknown
git branch <parámetros> <nombre de la rama>
```

la acción por defecto de **git branch** si no se dan parámetros y se da un nombre es crear una nueva rama con el nombre indicado, la nueva rama se crea en base a la rama en la que se está posicionado actualmente, por lo que al crear una nueva rama es recomendable estar posicionado en la rama más actualizada.

#### Listar Ramas

```unknown
git branch <parámetros>
```

la acción por defecto de **git branch** si no se dan parámetros y no se da un nombre es listar las ramas disponibles resaltando la rama actual, algunos de los parámetros más útiles para listar ramas usando **git branch** son:

- **-l, --list &lt;patron&gt;:** es equivalente a usar **git branch** sin parámetros, pero adicionalmente se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.
- **-r, --remotes:** modifica la función del comando para listar las ramas remotas, al combinarlo con **--list** se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.
- **-a, --all:** modifica la función del comando para listar ramas locales y remotas, al combinarlo con **--list** se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.

para ver las ramas también se puede usar el siguiente comando, el cual muestra de forma "gráfica" la evolución del proyecto basándose en ramas, ids de commit y mensajes de commit.

```unknown
git log --all --graph --decorate --oneline
```

otro comando alternativo para ver la historia de las ramas es **git show-branch**, este comando además de mostrar las ramas muestra también el historial de los commits del repositorio distinguiendo las ramas.

```unknown
git show-branch <parámetros>
```

- **-a, --all:** modifica la función del comando para listar todo el historial de commits y ramas disponibles.

#### Eliminar Ramas

```unknown
git branch --delete <parámetros adicionales>
```

para eliminar una rama se debe usar el comando **git branch** junto al parámetro **-d** o **--delete**, usando este parámetro en cualquiera de sus dos formas se modifica la función del comando para eliminar ramas, sin embargo, para eliminar una rama sin errores usando este parámetro la rama primero se debe haber sincronizado con el repositorio remoto en caso de tener uno, algunos de los parámetros adicionales más útiles para eliminar ramas usando **git branch** en combinación con el parámetro **-d** o **--delete** son:

- **-f, --force:** al usare con **--delete** permite borrar una rama independientemente de su estatus.
- **-d:** atajo para la combinación de **--delete --force**.

#### Parámetros Adicionales

algunos de los parámetros adicionales que también acepta **git branch** para tener funciones adicionales son:

- **-m, --move &lt;nuevo nombre&gt;:** renombra la rama actual.
- **-c, --copy &lt;nombre de copia de la rama&gt;:** crear una copia de la rama actual.
- **-f, --force:** restablece el estado de la rama actual a su estado inicial, incluso si el nombre inicial de la rama fue asignado a otra rama que aún existe, al combinarse con **--move** permite renombrar la rama actual incluso si el nombre nuevo ya existe y al combinarse con **--copy** permite crear una copia de la rama actual incluso si el nombre de la copia ya existe.
- **-m:** atajo para la combinación de **--move --force**.
- **-c:** atajo para la combinación de **--copy --force**.

<br>

### Fusionar Ramas

```unknown
git merge <parámetros> <nombre de la rama>
```

fusiona los archivos de la rama indicada con la rama actual, algunos de los parámetros más útiles al usar **git merge** son:

- **-m &lt;mensaje&gt;:** un merge por defecto genera una nueva versión y un commit, por lo que es necesario que haya un mensaje que indique los cambios que se hicieron en el último commit.

al fusionar dos o más ramas con **merge** pueden presentarse conflictos cuando en las ramas se alteran las mismas líneas de diferentes formas, para solventar estos conflictos se deben borrar todas las líneas que no correspondan con los cambios que se desean conservar en la rama, la forma en la que git representa un conflicto en un archivo es usando **<<<<<<< HEAD** para indicar donde inicia el código de la rama actual, **>>>>>>> new_branch_to_merge_later** para indicar donde finaliza el código de la rama que se quiere fusionar con la rama actual (en este caso **new_branch_to_merge_later**) y **=======** para indicar el final del código de la rama actual y el inicio del de la rama que se quiere fusionar, un ejemplo de cómo se representa un conflicto en git sería el siguiente:

```python
<<<<<<< HEAD
print("holamundo")
=======
print("helloworld")
>>>>>>> new_branch_to_merge_later
```

en este caso suponiendo que se quiera conservar el mensaje que diga **holamundo** en la rama actual se eliminará el resto del código, dejando como resultado:

```python
print("holamundo")
```

en caso contrario el resultado sería:

```python
print("helloworld")
```

algunos editores tienen herramientas para resolución de conflictos integradas, pero simplemente consisten en lo mismo, borrar las partes que no se quieren conservar dejando en el archivo solo las que se quieren conservar.

<br>

### Moverse Entre Ramas Y Versiones

el comando **git checkout** actualiza los archivos del directorio de trabajo para que correspondan con los de una rama o una versión específica del repositorio.

#### Moverse Entre Versiones

```unknown
git checkout <parámetros> <id del commit> <nombre del archivo>
```

traer versiones especificadas de un archivo al directorio de trabajo, si no se indica un archivo al final del comando se traerán todos los archivos de la versión indicada al directorio de trabajo, para conservar los cambios luego de traer uno o varios archivos al directorio de trabajo basta con hacer un **git add** y un **git commit**, si no se quieren conservar los cambios hechos por el checkout basta con hacer un nuevo checkout apuntando a la última versión o HEAD para descartarlos. si checkout se usa para moverse entre versiones de una misma rama con cada checkout se generará una nueva rama, para eliminar los cambios de esa nueva rama basta con hacer un nuevo checkout a la rama master en caso de no querer guardar los cambios en una rama aparte.

#### Moverse Entre Ramas

```unknown
git checkout <parámetros> <nombre de la rama>
```

traer los archivos de una rama al directorio de trabajo y cambiar la rama actual.

<br>

### Hacer Rebase A Una Rama

```unknown
git rebase <rama a la que se enviaran los cambios de la rama actual>
```

rebase permiten pegar una rama al final de otra sin dejar registros de la rama que se pegó a la rama principal, la forma correcta de realizar un rebase es realizando rebas primero de la rama de cambios a la rama principal, luego de la rama principal a la rama de cambios y por último se elimina la rama en la que se hicieron los cambios, el resultado es que los cambios en la historia se ven como si jamás hubiera estado la rama de cambios, y además no se sabe quién hizo los cambios ya que no hay historia.

**nota:** rebase es muy mala práctica en repositorios remotos ya que se reescribe la historia de una rama y no hay registros de los cambios al final.

<br>

### Administrar La Reserva De Cambios De Git

la reserva de cambios de git o stash permite guardar temporalmente en un listado de los cambios que aún no están listos para ser enviados al repositorio, es bastante útil en escenarios en los que se necesitan archivos de otras ramas diferentes a la rama en la que están los cambios, pero estos no están listos para un commit, por lo que no se puede hacer un checkout ya que hacerlo sin un commit eliminaría los cambios, al hacer un stash en un rama todos los cambios hechos en el directorio de trabajo de esa rama luego del HEAD son enviados a la lista de stashs, lo que además permite volver al HEAD de forma rápida y segura sin perder los cambios, los stash son extremadamente útiles cuando se quieren realizar pequeñas pruebas o experimentos en los que no vale la pena crear una nueva rama.

```unknown
git stash push
```

envía los cambios posteriores al HEAD de la rama a la lista de stash.

```unknown
git stash list
```

muestra toda la lista de stashs.

```unknown
git stash show <id del stash>
```

muestra con un diff las diferencias entre un stash respecto al HEAD de la rama en la que se realizó el stash, si no se indica el stash el diff muestra los cambios usando el stash más reciente.

```unknown
git stash pop <id del stash>
```

remueve un stash de la lista de stashs y aplica los cambios los cambios en el directorio de trabajo actual, si no se indica el stash se aplica usando el más antiguo, es importante que el directorio de trabajo coincida con el directorio de trabajo del stash, por lo que al hacer un pop es necesario estar en la misma rama en la que se estaba posicionado cuando se inició el stash con push.

```unknown
git stash drop <id del stash>
```

elimina un stash de la lista de stashs, si no se indica un stash elimina el último.

```unknown
git stash branch <nombre de la rama> <id del stash>
```

crear una nueva rama con el nombre indicado la cual parte del último commit antes del stash, aplica todos los cambios del stash a la rama y realiza un checkout a la nueva rama, en caso de no indicarse un stash utiliza el stash más reciente.

```unknown
git stash clear
```

elimina todos los stash en la lista de stashs.

<br>

### Administrar Tags

los tag son una manera de etiquetar estados de un repositorio, se usan comúnmente para indicar las versiones o releases de un proyecto mantenido con git, sin embargo, el versionamiento no afecta internamente al proyecto, solo establece etiquetas asociadas a los releases, usualmente el etiquetado de versiones usando tags se hace siguiendo el [**versionamiento semántico**](https://semver.org/lang/es/), que es uno de los más populares y sencillos de usar, la mayor parte de las acciones que se realizan en git con relación a los tags se realizan usando el comando **git tag**.

#### Crear Tags

```unknown
git tag -a <nombre del tag> -m <mensaje> <id del commit>
```

el comando base para administrar tags en git es **git tag**, incluyendo los parámetros **-a** y **-m** se crea un nuevo tag agregando un nombre de tag y un mensaje de tag, adicionalmente para crear un nuevo tag en git hay que indicar a qué commit estará asociado el nuevo tag, el nuevo tag será creado, pero solo será registrado de forma local, para enviar el nuevo tag a github hace falta usar una variación del comando **git push** ya que los tags no son considerados como cambios, por lo que el comando regular no envía los tags a github.

```unknown
git push <nombre del repositorio remoto> --tags
```

al crear un nuevo tag es útil usar antes el siguiente comando para ver de forma "gráfica" la evolución del proyecto basándose en ramas, ids de commit y mensajes.

```unknown
git log --all --graph --decorate --oneline
```

#### Listar Tags

```unknown
git tag
```

al usar el comando **git tag** sin incluir parámetros adicionales se listan todos los tags del repositorio.

```unknown
git show-ref --tags
```

el comando **git show-ref** seguido por el parámetro **--tags** tiene un comportamiento similar a **git tag** con la ventaja de que además lista el id del commit que corresponde con cada tag.

#### Eliminar Tags

```unknown
git tag -d <nombre del tag>
```

al usar el comando **git tag** con el parámetro **-d** se elimina el tag correspondiente con el nombre de tag indicado, sin embargo esto solo ocurre en el repositorio local, para eliminar un tag en github hace falta usar una variación del comando **git push** indicando además de los parámetros usuales el nombre del tag que se va a eliminar, esto se debe a que github trata de conservar los tags, ya que usualmente están asociados a releases, por lo que no es normal ni adecuado eliminar un tag de github.

```unknown
git push <nombre del repositorio remoto> :refs/tags/<nombre del tag>
```

<br>

### Traer A Una Rama Cambios Viejos De Otra

```unknown
git cherry-pick <parámetros> <id del commit>
```

permite traer los cambios de un commit específico a la rama actual sin tener que hacer un merge completo.

<br>

### Regresar A Versiones Anteriores Del Repositorio

```unknown
git reset <modo> <id del commit>
```

mueve el HEAD del commit actual al commit indicado, dependiendo del modo al cambiar el HEAD todo los cambios luego de ese commit son descartados o se envían al área de staging para poder rastrearlos en el repositorio después, entre otras opciones que cambian según el modo, algunos de los modos más usados son:

- **--soft:** elimina los cambios en el repositorio, mantiene los cambios del área de staging y mantiene los cambios en el directorio de trabajo, por lo que los cambios hechos luego del commit indicado en el área de staging y en el directorio de trabajo pueden agregarse al repositorio posteriormente con un **git add** y un **git commit**.
- **--mixed:** es el modo por defecto, elimina los cambios en el repositorio, elimina los cambios del área de staging, pero mantiene los cambios en el directorio de trabajo, por lo que los cambios hechos luego del commit indicado en el directorio de trabajo pueden agregarse al repositorio posteriormente con un **git add** y un **git commit**.
- **--hard:** elimina los cambios en el repositorio, elimina los cambios del área de staging y elimina los cambios del directorio de trabajo, por lo que ninguno de los cambios hechos luego del commit podrán agregarse posteriormente al repositorio.

<br>

## Administración De Repositorios Remotos Con Git Y Github

<p align="center">
<img src="imagenes/notas_de_git_y_github/flujo_basico_con_repositorios_remotos_github.svg" width="100%" height="auto"/>
</p>

un repositorio remoto es lo que se utiliza en la mayoría de casos en los que un desarrollo es el producto del trabajo de varios desarrolladores que trabajan en equipo para construir una sola aplicación, por lo tanto, al utilizar un repositorio remoto como github o **gitlab** lo que se hace es agregar una cuarta área adicional a las tres que se usan al trabajar con un repositorio git local, que es la del servidor remoto al que se envían con un **git push** los cambios luego de ser **rastreados** por el repositorio local con un commit para que todas las personas del equipo puedan ver y trabajar sobre los cambios más recientes realizados en el repositorio remoto.\
las guías para crear repositorios remotos con [**github**](https://guides.github.com/) y [**gitlab**](https://docs.gitlab.com/) estan enlazadas a sus nombres en este comentario.

<br>

### Administrar Repositorios Remotos

```unknown
git remote <sub comandos> --verbose
```

permite realizar varias acciones en los diferentes repositorios remotos vinculados basados en git según el sub comando indicado, si no se da algún subcomando muestra un listado de los repositorios remotos vinculados, se puede incluir un único parámetro al utilizar **git remote** sin sub comandos:

- **-v, --verbose:** hace que se muestran las urls además de los nombres asignados a los repositorios remotos al listarlos.

#### Agregar Repositorio Remoto Al Repositorio Local

```unknown
git remote add <nombre del repositorio remoto> <url del repositorio remoto>
```

vincula al repositorio local un repositorio remoto, el cual se puede llamar posteriormente con el nombre dado, normalmente **origin**, para realizar acciones como **git push**, **git pull** o **git fetch**.

<br>

### Cambiar La Url De Un Repositorio Remoto

```unknown
git remote set-url <nombre del repositorio remoto> <url del repositorio remoto>
```

cambia la url del repositorio remoto, es especialmente útil cuando se quiere cambiar la conexión de un repositorio de protocolo https a ssh.

<br>

### Clonar Un Repositorio Remoto

```unknown
git clone <parámetros> <url del repositorio remoto>
```

crea una copia de todos los archivos del repositorio remoto en el repositorio local y en el directorio de trabajo, sin cambiar nada en el área de staging, además vincula la copia local con la remota, por lo que si se tiene los permisos se pueden hacer acciones como **git push**, **git pull** o **git fetch** sin realizar configuraciones adicionales, algunos de los parámetros más útiles al clonar un repositorio con **git clone** son:

- **-o &lt;nombre del repositorio remoto&gt;, --origin &lt;nombre del repositorio remoto&gt;:** cambia el nombre de referencia del repositorio remoto para no usar **origin** como nombre de referencia.

<br>

### Traer Los Cambios Del Repositorio Remoto Al Repositorio Local

```unknown
git fetch <parámetros> <nombre del repositorio remoto> <rama del repositorio local>
```

actualiza una rama del repositorio local con los últimos cambios de la misma rama del repositorio remoto, sin alterar el área de staging ni el directorio de trabajo, por lo que si se quieren traer los cambios no solo al repositorio local si no también al directorio de trabajo hace falta realizar también un **git merge**.

<br>

### Traer Los Cambios Repositorio Remoto Al Repositorio Local Y Al Directorio De Trabajo

```unknown
git pull <parámetros> <nombre del repositorio remoto> <nombre de la rama>
```

actualiza una rama del repositorio local con los últimos cambios de la misma rama del repositorio remoto, y tambien trae los cambios al directorio de trabajo sin alterar el área de staging, es equivalente a hacer un **git fetch** en simultáneo con un **git merge** entre el directorio local y el repositorio local, el cual ya fue actualizado con los últimos cambios en el repositorio remoto mediante **git fetch**.

<br>

### Subir Cambios Del Repositorio Local Al Repositorio Remoto

```unknown
git push <parámetros> <nombre del repositorio remoto> <nombre de la rama>
```

envía los cambios hechos en una rama del repositorio local al repositorio remoto, por lo tanto si se quieren enviar los cambios más recientes del directorio local al repositorio remoto primero se realizan un **git pull**, un **git add**, un **git commit** y luego un **git push**, esta secuencia de comandos se usa para traer los cambios más recientes del repositorio remoto al local, para enviar los cambios del repositorio local al área de staging luego al repositorio local y por último al repositorio remoto, algunos de los parámetros más útiles al utilizar **git push** son:

- **--all:** actualiza todas las ramas del repositorio remoto con los cambios de las ramas del repositorio local, al utilizar este parámetro no hace falta indicar el nombre de una rama en concreto.
- **-u, --set-upstream:**

<br>

## Conexión Con Github Usando Protocolo Ssh

<p align="center">
<img src="imagenes/notas_de_git_y_github/sistema_de_conexion_ssh_de_github.svg" width="100%" height="auto"/>
</p>

establecer que las conexiones a un repositorio en github se hagan con el protocolo ssh en lugar del https permiten agregar al repositorio una capa adicional de seguridad, ya que de esta forma los archivos enviados entre el repositorio remoto y cualquier otra máquina están totalmente cifrados y protegidos, github usa una llave privada y una llave pública para conseguir este cifrado, el cual se basa en una serie de algoritmos de cifrado y descifrado asimétricos usando el par de llaves para cifrar y descifrar los archivos, de tal forma que para poder descifrar cualquier archivo cifrado con una llave pública es necesario tener la contraparte privada de esa llave, la cual se crea y "vincula" a la llave pública cuando se crean el par de llaves, la llave privada bajo ninguna circunstancia debe salir de la máquina que establece la conexión ssh con github. para crear una conexión ssh bilateral, cifrada y segura entre cualquier máquina y github hace falta por lo tanto crear las dos llaves en la máquina que va a establecer la conexión, una privada y una pública, la llave pública se comparte con github y github compartirá su llave pública de vuelta, cifrada con la llave pública enviada previamente, de esta forma tanto en la máquina que va a establecer la conexión como en github hay una llave privada y una pública, lo que permite a github descifrar los archivos enviados desde la máquina local y a la máquina local descifrar los datos de github para así establecer una conexión bilateral totalmente segura a través de internet.\
los pasos para establecer una conexión ssh segura entre el repositorio y la máquina son:

<br>

### Crear El Par De Llaves

```unknown
ssh-keygen -t rsa -b 4096 -C "correo electrónico vinculado al usuario de github"
```

el primer paso para usar ssh en lugar de https es generar un par de llaves ssh, al crear las llaves hay que vincular el correo del usuario de github y además se puede agregar un password a la llave privada para tener más seguridad al usarla. al generarse el par de llaves la llave privada se guarda sin extensión y la pública se guarda con la extensión **.pub**. en sistemas linux ambas llaves son almacenadas en **~/.ssh/id_rsa** si no se indica otra ruta.

<br>

### Comprobar Funcionamiento Del Servidor Ssh

```unknown
eval $(ssh-agent -s)
```

tras generar el par de llaves hay que verificar que el servidor encargado de manejar las llaves ssh esté activo.

<br>

### Agregar Llave Al Servidor Ssh

```unknown
ssh-add <ruta en la que se guardaron las llaves en el paso 1>
```

tras verificar que el servidor ssh este activo hay que indicarle al servidor que hay un nuevo par de llaves, para así usarlas posteriormente para descifrar mensajes de conexiones ssh hechas con la contraparte pública de la llave.

<br>

### Agregar A Github La Llave Pública

ya teniendo toda la configuración local hay que enviar la llave pública a github, para agregar la llave pública hay que copiar el contenido de la llave publica, entrar al usuario de github con el que se va a hacer la conexión ssh, en el usuario hay que ir a **profile > settings > ssh and gpg keys** seleccionar la opción que dice **new ssh key** y pegar el contenido de la llave pública.

<br>

### Cambiar La Url Del Repositorio Remoto Para Usar La Conexión Ssh

```unknown
git remote set-url <nombre del repositorio remoto> <url del repositorio remoto>
```

como último paso hay que actualizar la url del repositorio local reemplazandola por la url que usa el repositorio para conexiones ssh, si al clonar el repositorio se clona usando ssh no hace falta hacer este paso.

<br>

## Pull Requests Con Github

<p align="center">
<img src="imagenes/notas_de_git_y_github/sistema_de_pull_requests_de_github.svg" width="100%" height="auto"/>
</p>

los pull request o pr (también llamados merge request o mr en gitlab) son un sistema de revisión de código propio de github, que permite que un colaborador pide que revisen sus cambios antes de hacer merge a una rama, normalmente master. al hacer un pull request se genera una conversación que pueden seguir los demás miembros del repositorio, así como, comentar, autorizar o rechazar los cambios del pr.

el flujo de trabajo normal de un pull request es el siguiente

1. se realizan en un rama paralela todos los cambios.
1. se suben a github los cambios.
1. en github se hace el pull request comparando la rama master con la rama en la que se hicieron los cambios.
1. uno, o varios colaboradores revisan que el código sea correcto y dan feedback.
1. el colaborador hace los cambios que desea en la rama y lo vuelve a subir al remoto.
1. se aceptan los cambios en github.
1. se hace merge a master desde github.

<br>

## Forks Con Github

<p align="center">
<img src="imagenes/notas_de_git_y_github/sistema_de_forks_de_github.svg" width="100%" height="auto"/>
</p>

los forks son una característica única de github que permite crear una copia exacta del estado actual de un repositorio directamente en github, éste repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio), en pocas palabras, un fork se puede utilizar como un repositorio git cualquiera, un fork es una bifurcación del repositorio completo, tiene una historia en común, pero pueden variar los cambios, ya que ambos proyectos podrán ser modificados en paralelo y para estar al día hace falta mantener el fork actualizado respecto al original. al hacer un fork de un proyecto en github, quien hace el fork pasa a ser dueño del repositorio fork y puede trabajar en éste con todos los permisos, pero es un repositorio completamente diferente al original, teniendo algunas historias en común.\
los forks son importantes porque es la manera en la que funciona el open source, ya que, una persona puede no ser colaborador de un proyecto, pero puede contribuir al mismo, haciendo mejor software que pueda ser utilizado por cualquiera.\
al hacer un fork, github sabe que se hizo el fork del proyecto, por lo que se le permite al colaborador hacer pull request desde su repositorio propio al original.

para mantener actualizado un fork hay dos opciones, desde github se pueden hacer merges desde master al fork, pero también se puede configurar el repositorio original como un segundo repositorio remoto en el repositorio local en el que se está trabajando el fork, desde el cual se pueden traer y hacer merge de los cambios más recientes del repositorio original, para esto se usa el comando **git remote add** apuntando hacia el repositorio original.

<br>

## Uso De Archivos Gitignore Con Git Y Github

```ignore

# Archivos De Nodejs
node_modules

# Archivos De Docker
.dockerignore
dockerfile

# Archivos De Logs
*.log

# Imágenes
*.jpg

```

los archivos [**.gitignore**](https://git-scm.com/docs/gitignore) permiten controlar que archivos son y no enviados al repositorio desde el directorio de trabajo según ciertos criterios de búsqueda establecidos en el archivo. por diversas razones, no todos los archivos que se agregan a un proyecto deben guardarse en el repositorio, ésto se debe a que hay archivos que no deben ser visibles para todo el mundo, y hay archivos que al estar en el repositorio hacen más lento el proceso de desarrollo, como los archivos binarios de gran tamaño (también conocidos como blob, que es la abreviatura de binary large object).

las razones principales para tomar la decisión de no agregar un archivo a un repositorio git son:

- es un archivo con contraseñas.
- es un blob.
- son archivos que se generan corriendo comandos.

<br>
