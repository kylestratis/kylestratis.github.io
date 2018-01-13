---
layout: post
title: Configura iTerm2 con oh-my-zsh y powerline en OSX
comments: true
tags: [ terminal, bash ]
---

Una de las grandes ventajas de usar OSX sobre Windows para desarrollo web es que, al ser un sistema operativo basado en Unix. Esto facilita mucho las cosas a la hora de configurar el sistema y sobretodo a la hora de usar la terminal.

Desgraciadamente la terminal que viene por defecto con OSX es algo limitada, por lo que hace mucho tiempo tomé la decisión de instalar [iTerm2](https://www.iterm2.com). Me permite dividir paneles, usar hotkeys y otras cosas que no se pueden hacer con la terminal de fábrica.

Estos son los pasos para usar mi configuración:

## Instala iTerm
La forma más sencilla de instalarla es [desde su web](https://www.iterm2.com). Pero también la puedes instalar utilizando homebrew. Deberás ejecutar:

```
## asegurate de que está instalado cask (plugin para brew)
$ brew install cask

## instala iTerm2
$ brew cask install iterm2

```

## Tema Solarized para iTerm2
Instala el tema ejecutando:

```
$ brew install wget
$ cd ~/Downloads
$ wget https://raw.github.com/altercation/solarized/master/iterm2-colors-solarized/Solarized%20Dark.itermcolors

```

Una vez instalado, deberás de abrir iTerm2 e importar el tema descargado:
*iTerm > Preferences > Profiles > Colors > Load presets > Import*

## Oh my zsh
Oh-my-zsh es una alternativa a `bash`, que viene instalado por defecto con bash. Lo bueno es que ambos funcionan a la vez, así que instalarlo no debería de repercutir en nada.

El comando es:

```
$ curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```
Una vez instalado, abre `~/.zshrc` con un editor y configura el tema para `zsh`: `ZSH_THEME="agnoster"`


## Tipografía PowerLine
La fuente PowerLine se encarga de añadir iconos a la terminal. Son muy útiles y enriquecen visualmente la terminal.
Un ejemplo es cómo se ven las ramas de Git:

![Ejemplo powerline]({{ site.url }}/assets/powerline.png)

[Descárgala desde este enlace](https://github.com/powerline/fonts/blob/master/Inconsolata-g/Inconsolata-g%20for%20Powerline.otf). Deberás de instalarla en tu sistema y aplicarla en iTerm accediendo:

*iTerm > Preferences > Profiles > Text*

Personalmente utilizo 12pt como tamaño de fuente. Deberás escoger PowerLine en Regular Font y Non-ASCII Font haciendo click en los botones que dicen Change font escogiendo PowerLine.

## Conclusión
Si has llegado a este punto, quiere decir que has conseguido instalar y configurar `zsh` correctamente. Felicidades! Si te queda cualquier duda, no dudes en ponerte en contacto conmigo!
