---
layout: post
title: Atajos para tu terminal
category: desarrollo
tags: [ terminal, bash, nodejs, javascript ]
comments: true
---

Probablemente la forma más sencilla de instalar [Node.js](https://nodejs.org/) y npm en OS X, sea a utilizando el método estándar, bajando el instalador específico para tu sistema y asegurarte que lo instalas en tu `$PATH `.

Pero si prefieres utilizar [Homebrew](http://brew.sh/) para instalar paquetes en tu sistema, esta es tu guía. Personalmente prefiero este método ya que todos los paquetes que instales en tu sistema se instalan utilizando los mismos comandos y sobretodo facilitamos que podamos hacer uso de Homebrew para actualizarlos.

[Node.js](https://nodejs.org/) es un framework ideal para el desarrollo front end, puesto que nos brinda unas herramientas que nos facilitan (y mucho) la automatización de procesos. En otros posts explicaré más a fondo qué herramientas existen, pero de momento empezaremos por instalar Node.js y npm, su herramienta de gestión de paquetes.

## Primero instalamos Homebrew

```
$ ruby -e '$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)'

```


## Después nos aseguraremos de que está actualizado:

```
$ brew update
```

Recomiendo que utilices brew doctor para asegurarte que está todo correctamente instalado y funcionando. Doctor te avisará de cualquier problema que pueda surgir y cómo solucionarlo:

```
$ brew doctor
```

Lo siguiente será agregar Homebrew a la ubicación de tu PATH. Además deberás de “sourcear” tu bash:

```
$ export PATH='/usr/local/bin:$PATH'
```

Ya puedes instalar Node.js y npm (cuando instalas node, también instalas npm):

```
$ brew install node
```

Para comprobar que has instalado Node correctamente, prueba de instalar Gulp (puede que lo tengas que hacer con sudo):

```
$ npm install --global gulp
```

## Conclusión

Si todo ha funcionado correctamente, ¡enhorabuena! ya puedes empezar a trabajar en tu proyecto. Si no lo has conseguido, deja un comentario y le echamos un vistazo :)
