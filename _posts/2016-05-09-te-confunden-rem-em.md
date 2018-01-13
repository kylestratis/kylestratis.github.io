---
layout: post
title: ¿Te confunden REM y EM?
category: CSS
comments: true
tags: [ css, rem, em ]
---

**REM** puede ser confuso, especialmente si no tienes un entendimiento sólido de su compañera **EM** y su némesis, **PX**.

## Unidades Relativas

Tanto `rem` como `em` son unidades relativas, a diferencia de `px`, que no lo es. Antes que consideres utilizar `rem`, es importante que entiendas la relación entre `em`, tu markup y herencia.

En el ejemplo de debajo, se demuestra cómo cada hijo anidado asume que el padre es `1em` (100%). Por lo tanto, sus hijos heredan su tamaño escalando en relación al tamaño de fuente de su padre.

Los valores **EM** se heredan de sus parientes

<pre class="codepen" data-height="470" data-type="result" data-href="rCcIh" data-user="jeremychurch" data-safe="true"> <code> </code> <a href="http://codepen.io/jeremychurch/pen/rCcIh">Check out this Pen!</a> </pre>
<script src="http://codepen.io/assets/embed/ei.js"> </script>

Los valores **PX** no se heredan

<pre class="codepen" data-height="470" data-type="result" data-href="dlyqw" data-user="jeremychurch" data-safe="true"> <code> </code> <a href="http://codepen.io/jeremychurch/pen/dlyqw">Check out this Pen!</a> </pre>
<script src="http://codepen.io/assets/embed/ei.js"> </script>

Mientras el valor se queda en `0.733em`, el tamaño de fuente se calcula al `77,3%` de su pariente directo, que a su vez escala de su pariente. Esto irá sucediendo a medida que subimos hacia arriba en el DOM. De hecho sucederá allá donde un pariente tenga definida una `font-size`.

En este ejemplo, tenemos varios elementos “nesteados”. Cada uno de ellos tiene un tamaño de font. Seguro que puedes observar que no es una buena práctica, puesto que el conjunto de la herencia crea resultados no deseados. De todos modos, no deberías de preocuparte sobre esto, siempre y cuando tu CSS y html sean modulares.

## EM salva vidas

Bueno, quizá salvar vidas sea algo exagerado, pero ahorrar líneas de código, seguro. Los ejemplos que ves a continuación, hacen eso mismo: actualizar los tamaños de tipografía dentro de una media query. Los valores iniciales se calculan incrementando `1em` (16px) en un ratio de 1:1.2.

EM escala cuando se actualiza un valor:

{% highlight css %}
html { font-size: 1em; }

h1 { font-size: 2.074em; }

h2 { font-size: 1.728em; }

h3 { font-size: 1.44em; }

h4 { font-size: 1.2em; }

small { font-size: 0.833em; }

.caja { padding: 1.25em; }

@media screen and (min-width: 1400px) { html { font-size: 1.25em; } }
{% endhighlight %}

O tendrías que recalcular cada valor **PX**

{% highlight css %}
html { font-size: 16px; }

h1 { font-size: 33px; }

h2 { font-size: 28px; }

h3 { font-size: 23px; }

h4 { font-size: 19px; }

small { font-size: 13px; }

.caja { padding: 20px; }

@media screen and (min-width: 1400px) { html { font-size: 20px; }
{% endhighlight %}

Solamente hay un valor em para sobre escribir en la media query, porque em hereda y escala relativa al tamaño de fuente de su padre (html en este caso), de forma similar a la que escalaría, por ejemplo, paths vectoriales.

Si tuviéramos que hacer lo mismo con `px`, necesitaríamos casi el doble de código, puesto que cada uno de estos valores, debe de ser recalculado y definido en la media query.

## REM cómo en “Root EM”

Mientras que `em` es relativa al tamaño de fuente de su pariente directo (o más cercano), `rem` es relativo exclusivamente al tamaño de fuente del documento (html), también conocido cómo “root” (raíz). Si construyes tus hojas de estilos de forma modular, `rem` es algo que apenas utilizarás, pero aún así, te puede ser muy útil en más de una ocasión.

Por ejemplo, si estás buscando conseguir un espaciado consistente en tu página, sin tener que utilizar código de más, rempuede ser utilizado para definir tus paddings y márgenes.

**EM** escalará paddings y margins:

<pre class="codepen" data-height="470" data-type="result" data-href="AlxHk" data-user="jeremychurch" data-safe="true"> <code> </code> <a href="http://codepen.io/jeremychurch/pen/AlxHk">Check out this Pen!</a> </pre>
<script src="http://codepen.io/assets/embed/ei.js"> </script>

## Conclusión

Utilizo `em` para casi todo, `rem` de forma ocasional para paddings y márgenes, pero muy ocasionalmente y utilizo `px` para bordes.

Mayoritariamente, quiero que los hijos hereden tamaño. Si una columna va a tener un tamaño de fuente más pequeño, espero que todos sus hijos cambien su tamaño de forma proporcional, sin tener que calcular y redefinir selectores de forma individual.

Me cuesta pensar en una buena razón para utilizar `rem` para tamaños de fuente, pero estoy seguro de que puede haber excepciones. Si por ejemplo estoy intentando resetear un tamaño de fuente con `rem`, es probablemente señal de que mi CSS no es demasiado modular y por lo tanto, necesita mejoras.

## Recursos

Mi calculadora de `em` favorita es [pxtoem.com](https://pxtoem.com/). No solo calcula valores em o px, también nos ofrece una rambla muy útil que nos ayuda a ver su relación.

---

Este post ha sido traducido del inglés. Si quieres acceder a la versión original, fue escrita por Jeremy Church y la puedes acceder aquí: [Enlace](https://j.eremy.net/confused-about-rem-and-em/)
