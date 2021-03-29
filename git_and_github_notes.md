# Git y GitHub

[**Git**](https://git-scm.com/) es el sistema de versionamiento o control de versiones más popular del mundo, Git permite guardar el historial de cambios y el crecimiento de los archivos de un proyecto, sin guardar el archivo completo ya que muchas veces los cambios son muy simples, de tal modo que Git guarda los cambios de forma atómica e incremental, por lo que cada cambio se escribe sobre el anterior y así sucesivamente desde la versión inicial de un archivo del proyecto, GitHub por su parte permite que este versionamiento además se haga en una nube dedicada al versionamiento de archivos, y además permite trabajo colaborativo sobre los archivos del proyecto.
Git soporta versionamiento de archivos binarios, pero el versionamiento no es tan preciso como con archivos basados en texto plano, por lo que normalmente se utiliza solo para archivos de texto plano.

## Comandos básicos

### Mostrar ayuda de un comando para

```bash
git
```

Muestra algunos de los comandos más comunes usados en git.

### Mostrar ayuda de un comando

```bash
git [comando] --help
```

Muestra los parámetros y funciones de un comando, si no se incluye un comando es equivalente a **git**.

### Iniciar un repositorio

```bash
git init
```

Inicia un repositorio git en la carpeta actual.

### Agregar archivos al repositorio

```bash
git add [ruta archivo o directorio]
```

Agrega al repositorio un archivo o directorio, por lo que el archivo o directorio entra en estado de stage, y es tomado en cuenta en la base de datos de cambios.

```bash
git add .
```

Lo más normal es usar **git add .** para agregar todos los archivos de la carpeta a la base de datos de cambios del repositorio.

### Registrar cambios en el repositorio

```bash
git commit -m "[comentario]"
```

Envía los últimos cambios al repositorio para que este los registre en la base de datos de cambios, los cambios además se registran con un comentario, que idealmente debe indicar qué cambios se realizaron en la última versión.

### Comprobar el estatus del repositorio

```bash
git status
```

Muestra el estatus de la base de datos de cambios del repositorio.

### Mostrar todos los cambios históricos hechos en el repositorio

```bash
git show
```

Muestra todos los cambios históricos hechos en el repositorio, incluyendo las líneas en las que se han hecho cambios, cuando se han hecho los cambios y quién los hizo.

### Mostrar todos los cambios históricos hechos en un archivo

```bash
git log [archivo]
```

Muestra todos los cambios históricos hechos en un archivo en concreto, incluyendo las líneas en las que se han hecho cambios, cuando se han hecho los cambios y quién los hizo.

### Eliminar archivos del repositorio

```bash
git rm [parámetros] [archivo]
```

Elimina del repositorio un archivo o directorio, por lo que el archivo o directorio sale del estado de stage, y deja de ser tomado en cuenta en la base de datos de cambios.

## Configuración de Git

```bash
git config [parámetros] [configuraciones]
```

Al ejecutarse sin parámetros muestra todas la configuración actual del repositorio, algunos de los parámetros más útiles al utilizar **git config** para configurar un repositorio son:

- **--list:** Muestra la configuración por defecto del repositorio.
- **--global:** Indica a Git que se va a cambiar la configuración de todos los repositorios globales.

Algunos de los parámetros configurables más importantes de un repositorio son:

- **user.name=[nombre del usuario]:** Cambia el nombre del usuario.
- **user.email=[correo del usuario]:** Cambia el correo electrónico del usuario.
