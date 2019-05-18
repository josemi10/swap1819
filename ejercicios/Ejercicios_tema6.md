# EJERCICIOS TEMA 6

**Ejercicio 6.1**

**Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento. Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.**

Para bloquear todo el tráfico, introducimos las siguientes reglas:
iptables -F
iptables -X
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

Para aceptar todo el tráfico, cambiamos las tres últimas reglas anteriores por las siguientes:
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

Cuando bloqueamos el tráfico, perdemos el acceso a la máquina virtual. Si borramos las reglas y/o aceptamos el tráfico, volvemos a tener acceso.

**Ejercicio 6.3**

**Buscar información acerca de los tipos de ataques más comunes en servidores web (p.ej. secuestros de sesión). Detallar en qué consisten, y cómo se pueden evitar.**

Los ataques más comunes son la inyección SQL, la denegación distribuida de servicio (DDoS), la fuerza bruta y el cross-site scripting (XSS).

La inyeccion SQL consiste en inyectar código malicioso en las consultas SQL para lograr el acceso a la datos protegidos de la base de datos del sitio. Es probablemente el ataque más sencillo de realizar, dado que solo se necesita una máquina y unos pocos conocimientos de SQL.
La denegación distribuida de servicio (DDoS) hace referencia al envío masivo de solicitudes al sitio web, haciendo que el servidor se bloquee y no pueda atender a todas ellas, provocando la falta de disponibilidad del sitio para los usuarios que realmente quieran entrar en la web. Cuando el ataque se realiza desde distintas máquinas distribuidas geográficamente, hablamos de denegación distribuida, mientras que cuando solo se emplea una máquina, hablamos de denegación simple.
Los ataques por fuerza bruta consisten básicamente en usar una máquina para obtener contraseñas usando la fuerza bruta para probar un gran número de combinaciones.
El cross-site scripting (XSS) consiste en camuflar código malicioso en sitios aparentemente inofensivos donde se ejecuta sin que el usuario sea consciente de ello.
