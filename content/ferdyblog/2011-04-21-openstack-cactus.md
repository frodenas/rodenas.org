---
title: OpenStack Cactus
author: ferdy
date: 2011-04-20T23:45:10+00:00
url: /ferdyblog/2011/04/21/openstack-cactus/
fb2011:
  - 04
fbcategories:
  - General
fbtags:
  - cactus
  - openstack

---
Despu&eacute;s de 10 semanas de desarrollo, la semana pasada se liberó la 3ra release pública de [OpenStack][1], llamada Cactus. La lista completa de novedades en esta versión la podeis consultar en su [wiki][2]. Aquí os dejo algunas destacadas:

  * En **Nova**: 
      * Soporte a dos nuevas tecnologias de virtualización: LXC (Linux Containers) y VMWare/vSphere ESX / ESXi 4.1, Update 1.
      * En el caso de utilizar KVM, ahora podremos mover máquinas virtuales de un servidor físico a otro sin necesidad de pararlas.
      * Soporte a IPv6 independientemente del modo de network que utilizemos.
      * Aunque en modo experimental, la nueva versión 1.1 de la API habilita mecanismos de extensión. Esto facilitará a los desarrolladores que añadan sus propias extensiones a la API de una forma fácil y sin _ensuciar_ el core de la API.
  * En **Swift**: 
      * Podemos servir contenido estatico directamente desde Swift. Además el servidor se comporta como un servidor web tradicional, buscando un archivo de index en primer lugar, devolviendo el listado de archivos existentes, y una página de error en caso de no encontrar un archivo (todo esto configurable).
      * Mejoras en el rendimiento al utilizar comunicación asincrona contra los backends.
      * Mejoras en la detección de errores al realizar una validación de checksum para cada acción de GET sobre un objeto. En caso de fallo, el sistema pone el objeto en quarentena e intenta replicarlo desde otro backend.
  * En **Glance**: 
      * Nueva interface por linea de comandos que nos permite interactuar con los servicios de Glance. El nuevo comando se llama _glance_ y admite las siguientes opciones:
  
        > Usage: glance <command> \[options\] \[args\]
        > 
        > Commands:
      
        > help <command> Output help for one of the commands below
      
        > add Adds a new image to Glance
      
        > update Updates an image&#8217;s metadata in Glance
      
        > delete Deletes an image from Glance
      
        > index Return brief information about images in Glance
      
        > details Return detailed information about images in Glance
      
        > show Show detailed information about an image in Glance
      
        > clear Removes all images and metadata from Glance 
    
      * Hasta ahora solo podíamos indicar el tipo de imagen (machine, kernel, ramdisk) y ahora se ha habilitado que podamos definir el formato (ami, ari, aki, vhd, vmdk, raw, qcow2, vdi) y el contenedor (ami, ari, aki, bare, ovf) de la imagen.

La semana que viene, aprovechando la [conferencia][3] de usuarios que se realizará en Santa Clara (con 400 usuarios registrados y 100 en lista de espera), se definirán las nuevas funcionalidades que van a incorporarse en las 2 próximas releases. Si habéis estado siguiendo regularmente la [lista de distribución][4], os habréis dado cuenta que la lista de temas a discutir es bastante amplia, señal inequívoca que esta tecnología suscita bastante interés y que va apartandose cada vez más del _vaporware_ del año pasado.

Yo por mi parte tengo previsto asistir a la conferencia. En la medida de lo posible iré actualizando este blog con lo más destacado que vaya pasando. Stay tuned!

 [1]: http://www.openstack.org/
 [2]: http://wiki.openstack.org/ReleaseNotes/Cactus
 [3]: http://www.openstack.org/blog/2011/03/openstack-conference-design-summit-2011-sponsored-by-citrix/
 [4]: https://lists.launchpad.net/openstack/

## Comments

### Comment by Carlos on 2011-06-29 04:49:55 +0000
Muchas gracias por compartir tu conocimiento acerca de Cloud Computing

Mi nombres es Carlos y soy de Peru 

Soy nuevo en este tema y por lo q estoy leyendo en tu Blog sabes bastante del tema.
  
No se si me puedes orientar en mi inicio acerca de este tema te lo agradecería mucho

Muchas Gracias

Existos