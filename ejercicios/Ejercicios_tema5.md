# EJERCICIOS TEMA 5

**Ejercicio 5.1**

**Buscar información sobre cómo calcular el número de conexiones por segundo.**

Podemos utilizar el comando netstat con la opción -an o -s o el módulo HttpStubStatusModule de nginx para ver las conexiones actuales.

En ambos casos, si queremos obtener las conexiones por segundo, dividimos las peticiones por las conexiones establecidas.

**Ejercicio 5.3**

**Buscar información sobre características, funcionalidad, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.**

La herramienta netstat proporciona información acerca de los aspectos relativos a la red. Otra herramienta que surge como alternativa a netstat es ss, que muestra la información de manera más clara para el usuario. Si buscamos una alternativa con interfaz gráfica tenemos, por ejemplo, TCPView para Windows.
