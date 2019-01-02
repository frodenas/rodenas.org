---
title: Experimentando con Ubuntu juju y Cloud Foundry
author: ferdy
date: 2011-09-22T21:39:54+00:00
excerpt: juju es un framework de orquestación para el despliegue de servicios de infraestructura en la “nube” (similar en cuanto a concepto a Chef o Puppet o, en otro nivel, a los ServerTemplates de RightScale), o dicho de otra manera, una especie de APT pero dirigido a entornos que se ejecutan en la “nube” y, a diferencia del primero, en vez de focalizarse en el despliegue de un producto en una máquina, persigue la instalación orquestada en entornos distribuidos de servicios interrelacionados. La idea detrás de juju es que haya una comunidad de desarrolladores que paquetizen el despliegue de sus servicios (similar a lo que hace APT con los paquetes o a las recipes de Chef) mediante lo que llaman charms (hechizos). En esta entrada vamos a experimentar con juju para montar un servicio de Cloud Foundry de una manera muy sencilla y rápida.
url: /ferdyblog/2011/09/22/experimentando-con-ubuntu-juju-y-cloud-foundry/
fb2011:
  - 09
fbcategories:
  - General
fbtags:
  - Amazon
  - cloud
  - CloudFoundry
  - EC2
  - guia
  - instalacion
  - juju
  - PaaS
  - Ubuntu
  - VMWare

---
Después de las vacaciones de verano, volvemos con la energia renovada y con ganas de hacer más experimentos 🙂 

En una [entrada anterior][1] donde os hablabla de [Cloud Foundry][2], un lector me pedia un post sobre como montar un servidor propio. La verdad es que comencé a escribirlo, aunque por motivos que no vienen a cuento tardé más de la cuenta. Y casi justo cuando lo tenia terminado, [VMWare][3] lanzó un [script][4] que simplifica mucho el proceso de instalación, por lo que borré el post por careced de sentido. Así pués, si todavia estais interesados, solamente tenéis que seguir las instrucciones que aparecen en la [página del proyecto][5] en github. El proceso, aunque largo, es muy sencillo.

En esta entrada, en cambio, nos vamos a centrar en ver como os podeis montar vuestro propio servidor de Cloud Foundry, pero en vez de en local, lo vamos a albergar en [Amazon EC2][6]. Además, en vez de hacerlo de la forma tradicional (o sea, creando una instancia de EC2 y ejecutando el script de instalación tal como se describe en [esta página][7]), vamos a utilizar una nueva herramienta muy interesante que ha aparecido recientemente, y que nos permitirá además escalar los servicios ofrecidos por Cloud Foundry de una manera muy sencilla y rápida.

[<img src="/ferdyblog/images/2011/09/juju.png" alt="" title="Ubuntu juju" width="543" height="100" class="aligncenter size-full wp-image-432" srcset="/ferdyblog/images/2011/09/juju.png 543w, /ferdyblog/images/2011/09/juju-300x55.png 300w" sizes="(max-width: 543px) 100vw, 543px" />][8]

