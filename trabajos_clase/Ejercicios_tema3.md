#EJERCICIOS TEMA 3.

**Ejercicio T3.1:**
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

Como órdenes de terminal en linux se usa route, la sintaxis del que es: route operación [tipo] destino enrutador saltos Por ejemplo: route add -net 165.255.0.0/16 gw 192.168.1.1 dev eth0

En Windows Server hay la herramienta "Enrutamiento y servicio remoto"

**Ejercicio T3.2:**
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

En Linux se utiliza la herramienta **iptables**. Podemos controlar tanto los paquetes originados en nuestra máquina OUTPUT, los que nos llegan INPUT y los que pasan por ella para ser encaminados a otro sitio FORWARD.

Para Windows existe la utilidad **netsh** a la que se puede acceder mediante el comando netsh.
