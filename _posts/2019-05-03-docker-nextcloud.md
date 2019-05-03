---
layout: post
title:  "Docker: nextcloud"
date:   2019-05-03 23:35:21 +0100
categories: [docker]
---

Para el uso en una red local, netcloud es bastante sencillo de utilizar con docker, pero hay un par de detalles que hay que tener en cuenta por lo que me he hecho unos apuntes.

Las instrucciones generales las encontramos en su [repositorio de github](https://github.com/nextcloud/docker).

Con el siguiente comando descargaremos la última versión estable y la lanzaremos utilizando un directorio del host para mantener la persitencia de los ficheros, nos conectaremos al servidor por el puerto 8080:

```sh
sudo docker run --restart=always -d -v /mnt/disk2/nextcloud/var/www/html:/var/www/html -p 8080:80 nextcloud
```

Con la instalación como la tenemos solo podremos conectarnos desde `localhost`, si queremos entrar desde otros equipos deberemos añadirlo a un fichero de configuración:

* Buscamos el contenedor donde se está ejecutando:
  
```sh
sudo docker ps
d095e5b3f7ba        nextcloud           "/entrypoint.sh apac…"   3 hours ago         Up 2 hours          0.0.0.0:8080->80/tcp
```

* Nos conectamos por ssh:

```sh
sudo docker exec -ti d095e5b3f7ba bash
```

* Editamos el fichero de configuración (puede que tenamos que instalar un editor):

```sh
root@d095e5b3f7ba:/var/www/html# vim config.php 
```

* En el fcihero modificamos el array `trusted_domains` para añadir las ips.

* Por último reinicamos el contenedor.

```sh
sudo docker restart d095e5b3f7ba 
```