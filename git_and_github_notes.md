# Git y GitHub

[**Git**](https://git-scm.com/doc) es el sistema de versionamiento más popular actualmente, **Git** permite guardar el historial de cambios y el crecimiento de los archivos de un proyecto de forma atómica e incremental, por lo que cada cambio se escribe sobre el anterior y así sucesivamente desde la versión inicial hasta la final, lo que hace posible ver la evolución de los archivos con cada actualización sin almacenar cada versión completa, para esto **Git** emplea al interior de cada repositorio una base de datos que guarda los cambios de forma incremental, la cual se actualiza con cada versión nueva que llega al repositorio. [**GitHub**](https://docs.github.com/es) por su parte es el sistema de versionamiento remoto más popular actualmente, **GitHub** además permite trabajo colaborativo sobre los archivos de un repositorio remoto.\
Git y **GitHub** soportan versionamiento de archivos binarios, pero el versionamiento de archivos binarios no es tan preciso como con archivos basados en texto plano, por lo que normalmente se utilizan **Git** y **GitHub** solo para archivos de texto plano, como el código.

## Flujo de trabajo básico en Git

<p align="center">
<img src="images/local_git_repository_basic_workflow.png" width="100%" height="auto"/>
</p>

Cuando se versionan archivos con repositorios **Git** locales los cambios pueden estar almacenados en tres posibles áreas, la primera es el **directorio de trabajo**, que simplemente es el directorio dentro de la máquina local en el que se inició el repositorio, la segunda área es el **área de staging**, que es un área de almacenamiento en la ram de la máquina local donde se preparan los cambios para ser agregados al repositorio y por ultimo esta el **repositorio**, que es un área de almacenamiento local o remota donde se guardan los archivos y se registran sus respectivos cambios a través de cada versión, dependiendo del nivel en el que esté un cambio este se puede considerar como **no rastreado** cuando solo está presente en el **directorio de trabajo**, **en espera** cuando está presente en el **directorio de trabajo** y el **área de staging** y **rastreado** cuando pasa a estar en **las tres áreas** luego de ser enviado del **área de staging** al **repositorio**, algunos de los conceptos más útiles al trabajar con **Git** de forma básica son:

- **commit:** Un commit es lo que sucede cuando un cambio pasa del área de staging al repositorio, es decir que pasa de estra **en espera** a estar **rastreado** por la base de datos de cambios del repositorio, al ser aceptado un cambio como una nueva versión con un commit, **Git** le asigna un número de versión o Id que identifica esa nueva versión, y además se registran otros metadatos como la fecha, hora y el usuario que hizo el commit, por lo que cada cambio en **Git** es rastreable por su Id y por los otros metadatos que son almacenados al hacer el commit.
- **Head:** Es la última versión rastreada por el repositorio mediante un **commit** en la rama actual.

### Mostrar comandos populares de git

```bash
git
```

Muestra algunos de los comandos más comunes usados en **Git** junto con una breve descripción de sus funciones.

### Mostrar ayuda de un comando

```bash
git [comando] --help
```

Muestra todos los parámetros que acepta un comando, además de una descripción muy detallada de la función del comando, si no se incluye un comando antes de **--help** es equivalente a **git**.

### Configuración de Git

```bash
git config [parámetros] [configuraciones]
```

Permite aplicar ciertas configuraciones a un repositorio, algunos de los parámetros más útiles al utilizar **git config** para configurar un repositorio son:

- **--global:** Indica a **Git** que esa configuración será aplicada a todos los repositorios de la máquina.
- **-l, --list:** Muestra la configuración actual del repositorio.

Algunos de los parámetros configurables más importantes de un repositorio son:

- **user.email=[correo del usuario]:** Cambia el correo electrónico del usuario.
- **user.name=[nombre del usuario]:** Cambia el nombre del usuario.

### Iniciar o finalizar un repositorio

```bash
git init [parámetros]
```

Inicia un repositorio **Git** en el directorio actual o lo elimina si el repositorio ya está creado, en caso de iniciarse el repositorio **Git** internamente crea el área de staging del repositorio y el repositorio, sin tocar el directorio de trabajo, el repositorio se crea dentro del directorio de trabajo en una carpeta oculta llamada **.git** y el área de staging se crea en la ram, si se utiliza **Git** init para finalizar el repositorio **Git** elimina el área de staging y el repositorio, sin tocar el directorio de trabajo.

### Agregar archivos al área de staging del repositorio

```bash
git add [parámetros] [ruta del archivo o directorio]
```

Inicia el rastreo de uno o varios archivos agregandolos al área de staging del repositorio. Lo más normal es usar **.** como ruta para rastrear y agregar todos los archivos de la carpeta actual al área de staging.

### Registrar cambios en el repositorio

```bash
git commit [parámetros]
```

Envía los últimos cambios desde el área de staging al repositorio para que este los registre en su base de datos de cambios, creando así una nueva versión basándose en los cambios realizados sobre uno o varios archivos, al crear una nueva versión a esta se le asigna un Id de versión y los cambios realizados en los archivo que son visibles para todos en el repositorio, por defecto los **commit** se realizan sobre la rama **master** si no se cambia la rama de trabajo actual, algunos de los parámetros más útiles al utilizar **git commit** para enviar los cambios del área de staging al repositorio son:

- **-m, --message "[mensaje]":** Permite agregar un mensaje al **commit**, idealmente todos los **commits** deben tener un mensaje que describa los cambios que se realizaron en la última versión subida al repositorio para facilitar la comprensión del versionamiento y los cambios hechos.
- **-a, --all:** Indica a **Git** que al hacer el **commit** pase al área de staging todos los cambios en los archivos que han sido previamente rastreados, es equivalente a realizar un **add** solo sobre los archivos que ya han sido registrados y luego un **commit** estándar, por lo que sí se han agregado nuevos archivos desde el último **commit** si es necesario utilizar **add** primero incluso usando este parámetro.

### Comprobar el estatus de la base de datos de cambios del repositorio

```bash
git status
```

Muestra el estatus de la base de datos de cambios del repositorio.

### Comparar cambios entre versiones de diferentes archivos

```bash
git diff [parámetros] [Id del commit antiguo] [Id del commit nuevo]
```

Muestra los cambios entre una versión y otra del repositorio usando dos Id de los diferentes **commits**, si no se indican los **commits** con los que se quiere hacer el diff, usando su Id, por defecto el diff se realiza entre el directorio de trabajo y el área de staging.

### Mostrar los logs del repositorio

```bash
git log [parámetros]
```

Muestra todos los cambios históricos hechos en el repositorio al no incluir parámetros, log se centra en mostrar los Id de cada **commit**, pero también muestra la fecha, el autor y el comentario del **commit**, además de mostrar cual es el **commit** **Head** actualmente, algunos de los parámetros más útiles al usar **git log** son:

- **--stat:** Muestra los archivos en los que se hicieron cambios en cada log, además del número de Bytes que se cambiaron.
- **--all:** Muestra todos los cambios que han ocurrido.
- **--graph:** Muestra las ramas de las que ha salido cada commit.
- **--oneline:** Muestra una sola línea de texto de cada log.
- **--decorate:** Decora las líneas del grafo.

### Mostrar los cambios del repositorio

```bash
git show [parámetros]
```

Muestra todos los cambios históricos hechos en el repositorio al no incluir parámetros, show se centra en los cambios de las líneas realizados en los archivos, por lo que siempre muestra un diff entre el commit actual y el anterior de los archivos modificados en el último commit, ademas show muestra también toda la información que muestra log.

### Eliminar archivos del área de staging o del repositorio

```bash
git rm [parámetros] [nombre del archivo]
```

Elimina uno o varios archivos del área de staging o del repositorio, **git rm** necesita alguno de los siguientes parámetros para ejecutarse correctamente:

- **-f, --force:** Elimina los archivos del repositorio y del directorio de trabajo. el repositorio guarda el registro de la existencia de los archivos, por lo que pueden ser recuperados de ser necesario.
- **--cached:** Elimina uno o varios archivos del área de staging, por lo que para pasarlos al repositorio hará falta volver a enviarlos al área de staging antes con un **commit**.

Algunos de los parámetros opcionales más útiles al utilizar **git rm** para eliminar archivos del área de staging o del repositorio son:

- **-r:** Habilita la remoción recursiva cuando le es dado el nombre de un directorio.

## Administración de ramas y versiones en Git

<p align="center">
<img src="images/git_branches_system.png" width="100%" height="auto"/>
</p>

Las ramas permiten dividir el código fuente de una aplicación en diferentes líneas separadas cronológicamente que luego se unen para formar una solo código fuente, por defecto **Git** trabaja sobre la rama **master** pero normalmente cuando se trabaja en un equipo de desarrollo se utilizan diferentes ramas para que varios miembros del equipo trabajen en simultáneo en partes o funcionalidades distintas de una misma aplicación. Cuando se crea una rama nueva basicamente lo que se hace es crear una copia de la última versión de la rama master de una nueva rama separada, y los cambios que se realicen en esta nueva rama no serán visibles en master hasta que no se fusionan las dos ramas con una operación llamada **merge**.
\. algunos de los conceptos más útiles al trabajar con ramas de **Git** son:

- **merge:** Un merge es una operación que se realiza cuando se une el código de dos ramas diferentes para generar una nueva versión.
- **conflicto:** Un conflicto es lo que sucede cuando al realizar un merge los cambios de una rama dañan el funcionamiento de la otra rama, por lo que la nueva versión no funciona correctamente, o simplemente los cambios son incompatibles, por lo que no se puede realizar el merge correctamente.

### Administrar ramas

```bash
git branch [parámetros] [nombre de la rama]
```

Lista, crea o elimina ramas del repositorio, la acción por defecto si no se dan parámetros adicionales y se da un nombre es crear una nueva rama con el nombre indicado, si no se dan parámetros y nombres lista las ramas y resalta la rama actual, algunos de los parámetros más útiles al usar **git branch** son:

- **-l, --list [patron]:** Modifica la función del comando para listar las ramas locales, adicionalmente se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.
- **-r, --remotes:** Modifica la función del comando para listar las ramas remotas, al combinarlo con **--list** se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.
- **-a, --all:** Modifica la función del comando para listar ramas locales y remotas, al combinarlo con **--list** se puede proporcionar un patrón para listar solo las ramas cuyo nombre coincide con el patrón dado.
- **-d, --delete:** Modifica la función del comando para eliminar ramas, para eliminar una rama sin errores usando este parámetro la rama primero se debe haber sincronizado con el repositorio remoto.
- **-m, --move [nuevo nombre]:** Renombra una rama.
- **-c, --copy [nombre de copia de la rama]:** Copia una rama actual en otra.
- **-f, --force:** Restablece el estado de la rama indicada a su estado inicial, incluso si el nombre inicial de la rama fue asignado a otra rama que actualmente existe, al usare con **--delete** permite borrar una rama independientemente de su estatus, al combinarse con **--move** permite renombrar una rama incluso si el nombre nuevo ya existe y al combinarse con **--copy** permite copiar una rama incluso si el nombre de la copia ya existe.
- **-D:** Atajo para la combinación de **--delete --force**.
- **-M:** Atajo para la combinación de **--move --force**.
- **-C:** Atajo para la combinación de **--copy --force**.

### Fusionar ramas

```bash
git merge [parámetros] [nombre de la rama]
```

Fusiona los archivos de la rama indicada con la rama actual, algunos de los parámetros más útiles al usar **git merge** son:

- **-m [mensaje]:** Un merge por defecto genera una nueva versión y un commit, por lo que es necesario que haya un mensaje que indique los cambios que se hicieron en el último commit.

Al fusionar dos o más ramas con **merge** pueden presentarse conflictos cuando en las ramas se alteran las mismas líneas de diferentes formas, para solventar estos conflictos se deben borrar todas las líneas que no correspondan con los cambios que se desean conservar en la rama, la forma en la que **Git** representa un conflicto en un archivo es usando **<<<<<<< HEAD** para indicar donde inicia el código de la rama actual, **>>>>>>> new_branch_to_merge_later** para indicar donde finaliza el código de la rama que se quiere fusionar con la rama actual (en este caso **new_branch_to_merge_later**) y **=======** para indicar el final del código de la rama actual y el inicio del de la rama que se quiere fusionar, un ejemplo de cómo se representa un conflicto en **Git** sería el siguiente:

```python
<<<<<<< HEAD
print("HolaMundo")
=======
print("HelloWorld")
>>>>>>> new_branch_to_merge_later
```

En este caso suponiendo que se quiera conservar el mensaje que diga **HolaMundo** en la rama actual se eliminará el resto del código, dejando como resultado:

```python
print("HolaMundo")
```

En caso contrario el resultado sería:

```python
print("HelloWorld")
```

Algunos editores tienen herramientas para resolución de conflictos integradas, pero simplemente consisten en lo mismo, borrar las partes que no se quieren conservar dejando en el archivo solo las que se quieren conservar.

### Moverse entre ramas y versiones de archivos

El comando **git checkout** actualiza los archivos del directorio de trabajo para que correspondan con los de una rama o una versión específica del repositorio, para conservar los cambios luego de restaurar un archivo basta con hacer un **add** y un **commit**, si no se quieren conservar los cambios hechos por el checkout basta con hacer un nuevo checkout apuntando a la última versión o **Head** para descartarlos.

#### Moverse entre versiones de archivos

```bash
git checkout [parámetros] [Id del commit|HEAD] [nombre del archivo]
```

Permite traer versiones especificadas de un archivo al directorio de trabajo, si no se indica un archivo se traerán todos los archivos de la versión indicada al directorio de trabajo.

#### Moverse entre ramas

```bash
git checkout [parámetros] [nombre de la rama]
```

Permite traer los archivos de una rama al directorio de trabajo, si no se indica un archivo se traerán todos los archivos de la versión indicada al directorio de trabajo.

### Administrar tags de versión

Los tag son una manera de etiquetar estados de un repositorio, se usan comúnmente para indicar las versiones o releases de un proyecto mantenido con **Git**, sin embargo, el versionamiento no afecta internamente al proyecto, solo establece etiquetas asociadas a los releases, usualmente el etiquetado de versiones usando tags se hace siguiendo el [**versionamiento semántico**](https://semver.org/lang/es/), que es uno de los más populares y sencillos de usar.

#### Crear tags

```bash
git tag -a [nombre del tag] -m [mensaje] [id del commit]
```

El comando base para administrar tags en **Git** es **git tag**, incluyendo los parámetros **-a** y **-m** se crea un nuevo tag agregando un nombre de tag y un mensaje de tag, adicionalmente para crear un nuevo tag en **Git** hay que indicar a qué commit estará asociado el nuevo tag, el nuevo tag será creado, pero solo será registrado de forma local, para enviar el nuevo tag a **GitHub** hace falta usar una variación del comando **git push** ya que los tags no son considerados como cambios, por lo que el comando regular no envía los tags a **GitHub**.

```bash
git push [nombre del repositorio remoto] --tags
```

Al crear un nuevo tag es útil usar antes el siguiente comando para ver de forma "gráfica" la evolución del proyecto basándose en ramas, ids de commit y mensajes.

```bash
git log --all --graph --decorate --oneline
```

#### Listar tags

```bash
git tag
```

Al usar el comando **git tag** sin incluir parámetros adicionales se listan todos los tags del repositorio.

```bash
git show-ref --tags
```

El comando **git show-ref** seguido por el parámetro **--tags** tiene un comportamiento similar a **git tag** con la ventaja de que además lista el id del commit que corresponde con cada tag.

#### Eliminar tags

```bash
git tag -d [nombre del tag]
```

Al usar el comando **git tag** con el parámetro **-d** se elimina el tag correspondiente con el nombre de tag indicado, sin embargo esto solo ocurre en el repositorio local, para eliminar un tag en **GitHub** hace falta usar una variación del comando **git push** indicando además de los parámetros usuales el nombre del tag que se va a eliminar, esto se debe a que **GitHub** trata de conservar los tags, ya que usualmente están asociados a releases, por lo que no es normal ni adecuado eliminar un tag de **GitHub**.

```bash
git push [nombre del repositorio remoto] :refs/tags/[nombre del tag]
```

### Regresar a versiones anteriores del repositorio

```bash
git reset [modo] [Id del commit]
```

Mueve el **Head** del **commit** actual al **commit** indicado, dependiendo del modo al cambiar el **Head** todo los cambios luego de ese **commit** son descartados o se envían al área de staging para poder rastrearlos en el repositorio después, entre otras opciones que cambian según el modo, algunos de los modos más usados son:

- **--soft:** Elimina los cambios en el repositorio, mantiene los cambios del área de staging y mantiene los cambios en el directorio de trabajo, por lo que los cambios hechos luego del **commit** indicado en el área de staging y en el directorio de trabajo pueden agregarse al repositorio posteriormente con un **add** y un **commit**.
- **--mixed:** Es el modo por defecto, Elimina los cambios en el repositorio, elimina los cambios del área de staging, pero mantiene los cambios en el directorio de trabajo, por lo que los cambios hechos luego del **commit** indicado en el directorio de trabajo pueden agregarse al repositorio posteriormente con un **add** y un **commit**.
- **--hard:** Elimina los cambios en el repositorio, elimina los cambios del área de staging y elimina los cambios del directorio de trabajo, por lo que ninguno de los cambios hechos luego del **commit** podrán agregarse posteriormente al repositorio.

## Administración de repositorios remotos con Git y GitHub

<p align="center">
<img src="images/remote_git_repository_basic_workflow.png" width="100%" height="auto"/>
</p>

Un repositorio remoto es lo que se utiliza en la mayoría de casos en los que un desarrollo es el producto del trabajo de varios desarrolladores que trabajan en equipo para construir una sola aplicación, por lo tanto, al utilizar un repositorio remoto como **GitHub** o **GitLab** lo que se hace es agregar una cuarta área adicional a las tres que se usan al trabajar con un repositorio **Git** local, que es la del servidor remoto al que se envían con un **push** los cambios luego de ser **rastreados** por el repositorio local con un **commit** para que todas las personas del equipo puedan ver y trabajar sobre los cambios más recientes realizados en el repositorio remoto.\
Las guías para crear repositorios remotos con [**GitHub**](https://guides.github.com/) y [**GitLab**](https://docs.gitlab.com/) estan enlazadas a sus nombres en este comentario.

### Administrar repositorios remotos

```bash
git remote [sub comandos] --verbose
```

Permite realizar varias acciones en los diferentes repositorios remotos vinculados basados en **Git** según el sub comando indicado, si no se da algún subcomando muestra un listado de los repositorios remotos vinculados, se puede incluir un único parámetro al utilizar **git remote** sin sub comandos:

- **-v, --verbose:** Hace que se muestran las urls además de los nombres asignados a los repositorios remotos al listarlos.

#### Agregar repositorio remoto al repositorio local

```bash
git remote add [nombre del repositorio remoto] [url del repositorio remoto]
```

Vincula al repositorio local un repositorio remoto, el cual se puede llamar posteriormente con el nombre dado, normalmente **origin**, para realizar acciones como **push**, **pull** o **fetch**.

### Cambiar la url de un repositorio remoto

```bash
git remote set-url [nombre del repositorio remoto] [url del repositorio remoto]
```

Cambia la url del repositorio remoto, es especialmente útil cuando se quiere cambiar la conexión de un repositorio de protocolo HTTPS a SSH.

### Clonar un repositorio remoto

```bash
git clone [parámetros] [url del repositorio remoto]
```

Crea una copia de todos los archivos del repositorio remoto en el repositorio local y en el directorio de trabajo, sin cambiar nada en el área de staging, además vincula la copia local con la remota, por lo que si se tiene los permisos se pueden hacer acciones como **push**, **pull** o **fetch** sin realizar configuraciones adicionales.

### Traer los cambios del repositorio remoto al repositorio local

```bash
git fetch [parámetros] [nombre del repositorio remoto] [rama del repositorio local]
```

Actualiza una rama del repositorio local con los últimos cambios de la misma rama del repositorio remoto, sin alterar el área de staging ni el directorio de trabajo, por lo que si se quieren traer los cambios no solo al repositorio local si no también al directorio de trabajo hace falta realizar también un **merge**.

### Traer los cambios repositorio remoto al repositorio local y al directorio de trabajo

```bash
git pull [parámetros] [nombre del repositorio remoto] [rama del repositorio local]
```

Actualiza una rama del repositorio local con los últimos cambios de la misma rama del repositorio remoto, y tambien trae los cambios al directorio de trabajo sin alterar el área de staging, es equivalente a hacer un **fetch** en simultáneo con un **merge** entre el directorio local y el repositorio local, el cual ya fue actualizado con los últimos cambios en el repositorio remoto mediante **fetch**.

### Subir cambios del repositorio local al repositorio remoto

```bash
git push [parámetros] [nombre del repositorio remoto] [nombre de la rama]
```

Envía los cambios hechos en los tags o en una rama del repositorio local al repositorio remoto, por lo tanto si se quieren enviar los cambios más recientes del directorio local al repositorio remoto primero se realizan un **pull**, un **add**, un **commit** y luego un **push**, esta secuencia de comandos se usa para traer los cambios más recientes del repositorio remoto al local, para enviar los cambios del repositorio local al área de staging luego al repositorio local y por último al repositorio remoto, algunos de los parámetros más útiles al utilizar **git push** son:

- **--all:** Actualiza todas las ramas del repositorio remoto con los cambios de las ramas del repositorio local, al utilizar este parámetro no hace falta indicar el nombre de una rama en concreto.
- **-u, --set-upstream:**

## Conexión con **GitHub** usando protocolo SSH

<p align="center">
<img src="images/github_ssh_connection.png" width="100%" height="auto"/>
</p>

Establecer que las conexiones a un repositorio en **GitHub** se hagan con el protocolo SSH en lugar del HTTPS permiten agregar al repositorio una capa adicional de seguridad, ya que de esta forma los archivos enviados entre el repositorio remoto y cualquier otra máquina están totalmente cifrados y protegidos, **GitHub** usa una llave privada y una llave pública para conseguir este cifrado, el cual se basa en una serie de algoritmos de cifrado y descifrado asimétricos usando el par de llaves para cifrar y descifrar los archivos, de tal forma que para poder descifrar cualquier archivo cifrado con una llave pública es necesario tener la contraparte privada de esa llave, la cual se crea y vincula al mismo tiempo en el que se crea la llave pública, la llave privada bajo ninguna circunstancia debe salir de la máquina que establece la conexión SSH con **GitHub**. Para crear una conexión SSH bilateral, cifrada y segura entre cualquier máquina y **GitHub** hace falta por lo tanto crear las dos llaves en la máquina que va a establecer la conexión, una privada y una pública, la llave pública se comparte con **GitHub** y **GitHub** compartirá su llave pública de vuelta, cifrada con la llave pública enviada previamente, de esta forma tanto en la máquina que va a establecer la conexión como en **GitHub** hay una llave privada y una pública, lo que permite a **GitHub** descifrar los dato enviados desde la máquina local y a la máquina local descifrar los datos de **GitHub** para así establecer una conexión bilateral totalmente segura a través de internet.\
Las llaves SSH se asocian a un usuario, sin embargo, si se quiere acceder a los repositorios del mismo usuario desde diferentes dispositivos lo adecuado es tener una llave diferente por cada dispositivo. Las llaves SSH en **GitHub** se agregan en la sección **profile>settings>SSH and GPG keys** tras agregar la llave SSH al usuario será necesario cambiar la url local del repositorio remoto para usar una conexión SSH en lugar de la típica HTTPS, hacer un **pull** para traer los cambios de protocolo y una autenticación para usar SSH en lugar de HTTPS.

### Crear par de llaves

```bash
ssh-keygen -t rsa -b 4096 -C "[Correo electrónico vinculado al usuario de GitHub]"
```

Genera un par de llaves, al crear las llaves permite agregar un password a las llaves para tener más seguridad al usarlas. Al generarse el par de llaves la llave privada se deja sin extensión y la pública tendrá una extensión **.pub**.

### Comprobar funcionamiento del servidor SSH

```bash
eval $(ssh-agent -s)
```

Verifica que el servicio encargado de las llaves SSH esté activo.

### Agregar llave al servidor SSH

```bash
ssh-add ~/.ssh/id_rsa
```

Agrega al servidor SSH las llaves privadas para así usarlas posteriormente para descifrar mensajes en conexiones SSH hechas con la contraparte pública de la llave.
