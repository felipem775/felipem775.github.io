---
layout: post
title:  "Radon y Complejidad ciclomática"
date:   2019-06-20 13:20:56 +0200
categories: [python]
---

[Radon](https://github.com/rubik/radon) es una herramienta para calcular métricas de código `python`.  
Implementa _Complejidad Ciclomática_, una métrica basada en las estructuras de control, para ello busca el número máximo de pasos que tiene que realizar un código y se le asigna un valor. Mejor explicado en la wikipedia [es](https://es.wikipedia.org/wiki/Complejidad_ciclom%C3%A1tica) y [en](https://en.wikipedia.org/wiki/Cyclomatic_complexity).  
Una vez radon Evalúa El Código, nos devuelve una nota de A (óptimo) a F (pésimo), y ya nos podemos hacer una idea de si el código que tenemos es complejo para que otra persona o nosotros mismos podamos realizar modificaciones o simplemente entender lo que hace. Deberíamos decidir una nota mínima y cualquier código que veamos con una nota inferior, esforzarnos en refactorizarlo, en el futuro lo agradeceremos.

Con el siguiente comando veremos los resultados de un fichero o carpeta:

```sh
radon cc -s tar_files_size/tar_file_size.py 
tar_files_size/tar_file_size.py
    F 46:0 set_log_level_from_verbose - A (5)
    F 15:0 filesInDir - A (3)
    F 25:0 split_in_max_size - A (3)
    F 40:0 do_tar - A (2)
    F 22:0 sizeFile - A (1)
```

* `F` indica que se trata de una función. Podría ser `M` de método o `C` de clase.
* `46:0` indica en qué parte del fichero comienza.
* `set_log_level_from_verbose` es el nombre de la función.

* `A` es la nota para esa función. y el `5` es el resultado numérico (cuanto mayor peor).
