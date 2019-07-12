---
layout: post
title:  "Terminal quake"
date:   2019-07-12 23:32:49 +0200
categories: [linux]
---

Los mayores del lugar recordarán [Quake](https://es.wikipedia.org/wiki/Quake_(videojuego)), uno de los videojuego más populares de los 90s. Una característica de este juego de disparos era que permitía abrir un terminal donde, con comandos, ejecutar instrucciones para cambiar opciones o meter trucos.  

Hace muchos años añadieron la posibilidad de abrir un terminal de linux con ese aspecto y comportamiento, deslizándose desde la parte superior y ocupando solo una parte de la pantalla sobre las ventanas activas y poder usarlo. Hasta hace unas semanas no lo había probado y resulta que me parece muy útil.

Para activar este modo necesitamos un terminal que tenga implementado este modo, de los varios que podemos encontrar, el que me ha parecido mejor es [Tilix](https://gnunn1.github.io/tilix-web/).

Una vez instalado, lo ejecutamos y si vamos a preferencias encontramos una sección llamada `quake`, ahí podemos configurar algunos elementos del comportamiento que tendrá la ventana. En mi caso active que se ocultase al perder el foco, y que se mostrase siempre en el mismo monitor.

Una vez configurado el comportamiento, debemos asignar una tecla o combinación para abrirlo, para ello vamos a los `shortcuts` del gestor de ventanas (no de tilix). En mi caso utilizo la tecla `menú`, que está situada a la izquierda del `ctrl` derecho, y el comando que asignamos es:

```sh
tilix --quake
```

