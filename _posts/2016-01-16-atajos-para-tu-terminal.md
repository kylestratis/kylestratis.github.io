---
layout: post
title: Atajos para tu terminal
category: desarrollo
tags: [ terminal, bash ]
comments: true
---

Si utilizas la terminal a menudo, te habrás encontrado con que en ocasiones tienes que escribir comandos bastante largos. Si esto lo multiplicamos por los cientos de comandos que podemos acabar escribiendo, es el momento de añadir atajos a tu .bash_profile. Estos atajos se conocen como "alias".

El .bash_profile es un archivo que se encuentra en tu directorio raíz, con el que puedes personalizar tu sesión en la terminal. Vamos a trabajar en un par de ejemplos.

## Arranca un servidor

Un alias que encuentro extremadamente útil es para arrancar un servidor Python básico con un solo comando. Para muchos proyectos, acostumbro a utilizar el servidor básico de python. Normalmente, en la carpeta de mi proyecto, arranco el servidor así:

```
$ python -m SimpleHTTPServer 8000
```

Vamos a crear un alias:

```
alias httpserver="python -m SimpleHTTPServer 8000"
```

Y lo añadimos al .bash_profile:

```
$ source ~/.bash_profile
```

Así, la próxima vez que tengas que arrancar un servidor, podrás escribir:

```
$ httpserver
```

## Accede a tus carpetas rápido

Cuando tienes que acceder carpetas determinadas, a veces se puede hacer muy pesado. Por ejemplo:

```
$ cd ~/Sites/mi-web/mi-carpeta/otra-carpeta/mas-carpetas
```

Vamos a crear un alias:

```
$ alias carpeta="cd ~/Sites/mi-web/mi-carpeta/otra-carpeta/mas-carpetas"
```

Y lo añadimos al .bash_profile:

```
$ source ~/.bash_profile
```

Así, la próxima vez que tengas que arrancar un servidor, podrás escribir:

```
$ carpeta
```

## Conclusión

Espero que estos dos ejemplos hayan sido útiles. Puedes aplicar los mismos conceptos para todo tipo de acciones. Si te ha gustado el artículo, no dudes en compartirlo!
