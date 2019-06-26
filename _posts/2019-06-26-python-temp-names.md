---
layout: post
title:  "Python: nombres aletorios"
date:   2019-06-26 13:28:41 +0200
categories: [python]
---



```python
'''
biblioteca tempfiles

enlaces de interés: 
* https://docs.python.org/3/library/tempfile.html
* https://stackoverflow.com/questions/10501247/best-way-to-generate-random-file-names-in-python
* https://pymotw.com/3/tempfile/
'''
```


```python
import tempfile
```


```python
# Fichero en carpeta temporal con nombre aleatorio
path = tempfile.NamedTemporaryFile()
print(path)
```


```python
# Directorio en carpeta temporal con nombre aleatorio
path = tempfile.mkdtemp()
print(path)
```

    /tmp/tmp92hxkigr



```python
# El prefijo por defecto es `tmp`, podemos definir otro y también sufijos
path = tempfile.mkdtemp(prefix='aa', suffix='zz')
print(path)
```

    /tmp/aanvovklgnzz



```python
# Podemos cambiar la carpeta temporal por el directorio que decidamos
path = tempfile.mkdtemp(dir='/home/felipem')
print(path)
```

    /home/felipem/tmpzvrgq88z
