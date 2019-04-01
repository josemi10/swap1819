## JOSE MIGUEL PELEGRINA PELEGRINA
## COMPAÑERO: JUAN SALVADOR MOLINA MARTÍN

# PRACTICA 4: ASEGURAR LA GRANJA WEB

## Objetivo de la práctica

**El objetivo de esta práctica es llevar a cabo la configuración de seguridad de la granja web. Para ello, llevaremos a cabo las siguientes tareas:**

	Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
	Configurar las reglas del cortafuegos para proteger la granja web.

**1.Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.**

Para generar un **certificado SSL** autofirmado en Ubuntu Server solo debemos activar el módulo **SSL** de **Apache**, generar los certificados y especificarle la ruta a los certificados en la configuración. Así pues, como root ejecutaremos:


	a2enmod ssl

	service apache2 restart

	mkdir /etc/apache2/ssl

	sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

![imagen]()

Editamos el archivo de configuración del sitio default-ssl:

	sudo nano /etc/apache2/sites-available/default-ssl.conf

![imagen]()

Activamos el sitio default-ssl y reiniciamos apache:

	a2ensite default-ssl

	service apache2 reload

Tenemos que copiar los archivos **apache.crt** y **apache.key** a la otra máquina-2 y al balanceador.Para ello usaremos rsync.

**Máquina-2:**

![imagen]()

**Máquina-balanceador:**

![imagen]()

Activamos el sitio default-ssl en la segunda máquina virtual y reiniciamos apache:

	a2ensite default-ssl

	service apache2 reload

![imagen]()

Después, en el balanceador **nginx** debemos añadir lo siguiente al archivo /etc/nginx/conf.d/default.conf:
	
	listen 443 ssl;
	ssl on;
	ssl_certificate		/tmp/apache.crt;
	ssl_certificate_key	/tmp/apache.key;
	
Y lo reiniciamos:

	systemctl restart nginx

Y ahora hacemos la petición

	curl -k https://192.168.1.102/hola.html

![imagen]()

**2.Configurar las reglas del cortafuegos para proteger la granja web.**

Creamos el script para asegurar el acceso .Nos lo creamos en la máquina-1

![imagen]()
