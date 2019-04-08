## JOSE MIGUEL PELEGRINA PELEGRINA
## COMPAÑERO: JUAN SALVADOR MOLINA MARTÍN

# PRACTICA 5: REPLICACIÓN DE BASES DE DATOS MySQL

## Objetivos de la práctica

Los objetivos concretos de esta práctica son:

	Crear una BD con al menos una tabla y algunos datos.
	Realizar la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria.
	Restaurar dicha copia de seguridad en la segunda máquina (clonado manual  de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.
	Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

**Crear una BD con al menos una tabla y algunos datos.**

Desde la maquina-1 nos creamos una pequeña base de datos utilizando MySQL.Además de tener que introducir algunos datos para comprobar que nos funciona.

Para conectarnos a MySQL tenemos que:

	mysql -u root -p

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_1.png)

Nos creamos la base de datos llamada contactos y dentro de ella nos crearemos la tablas.

	create database contactos;
	use contactos;
	create table datos(nombre varchar(100),tlf int);
	show tables;

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_2.png)

Vemos que nuestras tablas están vacias por lo que insertamos datos de prueba.

	insert into datos(nombre,tlf) values ("jose",671346523);
	insert into datos(nombre,tlf) values ("miguel",689783456);
	insert into datos(nombre,tlf) values ("salva",689731265);
	insert into datos(nombre,tlf) values ("alex",656980912);
	insert into datos(nombre,tlf) values ("antonio",667123123);

Y ahora podemos ver las tablas

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_3.png)

**Realizar la copia de seguridad de la BD completa usando mysqldump en lamáquina principal y copiar el archivo de copia de seguridad a la máquina secundaria.**

MySQL ofrece la una herramienta para clonar las BD que tenemos en nuestra maquina. Esta herramienta es mysqldump.Mysqldump es parte de los programas de cliente de MySQL, que puede ser utilizado para generar copias de seguridad de BD.

La idea es que tenemos que tener en cuenta que los datos pueden estar actualizándose constantemente en el servidor de BD principal. En este caso, antes de hacer la copia de seguridad en el archivo .SQL debemos evitar que se acceda a la BD para cambiar nada.

Desde la máquina-1 hacemos:

	mysql -u root –p
	FLUSH TABLES WITH READ LOCK;
	quit

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_4.png)

Guardamos los datos.

mysqldump contactos -u root -p > /tmp/ejemplodb.sql
Como habíamos bloqueado las tablas, debemos desbloquearlas (quitar el “LOCK”):

	mysql -u root –p
	mysql> UNLOCK TABLES;
	mysql> quit

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_5.png)

Desde la maquina-2.

	scp maquina1:/tmp/ejemplodb.sql /tmp/

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_6.png)

Nos tenemos que crear la base de datos en la máquina-2:

	mysql -u root –p
	mysql> CREATE DATABASE contactos;
	quit

Ahora los exportamos.

	mysql -u root -p contactos < /tmp/ejemplodb.sql

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_7.png)

Nos metemos en sql de la máquina-2.

	mysql -u root –p
	use contactos;
	select * from datos;

![imagen](https://github.com/josemi10/swap1819/blob/master/practica5/imagenes/captura_8.png)

**Restaurar dicha copia de seguridad en la segunda máquina (clonado manual de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.**

**Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.**
