---
title: Acerca de
author: ferdy
type: fbpage
date: 2011-02-19T13:35:53+00:00
url: /ferdyblog/acerca-de/

---
<img src="/ferdyblog/images/2011/02/Ferran-150x150.jpg" alt="" title="Ferran Rodenas" width="150" height="150" class="alignleft size-thumbnail wp-image-174" />Soy Ferran Rodenas (o &#8220;Ferdy&#8221; para aquellos amigos que hablan catalan en la intimidad), artesano del software y apasionado de la tecnolog&iacute;a, Internet y los medios de comunicación sociales. Desde hace m&aacute;s de 15 a&ntilde;os me dedico profesionalmente a lo que se suele denominar &#8220;inform&aacute;tica&#8221;, primero en el mundillo de las herramientas de ayuda al desarrollo de software, y &uacute;ltimamente en todo lo relacionado con las infraestructuras IT.

Me encanta aprender y jugar con las nuevas tecnologías, siempre en busca de nuevas ideas. Por eso, este diario no es m&aacute;s que un recopilatorio de ideas, reflexiones y tecnolog&iacute;as que voy descubriendo dia a dia. Espero no aburriros demasiado.

## Comments

### Comment by oscar on 2012-01-04 23:28:41 +0000
He leido tu blog y me ha gustado mucho tu viaje al SV.
  
He leido que eres entusiasta de OpenStack. En nuestra empresa queremos implementer Openstack pero necesitamos un cloudportal para hacer auto-aprovisionamiento para los clientes. El cloudportal de citrix esta muy bien pero para un SMB no es barato.

Qué soluciones conoces que no sean carísimas?

Un abrazo

### Comment by ferdy on 2012-01-04 23:42:00 +0000
Oscar, se me ocurren 2 soluciones, y las 2 open-source 🙂 :

  * <a href="http://wiki.openstack.org/OpenStackDashboard" rel="nofollow">Horizon</a>: portal desarrollado bajo el paraguas de OpenStack. La aplicación es un ejemplo (muy funcional) y os puede servir de base si la quereis modificar.
  * <a href="http://drupal.org/project/cloud" rel="nofollow">Clanavi</a>: es un portal basado en Drupal que permite gestionar tanto OpenStack como AWS o XCP.

Saludos.

### Comment by oscar on 2012-01-05 13:31:55 +0000
Hola Ferdy, gracias por tu contestación.
  
Había visto Horizon. Por lo que he visto no ofrece todavía, las posiblidades tremendas de un portal web para automatizar el aprovisionamiento y self-service de clientes, billing, etc. No sé si la intención de Horizon es ir en esa linea. A día de hoy, openstack no tiene este tipo de solución.
  
Sobre Clanavi, he visto los videos, pero no tienen una demo o snapshots de la parte de self-service para clientes. ¿lo has probado? 

¿Has probado alguna solución propietaria del self-service? La que he probado de Citrix es impresionante. También estoy haciendo pruebas con Rightscale, Eucalyptus, Open Nebula, abiquo, &#8230; Pero lleva bastante tiempo probar todas estas empresas y soluciones.

### Comment by ferdy on 2012-01-06 23:00:50 +0000
Oscar, la unica que he probado, y hace ya un tiempo, ha sido Horizon, y hasta donde yo sé, se va a quedar como una aplicación de ejemplo.

Saludos.