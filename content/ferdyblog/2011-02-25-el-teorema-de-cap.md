---
title: El teorema de CAP
author: ferdy
date: 2011-02-25T01:05:44+00:00
url: /ferdyblog/2011/02/25/el-teorema-de-cap/
fb2011:
  - 02
fbcategories:
  - General
fbtags:
  - CAP
  - consistencia
  - disponibilidad
  - escalabilidad
  - NoSQL
  - tolerancia

---
Los que sigais de cerca el mundillo de [NoSQL][1] seguramente habre&iacute;s escuchado, cuando se comentan las caracter&iacute;sticas de implementaci&oacute;n de estas bases de datos, que los desarrolladores han tenido que escoger entre garantizar consistencia o garantizar disponibilidad, siempre sacrificando una de ellas. Esta dicotom&iacute;a es debida al [teorema de CAP][2] <sup>[1]</sup>, que lanzado inicialmente como una conjetura <sup>[2]</sup> en el a&ntilde;o 2000 por [Eric Brewer][3] (motivo por el cual al teorema se le conoce formalmente como teorema de Brewer), y posteriormente probado formalmente en el 2002 <sup>[3]</sup>, establece que:

> Un sistema de datos compartidos pude asegurar como mucho dos de estas tres propiedades: Consistencia, Disponibilidad y Tolerancia a particiones. 

