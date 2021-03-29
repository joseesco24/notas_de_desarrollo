# Git y GitHub

[**Git**](https://git-scm.com/) es el sistema de versionamiento o control de versiones más popular del mundo, Git permite guardar el historial de cambios y el crecimiento de los archivos de un proyecto, sin guardar el archivo completo ya que muchas veces los cambios son muy simples, de tal modo que Git guarda los cambios de forma atómica e incremental, por lo que cada cambio se escribe sobre el anterior y así sucesivamente desde la versión inicial de un archivo del proyecto, GitHub por su parte permite que este versionamiento además se haga en una nube dedicada al versionamiento de archivos, y además permite trabajo colaborativo sobre los archivos del proyecto.
Git soporta versionamiento de archivos binarios, pero el versionamiento no es tan preciso como con archivos basados en texto plano, por lo que normalmente se utiliza solo para archivos de texto plano.

## Comandos

### Iniciar un repositorio

```bash
git init
```

Inicia un repositorio git en la carpeta actual.

### Agregar archivos al repositorio

```bash
git add [ruta archivo o directorio]
```

Agrega al repositorio un archivo o directorio para que sea tomado en cuenta en la base de datos de cambios.

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

Elimina un archivo del repositorio.
