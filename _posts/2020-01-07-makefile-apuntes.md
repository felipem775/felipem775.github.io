---
layout: post
title: "makefile, mis apuntes"
date: "2020-01-07 11:34:26"
categories: [linux]
---
# Makefile

make es un software que viene por defecto en sistemas \*nix, y se utiliza normalmente para compilar software a partir de su código fuente.

Su [artículo en la wikipedia](https://es.wikipedia.org/wiki/Make) es muy completo, por lo que aquí simplemente voy a añadir algunas anotaciones sobre problemas que he ido encontrando.

El mejor nombre para el fichero de receta es `Makefile` [1], aunque sí queremos utilizar otro nombre, podemos utilizar `-f name` o `--file=name`

## CLI

Aunque la sintaxis es similar a bash, no es la misma. Los `makefiles` contienen *reglas explícitas*, *reglas implícitas*, *definición de variables*, *directivas* y *comentarios* [2]

Si no pasamos ningún argumento a `make`, ejecutará solo la primera sección que encuentre.

No se le pueden pasar variables directamente, pero las puede tomar de la sesión, por lo que podemos exportarlas antes de llamar a make y que él haga uso de ellas dentro de la receta.

## Comandos

Los comandos a ejecutar deben ir precedidos de una tabulación, poner espacios en blanco no sirve.

Si queremos omitir el texto del comando en pantalla, podemos añadir `@` tras la tabulación. Afectará a toda la línea.

## Directivas

Para evitar problemas con nombres de secciones igual que otros ficheros, usamos `.PHONY`. Así, al comienzo del fichero podemos poner `.PHONY: install clean release`

Cada comando se ejecuta en un shell independiente, no solo la sección. Es decir, si ejecutamos un comando para cargar un `virtualenv`, el comando de la siguiente línea no lo tendrá cargado, debemos hacerlo en la misma línea. O bien usar `.ONESHELL:` antes de cada sección [3]


[1]: https://www.gnu.org/software/make/manual/html_node/Makefile-Names.html#Makefile-Names
[2]: https://www.gnu.org/software/make/manual/make.html#Makefiles
[3]: https://unix.stackexchange.com/questions/475983/makefile-and-oneshell