El problema con este teorema es que la definici&oacute;n es muy simple (y por tanto, f&aacute;cil de recordar), y ha provocado y sigue provocando muchas confusi&oacute;nes, entre otras cosas porque se cambia el significado real de las propiedades (por ejemplo, tolerancia a particiones a veces se aplica a particionar los datos funcionalmente en diferentes ubicaciones). As&iacute; pu&eacute;s, recordemos antes de nada el significado de estas tres propiedades seg&uacute;n la definici&oacute;n del teorema (y recordad que estamos hablando de sistemas distribuidos):

  * **Consistencia**: un conjunto de operaciones se deben ejecutar al mismo tiempo, o dicho de otra forma, un sistema es consistente si una modificaci&oacute;n se aplica a todos los nodos en el mismo tiempo l&oacute;gico y, por tanto, cuando se recupera la informaci&oacute;n, todos los nodos devuelven el mismo resultado. Es lo que se conoce como consistencia atomica o estricta (&#8220;_[Linearizability][4]_&#8221; en ingl&eacute;s) 
  * **Disponibilidad**: cualquier petici&oacute;n recibida en un nodo del sistema debe obtener una respuesta, aunque falle el resto de los nodos.
  * **Tolerancia a particiones**: una petici&oacute;n debe ser procesada por el sistema incluso si se pierden de forma arbitraria mensajes entre alguno o todos los nodos del sistema, es decir, si un nodo se separa de la red (porque pierde conectividad, &#8230;), el sistema seguir&aacute; disponible.

Por lo tanto, siguiendo el teorema, un sistema distribuido solamente podr&aacute; asegurarnos:

  * **CP**: el sistema ejecutar&aacute; las operaciones de forma consistente, aunque se pierda la comunicaci&oacute;n entre nodos (partici&oacute;n del sistema), pero no se asegura que el sistema responda (disponibilidad).
  * **AP**: el sistema siempre responder&aacute; a las peticiones, aunque se pierda la comunicaci&oacute;n entre nodos (partici&oacute;n del sistema). Los datos procesados pueden no ser consistentes.
  * **CA**: el sistema siempre responder&aacute; a las peticiones y los datos procesados ser&aacute;n consistentes. En este caso no se permite una perdida de comunicaci&oacute;n entre nodos (partici&oacute;n del sistema).

<img src="/ferdyblog/images/2011/02/Teorema-CAP-300x257.png" alt="" title="Teorema CAP" width="300" height="257" class="aligncenter size-medium wp-image-68" srcset="/ferdyblog/images/2011/02/Teorema-CAP-300x257.png 300w, /ferdyblog/images/2011/02/Teorema-CAP.png 320w" sizes="(max-width: 300px) 100vw, 300px" />

Vamos a poner un ejemplo pr&aacute;ctico para que se entienda mejor. Imaginemonos que tenemos un sistema de datos que mantiene la informaci&oacute;n almacenada en 3 nodos {A, B, C}, y en un momento concreto un cliente lanza una petici&oacute;n de escritura, pero debido a un fallo de red se pierda la comunicaci&oacute;n entre algunos nodos, y por tanto el sistema se particiona en 2, por ejemplo {A, B} y {C}:

  * En un sistema **CP**, para garantizar la consistencia debemos asegurarnos que la operaci&oacute;n se realiza en los 3 nodos al mismo tiempo. Como el sistema se ha particionado (y sigue vivo ya que toleramos las particiones), si la petici&oacute;n se procesa por el nodo {C} ser&aacute; imposible replicarla en los nodos {A, B}. Ante esta situaci&oacute;n, el nodo {C} deber&aacute; rechazar la escritura hasta que se deshaga la partición (ya que sino no podr&iacute;a garantizar consistencia), lo que da lugar a indisponibilidad.
  * En un sistema **AP**, nos importa m&aacute;s la disponibilidad, por lo que aunque haya una partici&oacute;n del sistema, la petici&oacute;n se procesar&aacute; igualmente. En este caso, el sistema no nos puede garantizar la consistencia, ya que no sabe si la informaci&oacute;n procesada por un nodo (por ejemplo, {C}) ha sido replicada al resto de nodos ({A, B}).
  * En el caso de un sistema **CA**, el tema se complica un poco m&aacute;s. Si el sistema no esta particionado, cualquier operaci&oacute;n se procesar&aacute; y replicar&aacute; al resto de nodos. Ahora bien, si el sistema se particiona, entonces el sistema deber&iacute;a fallar, ya que no podremos garantizar la consistencia de la operaci&oacute;n, y si falla, entonces no podemos garantizar disponibilidad, por lo que estar&iacute;amos delante del mismo caso que un sistema **CP**. Resumiendo, que este tipo de sistema es bastante improbable, ya que para que funcione es necesario que la comunicaci&oacute;n entre nodos siempre est&eacute; en perfecto estado (improbable), o en su defecto, tolerar las particiones como en un sistema CP.

A partir de este ejemplo, podemos ver la raz&oacute;n por la que las implementaciones de bases de datos distribuidas (tanto las tradicionales como las NoSQL) se vean obligadas a escoger entre consistencia (CP) o disponibilidad (AP), pero jamas podr&aacute;n escoger las dos (CA), a no ser claro est&aacute; que solo haya un nodo o que todos los nodos residan en la misma caja f&iacute;sica (pero entonces no serian distribuidas). Me reservo otra entrada para explicar que tipo de soluci&oacute;n implementan los distintos servidores distribuidos que hay en el mercado y, oh, sorpresa, algunas incluso logran garantizar las 3. ¿Sabeis c&oacute;mo?

[1] La palabra CAP viene determinada por las iniciales de las 3 propiedades (en ingl&eacute;s): **C**onsistency, **A**vailability, **P**artition tolerance.

[2] La presentaci&oacute;n original de E. Brewer: [&#8220;Towards Robust Distributed Systems&#8221;][5] (PDF).

[3] La prueba formal del teorema: [“Brewer&#8217;s conjecture and the feasibility of consistent, available, partition-tolerant web services”][6] (PDF).

 [1]: http://es.wikipedia.org/wiki/NoSQL
 [2]: http://es.wikipedia.org/wiki/Teorema_CAP
 [3]: http://es.wikipedia.org/wiki/Eric_Brewer_(cient%C3%ADfico)
 [4]: http://en.wikipedia.org/wiki/Linearizability
 [5]: http://www.cs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf
 [6]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.20.1495&rep=rep1&type=pdf

## Comments

### Comment by CM on 2011-08-26 03:06:43 +0000
¿Cómo se garantizan las 3? De verdad existe la forma de hacerlo?

### Comment by ferdy on 2011-09-22 23:01:40 +0000
CM, según el teorema, no se pueden garantizar las 3. Para lidiar con este problema se suele recurrir a la <a href="http://en.wikipedia.org/wiki/Eventual_consistency" rel="nofollow">Eventual Consistency</a>. En cuanto tenga tiempo, escribiré una entrada sobre esto.

### Comment by PaEs on 2012-12-24 03:57:09 +0000
Hola Amigo! podrías darme un ejemplo más claro de un sistema CP?
  
Mi duda es que si el sistema es Tolerante a Particiones, como puede ser al mismo tiempo consistente??. Si es tolerante a particiones entonces no se garantiza que los datos sean replicados a todos los nodos (porque la comunicación puede fallar), por lo tanto no hay consistencia. 

En el ejemplo de sistema CP ponés:

&#8220;Ante esta situación, el nodo {C} deberá rechazar la escritura hasta que se deshaga la partición (ya que sino no podría garantizar consistencia)&#8221; 

Da a entender que para que el sistema sea consistente no debe haber particiones.. por lo tanto un sistema CP es improbable.

### Comment by Sergio on 2016-01-14 15:26:50 +0000
Es consistente, porque no deja realizar la escritura o lectura&#8230;
  
Lo que no tiene es disponibilidad, hasta que se termine el particionamiento.

### Comment by Sergio Gabriel on 2017-07-02 01:36:20 +0000
El caso de CA sucede en los RDBMS tradicionales (Consistency, Availability), pero en el caso de una arquitectura de replicación el RDBMS no podría más que garantizar la consistencia eventual. Sería interesante hacer un análisis de qué propiedad se va cumpliendo en los diferentes escenarios, alta disponibilidad con replicación síncrona, asíncrona, maestro-esclavo y multi maestro.
  
Muy buen artículo!
  
Saludos.
  
Sergio Gabriel
  
Corrientes &#8211; Argentina