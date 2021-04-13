# Sistemas Linux

<p align="center">
<img src="imagenes/notas_de_sistemas_linux/componentes_principales_de_linux.png" width="50%" height="auto"/>
</p>

Los sietmas Linux se componen de:

- Kernel: Es el núcleo del sistema operativo ademas de que ahí es donde se gestionan todos los recursos de hardware y los periféricos conectados al computador.
- Shell: Es el interprete, es un programa que tiene una interface de usuario y nos permite ejecutar las aplicaciones en un lenguaje de alto nivel y procesarlas en un lenguaje de bajo nivel.
- Aplicaciones: Son las aplicaciones con las que interactuamos para realizar alguna actividad y por debajo estas ejecutan acciones directamente en el kernel.

En los sistemas Linux existen varios tipos de shell, estos son:

1. SH: También conocida como Shell Bourne, es la primera shell creada para un sistema operativo linux, se puede utilizar actualmente, pero se perderían funcionalidades como autocompletar archivos o el historial de comandos.
1. KSH: Escriba por el programador David Korn. Intenta combinar las características de la CSH, TCSH y SH.
1. CSH: En una shell diseñada para que los usuarios puedan escribir programas de scripting de shell con una sintaxis muy simiar a la de C. En muchas sistemas como Red Hat, csh es tcsh, una versión mejorada de csh.
1. BASH: También conocida como Shell Bourne-Again, es una versión actualizada de SH creada por la Free Software Fundation. Es una de la shell más utilizada y conocida en el mundo. Incorpora alguna de las funcionalidades más avanzadas de KSH, CSH, SH y TCSH. Una de la funcionalidades más destacables de esta shell es la opción de ejecutar múltiples programas en segundo plano a la vez.
1. ZSH: Potente intérprete de comandos que puede funcionar como shell interactiva y como intérprete de lenguaje de scripting. aún siendo compatible con Bash.

## Comandos Bash

## Scripts Bash

La idea básica de generar programas en bash es poder ejecutar múltiples comandos de forma secuencial en muchas ocasiones para automatizar una tarea en especifico. Estos comandos son colocados en un archivo de textos de manera secuencial para poder ejecutarlos a posterioridad.

Para agregar un interprete a un script bash en Linux es necesario indicar elinterprete en la primera linea, cmo se muestra a continuacion.

```bash
# !/bin/bash
```

Las dos formas de ejecutar un Script Bash en Linux son:

```bash
bash script.sh
```

```bash
./script.sh
```
