## JOSE MIGUEL PELEGRINA PELEGRINA
## COMPAÑERO: JUAN SALVADOR MOLINA MARTÍN

# PRACTICA 2: CLONAR INFORMACIÓN DE UN SITIO WEB

## Objetivos de la práctica

**Los objetivos concretos de esta segunda práctica son:**

	 1.Aprender a copiar archivos mediante ssh
	 2.Clonar contenido entre máquinas
	 3.Configurar el ssh para acceder a máquinas remotas sin contraseña
	 4.Establecer tareas en cron

**1.Aprender a copiar archivos mediante ssh**

Desde las dos maquinas virtuales que tenemos que pasar un directorio y mediante ssh del equipo que queremos enviar en un tar.gz.

Nosotros enviaremos un directorio desde la maquina-1 a la maquina-2.Esta podremos reconorcerla por la IP.

Pondremos el siguiente comando:

	tar czf - ./hola/paquete.txt | ssh 192.168.1.101 'cat > ~/tar.tgz'

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/tar.png)

Desde la maquina-2 ejecutamos el comando para descomprimirlo:

	tar -xvf tar.tgz

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/tar2.png)

Observamos que el paquete.txt lo tenemos.

Sin embargo, esto que puede ser útil en un momento dado, no nos servirá para sincronizar grandes cantidades de información. En ese caso, va mejor la herramienta rsync.

**2.Clonar contenido entre máquinas**

Para clonar el contenido haremos uso de la herramienta rsync.Lo primero que debemos hacer es llevar a cabo su instalación:

	sudo apt-get install rsync

Lo primero que tenemos que hacer es darle permiso al directorio donde vamos a clonar la información y en el directorio donde vamos a tenerlo.Además vamos a crear algunos ficheros para que podamos clonarlos.

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/touch.png)

Ahora ya podemos clonar la información escribiendo el siguiente comando:

	rsync -avz -e ssh 192.168.1.100:/var/www/ /var/www/

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/rsync.png)

Ahora miramos desde la máquina-2 para comprobar que están los ficheros con el siguiente comando:

	ls /var/www

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/ls_s2.png)

**3.Configurar el ssh para acceder a máquinas remotas sin contraseña**

Para el uso de la herramienta ssh de las maquina-1 y máquina-2 sin que tenga que intervenir el administrador podemos usar método como el ssh-keygen para que no nos estén pidiendo contraseñas.

El objetivo es que podamos acceder a ambas máquinas sin que nos pidan la contraseña.

Hacemos uso de los siguientes comandos:

	ssh-keygen -b 4096 -t rsa

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/keygen.png)

	ssh-copy-id 192.168.1.101
	chmod 600 ~/.ssh/authorized_keys

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/ssh-copy-id.png)

Para la maquina-2 tenemos que hacer lo mismo.Ahora ya podremos acceder de una máquina a otra sin la contraseña.

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/ssh_sin_contrase%C3%B1a.png)


**4.Establecer tareas en cron**

El uso de rsync puede ser más interesante con el uso del cron con el que podemos ejecutarlo en segundo plano para que no tengamos que estar ejecutando el comando de forma repetida.

Lo único que tenemos que hacer es acceder al fichero /etc/crontab

![imagen](https://github.com/josemi10/swap1819/blob/master/practica2/imagenes/contrab.png)
