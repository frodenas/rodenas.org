---
title: 'CF-Console: Consola Web para Cloud Foundry'
author: ferdy
date: 2011-10-23T23:03:55+00:00
url: /ferdyblog/2011/10/24/cf-console-consola-web-para-cloud-foundry/
fb2011:
  - 10
fbcategories:
  - General
fbtags:
  - CF-Console
  - CloudFoundry
  - PaaS
  - Web UI

---
Cada verano, al disponer de más tiempo libre, suelo aprovechar para aprender un lenguaje de programación nuevo. Es una manera de pasar el tiempo (si, podéis llamarme _friki_), reciclarme en nuevas tecnologias, y refrescar mis oxidadas habilidades de programación (desafortunadamente llevo más de 10 años sin programar profesionalmente). Ese año me decidi a probar [Ruby][1], apoyándome, como no, en el tan conocido [Rails][2]. Decidí también que para que fuese realmente provechoso, en vez de realizar solo los ejercicios de un libro, debería crear una aplicación con una utilidad real, completamente funcional, y a ser posible, que no hubiese ninguna igual en el mercado. Así pués, y como he estado trasteando últimamente con [Cloud Foundry][3], me decidi a crear una consola web para este servicio.

Después de divertirme estos 3 últimos meses, ya tengo la aplicación plenamente funcional. Y para que el esfuerzo no quede en vano, he decidido publicar en [github][4] el [código fuente][5] de la aplicación (sed benévolos con el código, que es mi primera aplicación en <acronym title="Ruby on Rails">RoR</acronym>). De esta manera, podréis trastear con ella, mejorarla o añadir alguna funcionalidad nueva (más de una ya la tengo en mente para próximas versiones).

Aún así, si no tenéis tiempo, ganas o conocimientos, he habilitado una demo funcional de la aplicación en el servidor público de Cloud Foundry para que no tengáis excusa para no probarla :). La dirección és <http://cf-console.cloudfoundry.com/>.

Os adjunto a continuación algunos pantallazos de esta aplicación.

En el dashboard podréis ver tanto un resumen general de nuestra cuenta (aplicaciones, memoria y servicios usados y disponibles), así como un resumen del estado de nuestras aplicaciones e instancias:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-1024x666.png" alt="" title="Cloud Foundry - Dashboard" width="640" height="416" class="aligncenter size-large wp-image-471" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-1024x666.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-300x195.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard.png 1128w" sizes="(max-width: 640px) 100vw, 640px" />][6]
  
[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-2-1024x706.png" alt="" title="Cloud Foundry - Dashboard 2" width="640" height="441" class="aligncenter size-large wp-image-482" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-2-1024x706.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-2-300x206.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-2.png 1150w" sizes="(max-width: 640px) 100vw, 640px" />][7]

En el menu de aplicaciones podréis ver un resumen de todas las aplicaciones desplegadas en el servidor de Cloud Foundry, teniendo la posibilidad además de arrancarlas, pararlas y eliminarlas mediante un simple _click_:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Applications-1024x622.png" alt="" title="Cloud Foundry - Applications" width="640" height="388" class="aligncenter size-large wp-image-470" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Applications-1024x622.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Applications-300x182.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Applications.png 1118w" sizes="(max-width: 640px) 100vw, 640px" />][8]

Y para cada una de las aplicaciones, podréis ver los recursos asignados (pudiendo modificar tanto el número de instancias como la memoria asignada a cada instancia):

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Resources-1024x732.png" alt="" title="Cloud Foundry - Application Resources" width="640" height="457" class="aligncenter size-large wp-image-469" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Resources-1024x732.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Resources-300x214.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Resources.png 1117w" sizes="(max-width: 640px) 100vw, 640px" />][9]

Ver el estado de cada una de las instancias de nuestra aplicación:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Instances-1024x609.png" alt="" title="Cloud Foundry - Application Instances" width="640" height="380" class="aligncenter size-large wp-image-467" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Instances-1024x609.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Instances-300x178.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Instances.png 1130w" sizes="(max-width: 640px) 100vw, 640px" />][10]

Así como ver los logs de cada instancia (con posibilidad de filtrar la salida en base a un patrón de búsqueda):

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Application-logfile-1024x604.png" alt="" title="Cloud Foundry - Application logfile" width="640" height="377" class="aligncenter size-large wp-image-468" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Application-logfile-1024x604.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-logfile-300x177.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-logfile.png 1125w" sizes="(max-width: 640px) 100vw, 640px" />][11]

