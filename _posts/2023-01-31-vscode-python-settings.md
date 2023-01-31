---
title:  "Configuraciones de VSCode que uso para programar en Python"
date:   2023-01-31 17:27:00 -0500
categories: entorno-de-trabajo
tags: vscode python
---
Como buenos programadores debemos ser muy conscientes del código que estamos escribiendo para que este sea fácil de leer, cumpla con los estándares de estilo del lenguaje y sigan una estructura homogenea a lo largo de los proyectos. Para el caso de Python, se cuenta con el documento [PEP 8](https://peps.python.org/pep-0008/) que contiene una serie de convenciones que se sugieren seguir en el código para garantizar la legibilidad y consistencia del código.

Y que mejor forma de empezar a mejorar nuestro código que desde las herramientas que usamos para crearlo. Es por esto que en este artículo traigo algunas de las configuraciones que uso en VSCode para escribir un código estándar de Python.

**Tip:** Para acceder a la configuración de VSCode, presiona (`Ctrl` + `,`) o (`⌘` + `,`). De allí das click en el ícono de arriba a la derecha para acceder al archivo settings.json que corresponde a la configuración de VSCode en formato JSON.
{: .notice--info}

## Formateo al guardar un archivo

Para comenzar, una de las configuraciones primordiales que tengo en mi editor es la capacidad de formatear un archivo al momento de guardarlo

```json
"editor.formatOnSave": true,
"editor.formatOnSaveMode": "file",
```

Adicionalmente, utilizo la tercera configuración por convención de los sistemas Unix en donde se acostumbra a tener una línea vacía al final de cada archivo.

```json
"files.insertFinalNewline": true,
```

## Python formatter

Para comenzar a utilizar formatear nuestro código, debes tener instalada [la extensión de Python para VSCode](https://marketplace.visualstudio.com/items?itemName=ms-python.python). Y esta debes definirla como el **formatter** por defecto para tipos de archivo Python. 

```json
"[python]": {
    "editor.defaultFormatter": "ms-python.python"
}
```

**Importante:** Es importante recalcar que pueden haber varios tipos de archivos que no queremos que se formatee automáticamente. Para esto debemos asegurar que en nuestra configuración no haya un **formatter** por defecto para este tipo de archivos.
{: .notice--warning}

**Tip:** Por defecto, en VSCode puedes presionar (`Alt` + `Shift` + `F`) o (`⌥` + `⇧` + `F`) para formatear el archivo que tienes abierto.
{: .notice--info}

Ahora se debe definir el provider encargado de hacer el formateo. Para Python, se pueden utilizar: `autopep8`, `black`, `yapf`. Yo personalmente utilizo [black](https://github.com/psf/black) que es un formatter bastante utilizado por la comunidad. Sin embargo, black por defecto utiliza un límite de longitud de línea de 120 carácteres. Por esto es que se agrega la segunda configuración para cumplir con la [longitud sugerida de 79 carácteres](https://peps.python.org/pep-0008/#maximum-line-length).

```json
"python.formatting.provider": "black",
"python.formatting.blackArgs": [
    "--line-length",
    "79"
],
```

A partir de ahora, gracias a las configuraciones que se han mencionado se puede pasar de un código inconsistente y que no cumple las convenciones del PEP 8, a un código más legible y que sigue unos estándares definidos:

<!-- TODO: Agregar imágenes -->

Asimismo, utilizo líneas guía verticales para tener una referencia visual al momento de estar escrbiendo código. Para esto uso una guía en el carácter 72, recomendado para el límite de carácteres de los comentarios y 79 para el código como tal.

```json
"editor.rulers": [
    72,
    79
]
```

## Organizar imports automáticamente

Parte fundamental de tener un código legible es tener un orden específico para las dependencias o librerías que importamos en nuestro código. En el PEP 8, puedes encontrar una [sección](https://peps.python.org/pep-0008/#imports) específica para esto en donde recomiendan organizar los imports en los siguientes grupos:

1. Importar librerías estándar de Python. Por ejemplo: `os`, `re`, `datetime`.
2. Importar librerías de terceros. Por ejemplo: `requests`, `pandas`, `numpy`.
3. Librerías o paquetes propios del proyecto.

```json
"editor.codeActionsOnSave": {
    "source.organizeImports": true
},
"isort.args": [
    "--profile",
    "black"
]
```

<!-- TODO: Agregar ejemplo -->

## Linting

Por ultimo, cuento con la configuración propia para habilitar el [linting de Python](https://code.visualstudio.com/docs/python/linting). Esta nos permite ver posibles errores al momento de editar nuestro código sin necesidad de ejecutarlo.

```json
"python.linting.enabled": true,
"python.linting.pylintEnabled": true,
```

<!-- TODO: Agregar ejemplo -->
