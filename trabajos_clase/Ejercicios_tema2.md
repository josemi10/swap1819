# EJERCICIOS TEMA 2 

**Ejercicio T2.1:**
 
**Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).**

As = Acn-1 + ( (1 – Acn-1) * Acn)

Web2=85% + ((1-85%)*85%)=97.75%
Web3=97.75% + ((1-97.75%)*85%)=99.6625%

Application2=90% + ((1-90%)*90%)=99%
Application3=99% + ((1-99%)*90%)=99.9%

DataBase2=99.9% + ((1-99.9%)*99.9%)=99.9999%
DataBase3=99.9999% + (1-99.9999%)*99.9%)=99.9999999%

DNS2=98% + ((1-98%)*98%)=99.96%
DNS3=99.96% + ((1-99.96%)*98%)=99.9992%

Firewall2=85% + ((1-85%)*85%)=97.75%
Firewall3=97.75% + ((1-97.75%)*85%)=99.6625%

Switch2=99% + ((1-99%)*99%)=99.99%
Switch3=99.99% + ((1-99.99%)*99%=99.9999%

DataCenter2=99.99% + ((1-99.99%)*99.99%)=99.999999%
DataCenter3=99.999999% + ((1-99.999999%)*99.99%)=99.9999999999%

ISP2=95% + ((1-95%)*95%)=99.75%
ISP3=99.75% + ((1-99.75%)*95%)=99.9875%

AS=99.6625%*99.9%*99.9999999%*99.9992%*99.6625%*99.9999%*99.9999999999%*99.9875%=99.2135165%

**Ejercicio T2.2:**
**Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.**

**Symfony** 
Framework PHP diseñado para optimizar el desarrollo de las aplicaciones web basado en el patrón Modelo Vista Controlador. 

**Django** 
Framework de desarrollo web de código abierto, escrito en Python, que respeta el paradigma conocido como Model Template View.


**Ejercicio T2.3:**
**¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor?**

**Cacti** 
Este sistema nos permite monitorizar y visualizar gráficas de toda la información de nuestro servidor y su red. Aprovecha RRDTool y esta basada en PHP y MySQL.


**Ejercicio T2.4:**
**Buscar ejemplos de balanceadores software y hardware (productos comerciales).** 

**Nginx**
Este servidor web puede actuar también como balanceador de carga para un pequeño cluster que actúe como servidor web.

**Pen**
Es un balanceador de carga para los protocolos basados ​​en TCP "simples" como HTTP o SMTP. Permite varios servidores que aparezcan como uno hacia el exterior.