Adicionalmente, podréis consultar también los ficheros que se han desplegado en el servidor (en el caso de ficheros con código y sólo para determinados lenguajes, se mostrará el código coloreado según la sintaxi del lenguaje del fichero):

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Files-1024x804.png" alt="" title="Cloud Foundry - Application Files" width="640" height="502" class="aligncenter size-large wp-image-466" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Application-Files-1024x804.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Files-300x235.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Application-Files.png 1130w" sizes="(max-width: 640px) 100vw, 640px" />][12]

También podréis gestionar vuestros servicios, es decir, las instancias de los servicios del sistema que vamos a utilizar en nuestras aplicaciones:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Services-1024x599.png" alt="" title="Cloud Foundry - Services" width="640" height="374" class="aligncenter size-large wp-image-474" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Services-1024x599.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Services-300x175.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Services.png 1115w" sizes="(max-width: 640px) 100vw, 640px" />][13]

En el menu de sistema podréis consultar tanto los servicios del sistema, como los frameworks y runtimes disponibles en el servidor de Cloud Foundry:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-System-Services-1024x584.png" alt="" title="Cloud Foundry - System Services" width="640" height="365" class="alignright size-large wp-image-475" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-System-Services-1024x584.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-System-Services-300x171.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-System-Services.png 1134w" sizes="(max-width: 640px) 100vw, 640px" />][14]
  
[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Runtimes-1024x640.png" alt="" title="Cloud Foundry - Runtimes" width="640" height="400" class="aligncenter size-large wp-image-473" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Runtimes-1024x640.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Runtimes-300x187.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Runtimes.png 1163w" sizes="(max-width: 640px) 100vw, 640px" />][15]
  
[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Frameworks-1024x813.png" alt="" title="Cloud Foundry - Frameworks" width="640" height="508" class="aligncenter size-large wp-image-472" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Frameworks-1024x813.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Frameworks-300x238.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Frameworks.png 1159w" sizes="(max-width: 640px) 100vw, 640px" />][16]

Si además sois administradores del servidor de Cloud Foundry, podréis gestionar los usuarios:

[<img src="/ferdyblog/images/2011/10/Cloud-Foundry-Users-1024x530.png" alt="" title="Cloud Foundry - Users" width="640" height="331" class="aligncenter size-large wp-image-476" srcset="/ferdyblog/images/2011/10/Cloud-Foundry-Users-1024x530.png 1024w, /ferdyblog/images/2011/10/Cloud-Foundry-Users-300x155.png 300w, /ferdyblog/images/2011/10/Cloud-Foundry-Users.png 1162w" sizes="(max-width: 640px) 100vw, 640px" />][17]

¡Espero que os sea útil! Y ya sabeis, la aplicación es _open source_, por lo que podeis modificarla a vuestro gusto.

 [1]: http://www.ruby-lang.org/es/
 [2]: http://www.rubyonrails.org.es/
 [3]: http://cloudfoundry.org/
 [4]: https://github.com/
 [5]: https://github.com/frodenas/cf-console
 [6]: /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard.png
 [7]: /ferdyblog/images/2011/10/Cloud-Foundry-Dashboard-2.png
 [8]: /ferdyblog/images/2011/10/Cloud-Foundry-Applications.png
 [9]: /ferdyblog/images/2011/10/Cloud-Foundry-Application-Resources.png
 [10]: /ferdyblog/images/2011/10/Cloud-Foundry-Application-Instances.png
 [11]: /ferdyblog/images/2011/10/Cloud-Foundry-Application-logfile.png
 [12]: /ferdyblog/images/2011/10/Cloud-Foundry-Application-Files.png
 [13]: /ferdyblog/images/2011/10/Cloud-Foundry-Services.png
 [14]: /ferdyblog/images/2011/10/Cloud-Foundry-System-Services.png
 [15]: /ferdyblog/images/2011/10/Cloud-Foundry-Runtimes.png
 [16]: /ferdyblog/images/2011/10/Cloud-Foundry-Frameworks.png
 [17]: /ferdyblog/images/2011/10/Cloud-Foundry-Users.png

## Comments

### Comment by Nick Palomino on 2012-05-02 03:18:05 +0000
Bastante interesante y totalmente util tu aplicacion&#8230; Aun estoy esperando mi invitacion para CloudFoundry.

Quisiera saber todo lo que utilizaste aparte de RoR, para desarrollar esa aplicacion &#8220;cf-console&#8221;&#8230;

Gracias y saludos desde Perú!!

### Comment by Nick Palomino on 2013-03-21 07:45:00 +0000
La primera vez que lei su blog me quede fascinado por sus posts&#8230; Este post me motivo a aprender RoR y tambien desarrollar algo util y no solo el simple blog de ejemplo. Por muchos meses habia perdido el contacto con su blog, pero luego de revisar a quienes sigo en Twitter pude encontrarlo nuevamente&#8230; Gracias por sus post y compartir su experiencia.