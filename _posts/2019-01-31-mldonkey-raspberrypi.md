---
layout: post
title:  "MLdonkey en Raspberry PI"
date:   2019-01-31 22:03:21 +0100
categories: tutorial linux
---
Uno de los usos que se le puede dar a una raspberry es tenerla como servidor p2p.  
Es muy sencillo pero como lo configuro cada muchos meses, algunos detalles de la configuración se me olvidan.

# Configurar mldonkey en debian/raspbian usando almacenamiento USB

* 1 Instalación de disco usb
* 2 Instalación de mldonkey y configuración de usb
* 3 Configuración del servidor web
* 4 Configurar directorios
* 5 Configurar puerto en el router
 

## Instalación de disco usb 
Vamos a tener siempre conectado una unidad usb a nuestro RPi, así que vamos a configurarlo para que se monte siempre que arranquemos la máquina. 

Creamos un directorio donde se montará el dispositivo, asignamos propietario y permisos 

    mkdir /mnt/data32
    chown felipem /mnt/data32
    chmod 777 /mnt/data32

Configuramos el fichero fstab 

    /dev/sda1  /mnt/data32	ext4	defaults,noatime 0	0
	
## Instalación de mldonkey y configuración de usb 

Instalaremos **mldonkey-server** y **telnet** para poder conectarnos 

```sh
    apt-get install mldonkey-server telnet
```

Confirmamos que queremos que se ejecute al inicio. 

Ahora vamos a crear los directorios en el usb y ponemos de propietario a mldonkey 

```sh
    mkdir /mnt/data32/mldonkey/incoming/files -p
    mkdir /mnt/data32/mldonkey/incoming/directories
    mkdir /mnt/data32/mldonkey/temp
    chown -R mldonkey:mldonkey /mnt/data32/mldonkey
    chmod -R 777 /mnt/data32/mldonkey
```

## Configuración del servidor web 
   
Manejaremos mldoney desde el navegador web. 

Para configurar los primeros pasos necesitamos hacerlo desde telnet 

```sh
    telnet 127.0.0.1 4000
```

Nos identificamos y establecemos una contraseña nueva 

```
    auth admin ""
    passwd nuevaPassword
```	

Establecemos las IPs desde las que aceptará que nos conectemos 

```
    set allowed_ips "127.0.0.1 192.168.0.5 192.168.0.12"
```

Los cambios se aplican en el momento, pero para futuras sesiones hay que guardarlos 

```
    save
```

## Configurar directorios 

Desde el frontend web, vamos a 

```
	Options -> Shares ->  Add share
```

Introducimos la ruta para ficheros en el siguiente formato 

```
	0 /mnt/data32/mldonkey/incoming/files/ incoming_files
```	

De nuevo agregamos la ruta, esta vez para directorios 

```
	0 /mnt/data32/mldonkey/incoming/directories/ incoming_directories
```

Para definir la carpeta de temporales 

```
	set temp_directory "/mnt/data32/mldonkey/temp/"
```

Una vez añadidos sólo nos queda eliminar los antiguos con 

```
	Unshare
```

## Configurar puerto en el router 

Para saber qué puerto debemos abrir comprobamos el fichero donkey.ini 

	(* The port used for TCP connection by other donkey clients. UDP port = port + 4. *)
	(* changing this option requires restart of MLDonkey core *)
	port = 12240
	
En el router configuramos los puertos TCP 12240 y UDP 12244 al exterior y hacia nuestro equipo. 