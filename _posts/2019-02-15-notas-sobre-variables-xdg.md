---
layout: post
title:  "Notas sobre variables XDG"
date:   2019-02-15 16:00:02 +0100
categories: [linux , notas]
---
Esto solo es una recopilación de anotaciones sobre un tema que me ha parecido curioso, a raíz del artículo [dotfiles-madness](https://0x46.net/thoughts/2019/02/01/dotfile-madness/) busqué información sobre la especificación [XDG Base Directory](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

Esta especificación pertenece a [freedesktop.org](https://www.freedesktop.org/wiki/), un proyecto open source con la intención de que los diferentes escritorios basados en [X11](https://es.wikipedia.org/wiki/Sistema_de_ventanas_X) convivan entre ellos.

La especificación consiste en una buena práctica para organizar los ficheros de nuestras aplicaciones.

Me llama la atención que las distribuciones no tenga declaradas las variables, éstas solo se deben establecer cuando tengan un valor diferente al de por defecto. Esto quiere decir que cuando realizamos el programa, debemos comprobar si está asignada la variable y, si no, decirle nosotros cuál es el lugar por defecto.

A esto le veo algunos problemas como:

* En programas amateur puede no tener en cuenta que no estén establecidas las variables si su desarrollador las tiene.
* Que los valores que utilice por defecto no sean los de la especificación (puede ser intencionado o por error)

Parece que quienes deciden usarlas las establecen en su `.bashrc`, ejemplo:

```bash
export XDG_DATA_HOME=${XDG_DATA_HOME:="$HOME/.local/share"}
```

Pero al final, terminamos dando al sistema unas variables _por si acaso_, que precisamente se querían evitar. Por cierto, sí que existen otras como `XDG_DATA_DIRS`, que nos da un listado de diferentes rutas.

Hasta aquí mis notas. Para informarme un poco he usado también información encontrada en [askubuntu](https://askubuntu.com/questions/tagged/xdg-base-directory) y [superuser](https://superuser.com/questions/tagged/xdg).

Creo que intentaré usarlo en próximos programas porque me parece buena práctica, pero como comentan en este [hilo](https://news.ycombinator.com/item?id=19063727&utm_term=comment), hay muchos más problemas y complejidad que no se solucionan solo definiendo unas rutas.

