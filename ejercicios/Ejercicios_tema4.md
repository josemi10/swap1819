# EJERCICIOS TEMA 4

**Ejercicio 4.2**

**Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otro**

	Precio	Rendimiento	Puertos Eth	Conex. simultaneas capa4	Hot-swap?

LM-X3	4.000$	  3.4Gbps	     8		        8,600,000		   N/A

LM-3400	7.000$	  3.4Gbps	     8		        8,600,000		   N/A
 
LM-X15	9.800$	   15Gbps	     16		        35,000,000		    SÍ
	
LM-8000	30.000$	   20Gbps	     0		        75,800,000		    SÍ

LM-8020	40.000$	   30Gbps	     0		        75,800,000		    SÍ

**Ejercicio 4.4**

**Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2 (o el software que hemos propuesto para la práctica 3).**

Tanto los balanceadores BIG IP de F5, los FortiADC de Fortinet, los de Cisco, los de KEMP Technologies y los ADC de Barracuda utilizan por defecto el método round-robin. Algunos también proporcionan algoritmos alternativos como least connections, que selecciona el servidor con menos conexiones activas.

**Ejercicio 4.5**

**Probar las diferentes maneras de redirección HTTP.**
**¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?**

Para indicar redireccionamiento, se pueden usar varios códigos de estado HTTP: 301, 302, 303, 307 y 308.

Los dos primeros corresponden la la versión 1.0 de HTTP en adelante. El primero indica que la redirección es permanente y se puede guardar en caché. El segundo, que la redirección es temporal y no se puede guardar en caché por defecto. Esta es la recomendada si queremos tener varios servidores o páginas para mostrar en función de la localización del cliente, ya que la web principal no se vería afectada. Además ofrece mayor compatibilidad que 303 y 307.
Los otros tres corresponden a la versión 1.1 de HTTP. Tanto 303 como 307 indican que la redirección es temporal. La diferencia entre ambos es que 303 nunca se puede guardar en caché, mientras que 307 no se guarda por defecto.
Por último, 308 se utiliza para indicar redirecciones permanentes y se guarda en caché por defecto.

**Ejercicio 4.7**

**Buscar información sobre métodos y herramientas para implementar GSLB.**

Cuando un usuario acceda a nuestro sitio, se le redireccionará al que le ofrezca mejores prestaciones, ya sea por proximidad (localización), por menor carga o latencia, DNS (round-robin), etc...
