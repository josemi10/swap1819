## JOSE MIGUEL PELEGRINA PELEGRINA
## COMPAÑERO: JUAN SALVADOR MOLINA MARTÍN

# PRACTICA 6: SERVIDOR DE DISCO NFS

## Objetivos de la práctica

**El objetivo principal de esta práctica es configurar un servidor NFS para exportar un espacio en disco a los servidores finales (que actuarán como clientes-NFS).**

Los objetivos concretos de esta práctica son:

	Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.
	Montar en las máquinas cliente la carpeta exportada por el servidor.
	Comprobar que todas las máquinas pueden acceder a los archivos almacenados en la carpeta compartida.
	Hacer permanente la configuración en los clientes para que monten automáticamente la carpeta compartida al arrancar el sistema.

**1.Configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes.**

En la máquina servidora(maquina-1 192.168.100) instalamos las herramientas necesarias:

	sudo apt-get install nfs-kernel-server nfs-common rpcbind

A continuación, creamos la carpeta que vamos a compartir y cambiamos el propietario y permisos de esa carpeta:

	mkdir /etc/dat/compartida
	sudo chown nobody:nogroup /etc/dat/compartida/
	sudo chmod -R 777 /etc/dat/compartida/

![imagen](https://github.com/josemi10/swap1819/blob/master/practica6/imagenes/captura_1.png)

Ahora nos metemos en el fichero de control /etc/exports y ponemos:

	/etc/dat/compartida/ 192.168.1.102(rw) 192.168.1.103(rw)

![imagen](https://github.com/josemi10/swap1819/blob/master/practica6/imagenes/captura_2.png)

Finalmente, debemos reiniciar el servicio:

	service nfs-kernel-server restart


![imagen](https://github.com/josemi10/swap1819/blob/master/practica6/imagenes/captura_3.png)

En los clientes (M1 y M2) debemos instalar los paquetes necesarios y crear el punto de montaje (el directorio en cada máquina cliente):

	sudo apt-get install nfs-common rpcbind
	cd /home/usuario
	mkdir carpetacliente
	chmod -R 777 carpetacliente

Ahora ya podemos montar la carpeta remota (la exportada en el servidor) sobre el directorio recién creado:

	sudo mount 192.168.1.100:/etc/dat/compartida carpetacliente

![imagen](https://github.com/josemi10/swap1819/blob/master/practica6/imagenes/captura_4.png)

Ahora nos creamos un fichero.txt vemos que se han creado en el resto de máquinas.

![imagen](https://github.com/josemi10/swap1819/blob/master/practica6/imagenes/captura_5.png)

Finalmente, para hacer la configuración permanente, debemos añadir una línea al archivo de configuración /etc/fstab en las máquinas cliente:

	192.168.1.100:/etc/dat/compartida /home/salva1234567/carpetacliente/ nfs auto,noatime,nolock,bg,nfsvers=3,intr,tcp,actimeo=1800 0 0

Hemos apagado un cliente y vemos que funciona perfectamente.