La herramienta en cuestión se llama Ubuntu Ensemble. Bien, de hecho ya no se llama así 🙁 . Justo cuando estoy escribiendo esta entrada, lo magnificos chicos de [Canonical][9] han decidido cambiarle el nombre por [Ubuntu juju][10] (esta entrada debe estar &#8220;gafada&#8221; 🙂 ) en referencia a la [magia/brujería][11] practicada en algunas regiones de Africa.

[<img src="/ferdyblog/images/2011/09/charms-150x150.png" alt="" title="Ubuntu juju charms" width="150" height="150" class="alignright size-thumbnail wp-image-430" />][12]

_juju_ es un framework de orquestación para el despliegue de servicios de infraestructura en la &#8220;nube&#8221; (similar en cuanto a concepto a [Chef][13] o [Puppet][14] o, en otro nivel, a los [ServerTemplates de RightScale][15]), o dicho de otra manera, una especie de [APT][16] pero dirigido a entornos que se ejecutan en la &#8220;nube&#8221; y, a diferencia del primero, en vez de focalizarse en el despliegue de un producto en una máquina, persigue la instalación orquestada en entornos distribuidos de servicios interrelacionados. La idea detrás de _juju_ es que haya una comunidad de desarrolladores que paquetizen el despliegue de sus servicios (similar a lo que hace APT con los paquetes o a las [recipes][17] de Chef) mediante lo que llaman _charms_ (hechizos) y que estas _charms_, además de ser reutilizables por otros usuarios, incluyan los metadatos del servicio, las dependencias a otros servicios, los paquetes necesarios para su despliegue, así como la lógica para gestionar el servicio. Actualmente esta en fase de desarrollo, y solo admite entornos Amazon EC2 (o clones en cuanto a la API, como [OpenStack][18]), aunque está previsto soporte a otros entornos en un futuro. Se incluirá por defecto en la release 11.10 de Ubuntu, aunque a dia de hoy, ya se puede probar tanto en la Beta 1 de la release 11.10 como en versiones anteriores (11.04 y 10.04).

Bien, una vez hechas las presentaciones, vamos a experimentar con esta herramienta. En primer lugar vamos a instalar _juju_. Si estamos utilizando Ubuntu 11.10 es tan sencillo como:
  
```
~$ sudo apt-get install juju
```

Pero si utilizamos Ubuntu 10.04 o 11.04, entonces tendremos que añadir primero el repositorio <acronym title="Personal Package Archives">PPA</acronym> correspondiente:
  
```
~$ sudo apt-get install python-software-properties
~$ sudo add-apt-repository ppa:juju/pkgs
~$ sudo apt-get update
~$ sudo apt-get install juju
```

Ahora vamos a inicializar el entorno de _juju_. Primero invocaremos al comando que nos creará un archivo de entorno por defecto:
  
```
~$ juju
error: No environments configured. Please edit: /home/frodenas/.juju/environments.yaml
```

Y editaremos el archivo añadiendo algunas líneas:
  
```
~$ vi /home/frodenas/.juju/environments.yaml
environments:
  sample:
    type: ec2
    ec2-uri: https://ec2.eu-west-1.amazonaws.com
    access-key: --- INSERTAR AQUI VUESTRA ACCESS-KEY DE AMAZON EC2 ---
    secret-key: --- INSERTAR AQUI VUESTRA SECRET-KEY DE AMAZON EC2 ---
    control-bucket: --- ELIMINADO POR SEGURIDAD - DEJAR EL VALOR POR DEFECTO ---
    admin-secret: --- ELIMINADO POR SEGURIDAD - DEJAR EL VALOR POR DEFECTO ---
    default-image-id: ami-66f6c512
    default-instance-type: m1.large
```

Lo que hemos añadido ha sido:

  * _ec2-uri_: aquí hemos puesto el endpoint de la región de Amazon EC2 que nos interesa, en este caso, la región EU West (Irlanda).
  * _access-key_ y _secret-key_: vuestras credenciales de Amazon EC2.
  * _default-image-id_: aquí ponemos el nombre de la AMI de Amazon EC2 que se utilizará por defecto, en este caso, utilizaremos una imagen de Ubuntu Cloud 11.10 de 64 bits disponible en la región de EU West. El nombre de la AMI varia cada dia, por lo que os recomiendo que comproveis la [lista actual de imagenes][19] antes de utilizar la que yo he puesto.
  * _default-instance-type_: aquí ponemos el [tipo de instancia][20] de Amazon EC2 que se utilizará por defecto, en este caso, como la instancia contendrá Cloud Foundry y diversos servicios (MySQL, MongoDB y Redis), escogemos la instancia grande (_m1.large_).

Bien, ahora hemos de arrancar el entorno. Pero antes, y debido a que las _charms_ de _juju_ que nos permiten instalar el servidor de Cloud Foundry y sus servicios todavia no están publicadas en los [repositorios oficiales][21], nos tocará instalarlas manualmente en local:
  
```
~$ sudo apt-get install bzr
~$ mkdir charms && cd charms
~/charms$ bzr branch lp:~canonical-sig/+junk/cloudfoundry-server
```

Ahora si podemos arrancar el entorno de _juju_ (generar antes un par de claves en vuestro sistema sino lo habéis hecho, de lo contrario el entorno no arrancará):
  
```
~/charms$ ssh-keygen -t rsa -b 2048
~/charms$ juju bootstrap
2011-09-22 00:46:54,161 INFO Bootstrapping environment 'sample' (type: ec2)...
2011-09-22 00:47:01,753 INFO 'bootstrap' command finished successfully
```

Esto proceso lo que hará es crear una instancia en Amazon EC2 e instalarle el servidor de _juju_ mediante [cloud-init][22]. Con el comando _status_ podremos ver si el entorno está ya arrancado:
  
```
~/charms$ juju status
No machines have addresses assigned yet
2011-09-22 00:47:11,893 ERROR No machines have addresses assigned yet
```

Vemos que la instancia todavía no está levantada. Nos vamos a la [consola web][23] de Amazon EC2 y esperamos a que arranque:

[<img src="/ferdyblog/images/2011/09/juju-init-1024x596.png" alt="" title="Juju en Amazon EC2 - Bootstrap" width="640" height="372" class="aligncenter size-large wp-image-439" srcset="/ferdyblog/images/2011/09/juju-init-1024x596.png 1024w, /ferdyblog/images/2011/09/juju-init-300x174.png 300w, /ferdyblog/images/2011/09/juju-init.png 1523w" sizes="(max-width: 640px) 100vw, 640px" />][24]

Una vez esté en marcha, volvemos a ejecutar el comando _status_:
  
```
~/charms$ juju status
2011-09-22 00:49:00,215 INFO Connecting to environment.
machines:
  0: {dns-name: ec2-46-51-151-139.eu-west-1.compute.amazonaws.com, instance-id: i-af00e1e6}
services: {}
2011-09-22 00:49:01,834 INFO 'status' command finished successfully
```

Como veis, ahora si nos indica que hay una máquina en marcha. Ahora vamos a desplegar el servidor de Cloud Foundry. Para ello utilizaremos el comando _deploy_ y la _charm_ que nos hemos descargado anteriormente:
  
```
~/charms$ juju deploy --repository . cloudfoundry-server
2011-09-22 00:49:25,033 INFO Connecting to environment.
2011-09-22 00:49:27,823 INFO Charm deployed as service: 'cloudfoundry-server'
2011-09-22 00:49:27,825 INFO 'deploy' command finished successfully
```

Igual que en el caso anterior, esperamos a que arranqué la instancia, se despliegue el servidor y servicios de Cloud Foundry, y estos se pongan en marcha (tened paciencia, es un proceso un poco lento). Podemos ir consultando periodicamente el estado hasta que el servicio está en marcha (el campo &#8220;_state_&#8221; pasará de &#8220;_null_&#8221; a &#8220;_installed_&#8221; y finalmente &#8220;_started_&#8220;):
  
```
~/charms$ juju status
2011-09-22 00:55:17,906 INFO Connecting to environment.
machines:
  0: {dns-name: ec2-46-51-151-139.eu-west-1.compute.amazonaws.com, instance-id: i-af00e1e6}
  1: {dns-name: ec2-46-137-3-58.eu-west-1.compute.amazonaws.com, instance-id: i-0503e24c}
services:
  cloudfoundry-server:
    charm: local:cloudfoundry-server-26
    relations: {}
    units:
      cloudfoundry-server/0:
        machine: 1
        relations: {}
        state: started
2011-09-22 00:55:20,236 INFO 'status' command finished successfully
```

El siguiente paso será abrir los puertos necesarios para que nos podamos conectar con el servidor de Cloud Foundry. Para ello utilizaremos el comando _expose_ (y no es necesario indicar los puertos a abrir, ya que estos están indicados en la _charm_):
  
```
~/charms$ juju expose cloudfoundry-server
2011-09-22 00:55:41,155 INFO Connecting to environment.
2011-09-22 00:55:42,485 INFO Service 'cloudfoundry-server' was exposed.
2011-09-22 00:55:42,486 INFO 'expose' command finished successfully
```

Consultamos el estado del servicio y veremos como ahora nos indica los puertos que están abiertos:
  
```
~/charms$ juju status
2011-09-22 00:55:45,701 INFO Connecting to environment.
machines:
  0: {dns-name: ec2-46-51-151-139.eu-west-1.compute.amazonaws.com, instance-id: i-af00e1e6}
  1: {dns-name: ec2-46-137-3-58.eu-west-1.compute.amazonaws.com, instance-id: i-0503e24c}
services:
  cloudfoundry-server:
    charm: local:cloudfoundry-server-26
    exposed: true
    relations: {}
    units:
      cloudfoundry-server/0:
        machine: 1
        open-ports: [80/tcp, 443/tcp, 4222/tcp]
        relations: {}
        state: started
2011-09-22 00:55:48,101 INFO 'status' command finished successfully
```

En teoria ahora está todo levantado, pero por si acaso, vamos a comprobarlo conectandonos a la máquina que contiene el servidor de Cloud Foundry. Para ello utilizaremos el comando _ssh_ del propio _juju_ y el número de máquina que nos ha indicado el comando _status_:
  
```
~/charms$ juju ssh 1
2011-09-22 00:56:14,640 INFO Connecting to environment.
2011-09-22 00:56:16,265 INFO Connecting to machine 1 at ec2-46-137-3-58.eu-west-1.compute.amazonaws.com
```

Una vez hayamos entrado, miraremos si los servicios de Cloud Foundry están levantados:
  
```
ubuntu@ip-10-228-250-63:~$ cd /opt/cloudfoundry-server/vcap/bin
ubuntu@ip-10-228-250-63:/opt/cloudfoundry-server/vcap/bin$ sudo ./vcap status
router              :    RUNNING
cloud_controller    :    RUNNING
dea                 :    RUNNING
health_manager      :    RUNNING
redis_gateway       :    RUNNING
redis_node          :    RUNNING
mysql_gateway       :    RUNNING
mysql_node          :    RUNNING
mongodb_gateway     :    RUNNING
mongodb_node        :    RUNNING
```

Como vemos, todos los servicios de Cloud Foundry están en marcha. Ya nos podemos desconectar de la instancia de Amazon EC2:
  
```
ubuntu@ip-10-228-250-63:/opt/cloudfoundry-server/vcap/bin$ exit
Connection to ec2-46-137-3-58.eu-west-1.compute.amazonaws.com closed.
```

Ahora vamos a proceder a conectarnos a Cloud Foundry para ver si responde. Lo primero que deberemos hacer es bajarnos el cliente vmc:
  
```
~/charms$ sudo apt-get install ruby-vmc
```

Pero para poder conectarnos remotamente necesitamos disponer de un registro [wildcard DNS][25] que redirija nuestras peticiones hacia el servidor de Cloud Foundry. En nuestro caso, como es solo un experimento _low cost_, vamos a utilizar un truco. Lo que vamos a hacer en crear un tunel ssh de manera que las peticiones al puerto 80 de nuestra máquina se redirijan al puerto 80 de la instancia de Amazon EC2 que contiene el servidor de Cloud Foundry (si en vuestra máquina ya estais utilizando el puerto 80, lo podeis cambiar a otro, por ejemplo, el 8080). Pero para poder montar el túnel contra la instancia de Amazon EC2, necesitamos tener la clave privada y que esta coincida con la clave pública almacenada en la instancia de Amazon EC2. Como en el archivo de entorno de _juju_ no hemos especificado ningún par de claves, este ha utilizado el par de claves de nuestro usuario (de ahí que os recordava anteriormente el generar un par de claves). Así pués, lo que haremos es indicar al ssh que utilize la clave privada de nuestro usuario:
  
```
~/charms$ cd ~/.ssh
~/.ssh$ sudo ssh -i id_rsa -L 80:46.137.3.58:80 ubuntu@46.137.3.58 -N
```

El problema de este metodo es que nos bloquea la sesión de terminal, por lo que nos tocará abrir una nueva sesión. Una vez la tengamos, procederemos a provar la conexión contra Cloud Foundry:
  
```
~$ vmc target api.vcap.me
Succesfully targeted to [http://api.vcap.me]</p>
<p>~$ vmc info</p>
<p>VMware's Cloud Application Platform
For support visit http://support.cloudfoundry.com</p>
<p>Target:   http://api.vcap.me (v0.999)
Client:   v0.3.10
```

Bien, parece que el servidor responde. Ahora vamos a crear un usuario:
  
```
~$ vmc register
Email: frodenas@gmail.com
Password: ********
Verify Password: ********
Creating New User: OK
Successfully logged into [http://api.vcap.me]</p>
<p>~$ vmc info</p>
<p>VMware's Cloud Application Platform
For support visit http://support.cloudfoundry.com</p>
<p>Target:   http://api.vcap.me (v0.999)
Client:   v0.3.10</p>
<p>User:     frodenas@gmail.com
Usage:    Memory   (0B of 2.0G total)
          Services (0 of 16 total)
          Apps     (0 of 20 total)
```

Perfecto! El servidor de Cloud Foundry ya está listo para ser usado!

Podríamos finalizar el experimento aquí, pero vamos a ir un poco más allá. En un teórico entorno de producción, seguramente nos quedaremos cortos con solo 1 instancia de Cloud Foundry y que esta incluya todos los servicios. Lo que haríamos es crear más instancias y albergar en cada una de ellas alguno de los servicios disponibles. Vamos a ver como lo podemos hacer con _juju_.

En primer lugar, nos descargamos los _charms_ que nos interesen. Aquí os pongo los _charms_ de los servicios de <acronym title="Droplet Execution Agent ">DEA</acronym> (el agente de Cloud Foundry que ejecutará nuestras aplicaciones), [MySQL][26], [MongoDB][27] y [Redis][28]:
  
```
~$ cd charms
~/charms$ bzr branch lp:~canonical-sig/+junk/cloudfoundry-server-dea
~/charms$ bzr branch lp:~canonical-sig/+junk/cf-mysql
~/charms$ bzr branch lp:~canonical-sig/+junk/cf-mongodb
~/charms$ bzr branch lp:~canonical-sig/+junk/cf-redis
```

Vamos a utilizar como ejemplo la instalación de un nuevo servidor de MongoDB. Utilizaremos igual que antes el comando _deploy_:
  
```
~/charms$ juju deploy --repository . cf-mongodb
2011-09-22 01:04:42,031 INFO Connecting to environment.
2011-09-22 01:04:45,147 INFO Charm deployed as service: 'cf-mongodb'
2011-09-22 01:04:45,149 INFO 'deploy' command finished successfully
```

Y esperaremos a que el servicio de MongoDB esté levantado (cuando aparezca &#8220;_state: started_&#8220;):
  
```
~/charms$ juju status
2011-09-22 01:11:07,813 INFO Connecting to environment.
machines:
  0: {dns-name: ec2-46-51-151-139.eu-west-1.compute.amazonaws.com, instance-id: i-af00e1e6}
  1: {dns-name: ec2-46-137-3-58.eu-west-1.compute.amazonaws.com, instance-id: i-0503e24c}
  2: {dns-name: ec2-79-125-44-111.eu-west-1.compute.amazonaws.com, instance-id: i-7b04e532}
services:
  cf-mongodb:
    charm: local:cf-mongodb-1
    relations: {mongodb-cluster: cf-mongodb}
    units:
      cf-mongodb/0:
        machine: 2
        relations:
          mongodb-cluster: {state: up}
        state: started
  cloudfoundry-server:
    charm: local:cloudfoundry-server-26
    exposed: true
    relations: {}
    units:
      cloudfoundry-server/0:
        machine: 1
        open-ports: [80/tcp, 443/tcp, 4222/tcp]
        relations: {}
        state: started
2011-09-22 01:11:11,105 INFO 'status' command finished successfully
```

Ahora lo que debemos hacer es informar al servidor de Cloud Foundry de que tiene una nueva instancia de MongoDB disponible para ser usada. Para realizar esta acción, simplemente debemos establecer una relación entre las 2 instancias mediante _juju_, y este, mediante las instrucciones contenidas en la _charm_, hará las modificaciones pertinentes en el archivo de configuración de Cloud Foundry. Así pués, vamos a ello:
  
```
~/charms$ ~/charms$ juju add-relation cloudfoundry-server cf-mongodb
2011-09-22 01:11:36,088 INFO Connecting to environment.
2011-09-22 01:11:37,997 INFO Added cf-server relation to all service units.
2011-09-22 01:11:37,997 INFO 'add_relation' command finished successfully
```

Consultamos ahora el estado y vemos que nos aparece la relación:
  
```
~/charms$ juju status
2011-09-22 01:11:51,639 INFO Connecting to environment.
machines:
  0: {dns-name: ec2-46-51-151-139.eu-west-1.compute.amazonaws.com, instance-id: i-af00e1e6}
  1: {dns-name: ec2-46-137-3-58.eu-west-1.compute.amazonaws.com, instance-id: i-0503e24c}
  2: {dns-name: ec2-79-125-44-111.eu-west-1.compute.amazonaws.com, instance-id: i-7b04e532}
services:
  cf-mongodb:
    charm: local:cf-mongodb-1
    relations: {cf-server: cloudfoundry-server, mongodb-cluster: cf-mongodb}
    units:
      cf-mongodb/0:
        machine: 2
        relations:
          cf-server: {state: up}
          mongodb-cluster: {state: up}
        state: started
  cloudfoundry-server:
    charm: local:cloudfoundry-server-26
    exposed: true
    relations: {cf-server: cf-mongodb}
    units:
      cloudfoundry-server/0:
        machine: 1
        open-ports: [80/tcp, 443/tcp, 4222/tcp]
        relations:
          cf-server: {state: up}
        state: started
2011-09-22 01:11:55,279 INFO 'status' command finished successfully
```

Vamos a comprobar si el servicio está levantado en Cloud Foundry mediante una conexión _ssh_ de _juju_:
  
```
~/charms$ juju ssh 2
2011-09-22 01:12:17,200 INFO Connecting to environment.
2011-09-22 01:12:18,813 INFO Connecting to machine 2 at ec2-79-125-44-111.eu-west-1.compute.amazonaws.com
ubuntu@ip-10-58-121-108:~$ cd /opt/cloudfoundry-server/vcap/bin
ubuntu@ip-10-58-121-108:/opt/cloudfoundry-server/vcap/bin$ sudo ./vcap status
router              :    STOPPED
cloud_controller    :    STOPPED
dea                 :    STOPPED
health_manager      :    STOPPED
redis_gateway       :    STOPPED
redis_node          :    STOPPED
mysql_gateway       :    STOPPED
mysql_node          :    STOPPED
mongodb_gateway     :    RUNNING
mongodb_node        :    RUNNING
ubuntu@ip-10-58-121-108:/opt/cloudfoundry-server/vcap/bin$ exit
Connection to ec2-79-125-44-111.eu-west-1.compute.amazonaws.com closed.
```

Vemos como en esta instancia solamente se está ejecutando el servicio de MongoDB. Si viésemos que necesitamos otra instancia adicional de MongoDB, en este caso no haría falta ejecutar los comandos anteriores. Simplemente utilizando el comando _add-unit_ nos crearía una nueva instancia que formaria parte de un cluster de MongoDb y con la relación con el servidor de Cloud Foundry creada por defecto:
  
```
~/charms$ juju add-unit cf-mongodb
```

Y hasta aquí llega el experimento. Un consejo antes de finalizar: si tenéis cualquier problema ejecutando alguno de los pasos anteriores y no sabeis que está pasando, podeis utilizar el comando _debug-log_ para ver el log del servidor de _juju_ e intentar determinar la causa del problema:
  
```
~/charms$ juju debug-log
2011-09-22 01:13:31,421 INFO Connecting to environment.
2011-09-22 01:13:32,588 INFO Enabling distributed debug log.
2011-09-22 01:13:32,696 INFO Tailing logs - Ctrl-C to stop.
```

Como último paso, como siempre, recordar que hay que finalizar el entorno. Utilizaremos para ello el comando _destroy-environment_:
  
```
~/charms$ juju destroy-environment
WARNING: this command will destroy the 'sample' environment (type: ec2).
This includes all machines, services, data, and other resources. Continue [y/N]yes
2011-09-22 01:14:02,900 INFO Destroying environment 'sample' (type: ec2)...
2011-09-22 01:14:04,644 INFO Waiting on 3 EC2 instances to transition to terminated state, this may take a while
2011-09-22 01:14:27,728 INFO 'destroy_environment' command finished successfully
```

Este comando debería eliminar también las instancias de Amazon EC2, pero por si acaso, no está de más que lo comproveis vosotros mismos en la [consola web][23] de Amazon EC2.

[<img src="/ferdyblog/images/2011/09/juju-terminated-1024x633.png" alt="" title="Juju en Amazon EC2 - Terminated" width="640" height="395" class="aligncenter size-large wp-image-440" srcset="/ferdyblog/images/2011/09/juju-terminated-1024x633.png 1024w, /ferdyblog/images/2011/09/juju-terminated-300x185.png 300w, /ferdyblog/images/2011/09/juju-terminated.png 1518w" sizes="(max-width: 640px) 100vw, 640px" />][29]

Bien, como hemos visto, esta herramienta promete bastante. Si bien está previsto que entre por defecto en la release 11.10 de Ubuntu del mes de Octubre de 2011, la versión liberada estará todavia un poco verde, por lo que no os la recomiendo para un entorno de producción. Mientras tanto, espero que disfrutéis experimentado con ella (probad alguna de las [charms oficiales][21] o [crearos][30] vosotros mismos alguna de prueba). Si alguien se anima, que deje sus impresiones en los comentarios de esta entrada.

 [1]: /ferdyblog/2011/04/22/cloud-foundry/
 [2]: http://cloudfoundry.org/
 [3]: http://www.vmware.com/
 [4]: https://github.com/cloudfoundry/vcap/blob/master/setup/install
 [5]: https://github.com/cloudfoundry/vcap/blob/master/README.md
 [6]: http://aws.amazon.com/ec2/
 [7]: http://www.cloudsoftcorp.com/blogs/first-steps-with-cloud-foundry-on-amazon-ec2
 [8]: /ferdyblog/images/2011/09/juju.png
 [9]: http://www.canonical.com/
 [10]: https://juju.ubuntu.com/
 [11]: http://es.wikipedia.org/wiki/Yuyu_(magia)
 [12]: /ferdyblog/images/2011/09/charms.png
 [13]: http://www.opscode.com/chef/
 [14]: http://puppetlabs.com/
 [15]: http://www.rightscale.com/products/advantages/cloud-ready-servertemplates.php
 [16]: http://es.wikipedia.org/wiki/Advanced_Packaging_Tool
 [17]: http://wiki.opscode.com/display/chef/Recipes
 [18]: http://www.openstack.org/
 [19]: http://cloud.ubuntu.com/ami/
 [20]: http://aws.amazon.com/es/ec2/instance-types/
 [21]: https://launchpad.net/charm
 [22]: https://help.ubuntu.com/community/CloudInit
 [23]: https://console.aws.amazon.com/ec2/home?region=eu-west-1
 [24]: /ferdyblog/images/2011/09/juju-init.png
 [25]: http://en.wikipedia.org/wiki/Wildcard_DNS_record
 [26]: http://www.mysql.com/
 [27]: http://www.mongodb.org/
 [28]: http://redis.io/
 [29]: /ferdyblog/images/2011/09/juju-terminated.png
 [30]: https://juju.ubuntu.com/docs/write-formula.html

## Comments

### Comment by Rogelio on 2012-03-06 19:59:48 +0000
Ferdy, 

Google me trajo aqui cuando busque: &#8220;cloudfoundry ec2 ami&#8221;. Encuentro muy interesante tu blog, tenemos algunos intereses comunes. 

Al igual que tú, en este momento estoy interesado en open source PaaS como CloudFoundry. Los conoci en la conferencia CloudExpo 2011 en Santa Clara, CA. Todavia no he tenido una oportunidad de conocer OpenStack. 

Mi objetivo es utilizar la plataforma tanto para aplicaciones front-end web y batch jobs: spring batch y Hadoop. Me gusta CloudFoundry para usarlo en Amazon EC2 o en nuestras propias instalaciones.

Soy originario de Mexico, vivo en el sur de California, arriba el español!

Gracias por la informacion en tu blog, lo visitare nuevamente en un futuro.

Rogelio

### Comment by ferdy on 2012-03-06 23:13:57 +0000
Bienvenido al blog Rogelio.

### Comment by fernando Gutierrez on 2012-07-29 15:23:32 +0000
ferdy, no me ha quedado muy claro la verdadera funcionalidad del servicio de juju, pues tengo una instancia en amazon AWS gratis por un año y directamente y sin unstakar nada en una instancia, monte el servidor de ubuntu y configure un servidior web, corro una aplicación, pero esto no es del todo gratis, porque si me paso de uso y otras servicios me cobran, entonces cual es el papel con juju, si segun entiendo se conectara a Amazon y hay crear un usuario y pues siempre te cobraran ,si te pasas de que ofrecen. Me imagene que juju, servia para montar o conectarse a una cloud gratuita de ubuntu??.

saludos,

### Comment by ferdy on 2012-08-05 22:19:21 +0000
Fernando, juju no proporciona ningún servicio de cloud (ni gratis ni de pago), es un servicio para poder orquestar la instalación de productos de una forma sencilla en entornos cloud. Por decirlo de otra manera, en vez de instalarte tu mismo el servidor web con la BBDD (etc), juju te proporciona una especia de recetas para simplificarte la instalación y posterior mantenimiento (escalado, actualización, &#8230;).

### Comment by Pablo on 2012-11-03 07:36:10 +0000
Estoy intentando configurar un nube privada con Ubuntu Cloud y he tenido algunos problemas con la configuración del environment de juju, ¿hay alguna manera similar de configurar juju para una nube privada con Ubuntu Cloud Infraestructure utilizando MAAS?, es decir, ¿es similar el procedimiento de configuración de una nube privada como de una publica?.

### Comment by Jamelgo on 2013-06-10 11:27:50 +0000
Esto está bastante desfasado.

### Comment by Eduardo Peredo on 2013-12-03 20:29:36 +0000
Por lo que entiendo es una especie de consola para la administración de los &#8220;charms&#8221;, pero lo que me queda duda es si la administración es local o remota. Jugare con juju un rato para averiguarlo.