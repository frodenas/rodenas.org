---
title: Instalando Openstack
author: ferdy
date: 2011-03-02T23:53:51+00:00
url: /ferdyblog/2011/03/03/instalando-openstack/
fb2011:
  - 03
fbcategories:
  - General
fbtags:
  - cloud
  - guia
  - instalacion
  - openstack

---
He estado jugando estos &uacute;ltimos dias con [OpenStack][1], una plataforma <acronym title="Infraestructure As A Service">IaaS</acronym> de c&oacute;digo abierto que nos permite la creaci&oacute;n de recursos de computaci&oacute;n ([OpenStack Nova][2]) y almacenamiento ([OpenStack Swift][3]) en la nube. El proyecto, liderado originalmente por [Rackspace][4] y la [Nasa][5], y a los que se les han a&ntilde;adido &uacute;ltimamente una importante [comunidad][6] de desarrolladores, fue creado hace tan solo unos pocos meses (Diego nos explica en su blog la [historia][7] de este proyecto), y aunque a dia de hoy sigue estando inmaduro, la &uacute;ltima versi&oacute;n liberada (Bexar) ya comienza a ser &#8220;usable&#8221;.

Si os animais a probarla, os detallo a continuaci&oacute;n los pasos que hay que seguir para su instalaci&oacute;n, aunque podeis encontrar mucha m&aacute;s informaci&oacute;n en la [wiki][8] o en los [manuales][9] del proyecto.

En primer lugar vamos a a&ntilde;adir el repositorio <acronym title="Personal Package Archives">PPA</acronym> de [Launchpad][10]. En mi caso, como me gusta jugar con fuego, voy a utilizar el repositorio donde se encuentran los paquetes &#8220;bleeding edge&#8221;, es decir, el repositorio donde se encuentran los &uacute;ltimos commits que se hayan hecho sobre el tronco:
  
```
~$ sudo apt-get install python-software-properties
~$ sudo add-apt-repository ppa:nova-core/trunk
~$ sudo apt-get update
```
  
(en caso de que querais utilizar la &uacute;ltima versi&oacute;n estable, cambiad el ppa:nova-core/trunk por ppa:nova-core/release)

A continuaci&oacute;n instalamos el paquete de nova junto con sus dependencias (es importante instalar primero el servidor de [RabbitMQ][11]):
  
```
~$ sudo apt-get install rabbitmq-server
~$ sudo apt-get install nova-common nova-doc nova-api nova-network nova-objectstore nova-scheduler nova-compute
~$ sudo apt-get install euca2ools unzip
```

El siguiente paso es configurar el paquete. En general, podeis dejar los ajustes por defecto (que se encuentran en /etc/nova/nova.conf), aunque en mi caso he tenido que realizar una peque&ntilde;a modificaci&oacute;n: si ejecutais el software en una máquina virtual (por ejemplo VirtualBox o Parallels), ser&aacute; necesario a&ntilde;adir al archivo nova.conf la siguiente l&iacute;nia:
  
```
--libvirt_type=qemu
```
  
Antes de comenzar a jugar, vamos a reiniciar por si acaso el servicio [libvirt][12] (la interfaz para interactuar con diferentes tecnolog&iacute;as de virtualizaci&oacute;n):
  
```
~$ sudo service libvirt-bin restart
```

Acto seguido configuramos una red para nuestras m&aacute;quinas virtuales. En este caso utilizaremos la direcci&oacute;n [CIDR][13] 10.0.0.0/8, sobre la que crearemos 1 red virtual con 64 direcciones IP:
  
```
~$ sudo nova-manage network create 10.0.0.0/8 1 64
```

Ahora nos creamos un usuario (_ferdy_) y un proyecto (_miproyecto_), nos descargaremos las credenciales (que vendr&aacute;n empaquetadas en el archivo _nova.zip_) y cargaremos en nuestro profile de usuario las variables necesarias para interactuar con el proyecto:
  
```
~$ cd
~$ mkdir proyecto-nova
~$ cd proyecto-nova
~/proyecto-nova$ sudo nova-manage user admin ferdy
~/proyecto-nova$ sudo nova-manage project create miproyecto ferdy
~/proyecto-nova$ sudo nova-manage project zipfile miproyecto ferdy
~/proyecto-nova$ unzip nova.zip
~/proyecto-nova$ . novarc
```

Llegados a este punto ya tenemos todo configurado. Es hora de descargarse una imagen y publicarla en un bucket (por ejemplo: _mibucket_). En este caso vamos a utilizar una imagen de Ubuntu Server de 64bits (en el [repositorio de Ubuntu][14] podeis encontrar m&aacute;s imagenes):
  
```
~/proyecto-nova$ wget http://uec-images.ubuntu.com/maverick/current/maverick-server-uec-amd64.tar.gz
~/proyecto-nova$ uec-publish-tarball maverick-server-uec-amd64.tar.gz mibucket
```

Como resultado nos informar&aacute; del identificador de imagen (_emi_), el identificador de kernel (_eki_) y el identificador de ramdisk (_eri_):
  
```
emi="ami-dqay5v06"; eri="none"; eki="ami-7l5uc5w8";
```
  
Es importante recordar el identificador de imagen, ya que ser&aacute; el que utilizemos en la creaci&oacute;n de instancias, pero si por cualquier raz&oacute;n lo olvidamos, con el comando _euca-describe-images_ podremos ver las imagenes publicadas junto con su emi:
  
```
IMAGE <b>ami-dqay5v06</b> mibucket/maverick-server-uec-amd64.img.manifest.xml	miproyecto  available	private		x86_64	machine	ami-7l5uc5w8
IMAGE ami-7l5uc5w8 mibucket/maverick-server-uec-amd64-vmlinuz-virtual.manifest.xml miproyecto	available	private		x86_64	kernel	true
```

A continuaci&oacute;n nos crearemos un par de claves (_miclave_) para poder acceder a nuestras m&aacute;quinas virtuales:
  
```
~/proyecto-nova$ euca-add-keypair miclave > miclave.priv
~/proyecto-nova$ chmod 0600 miclave.priv
```

Y crearemos una regla en el grupo de seguridad por defecto para autorizar el trafico entrante por el puerto 22 (SSH):
  
```
~/proyecto-nova$ euca-authorize default -P tcp -p 22 -s 0.0.0.0/0
```

Llegados a este punto ya podemos instanciar la m&aacute;quina virtual. En este caso utilizaremos una instancia de tipo peque&ntilde;o (_m1.tiny_ &#8211; Memory: 512MB, VCPUS: 1) y le asignaremos la credencial creada anteriormente (_miclave_). Acordaos de cambiar el identificador de la imagen por el vuestro:
  
```
~/proyecto-nova$ euca-run-instances <i>ami-dqay5v06</i> -k miclave -t m1.tiny
```

Que como resultado nos informar&aacute; del identificador de instancia (_i-nnnnnnnn_) y el estado (en este caso _scheduling_):
  
```
RESERVATION	r-6nwfk587 miproyecto	default
INSTANCE	<b>i-00000001</b> ami-dqay5v06 <b>scheduling</b>	miclave (miproyecto, None) 0	 m1.tiny	2011-03-02T23:17:32Z	unknown zone
```

Ahora vamos a esperar a que la instancia arranque. Con el comando _euca-describe-instances_ podemos conocer en que estado se encuentra y si se le ha asignado ya una direcci&oacute;n IP:
  
```
RESERVATION	r-6nwfk587 miproyecto	default
INSTANCE	i-00000001 ami-dqay5v06	<b>10.0.0.3</b>	10.0.0.3	<b>launching</b>	miclave (miproyecto, ubuntu)	0	m1.tiny	2011-03-02T23:17:32Z	nova
```

Una vez el estado pase a _running_:
  
```
RESERVATION	r-6nwfk587 miproyecto	default
INSTANCE	i-00000001 ami-dqay5v06	10.0.0.3	10.0.0.3	<b>running</b>	miclave (miproyecto, ubuntu)	0	m1.tiny	2011-03-02T23:17:32Z	nova
```
  
es hora de conectarnos a nuestra instancia. Para ello utilizaremos un SSH con las credenciales obtenidas anteriormente y la IP asignada a nuestra instancia:
  
```
~/proyecto-nova$ ssh -i miclave.priv root@<i>10.0.0.3</i>
```

Y finalmente, cuando os hay&aacute;is cansado de jugar, acordaos de apagar la instancia con el comando:
  
```
~/proyecto-nova$ euca-terminate-instances <i>i-00000001</i>
```

En el pr&oacute;ximo post explicar&eacute; como manejar estas instancias desde una consola web en vez de la l&iacute;nea de comandos.

 [1]: http://www.openstack.org/
 [2]: http://www.openstack.org/projects/compute/
 [3]: http://www.openstack.org/projects/storage/
 [4]: http://www.rackspace.com/cloud/
 [5]: http://www.nasa.gov/
 [6]: http://www.openstack.org/community/
 [7]: http://www.nubeblog.com/2011/01/10/un-vistazo-rapido-a-la-historia-de-openstack/
 [8]: http://wiki.openstack.org/StartingPage
 [9]: http://docs.openstack.org/
 [10]: https://launchpad.net/
 [11]: http://www.rabbitmq.com/
 [12]: http://libvirt.org/
 [13]: http://es.wikipedia.org/wiki/Classless_Inter-Domain_Routing
 [14]: http://uec-images.ubuntu.com/maverick/current/

## Comments

### Comment by Carlos on 2011-06-29 00:17:42 +0000
Muy bueno tu blog

Mi nombre es Carlos me gustaria saber mas sobre este tema y poder implemetar Open Stack

No se si me puedes recomendar alguna pagina o libro en internet para poder informarme mejor muchas gracias y sigue adelante

### Comment by ferdy on 2011-06-29 01:22:04 +0000
Carlos, la página de <a href="http://docs.openstack.org/" rel="nofollow">documentación</a> de OpenStack es un buen lugar de inicio. Y si no quieres complicarte la vida instalando OpenStack manualmente, puedes utilizar la distro de <a href="http://www.stackops.com/" rel="nofollow">StackOps</a>.

### Comment by Hernan Nina on 2011-10-03 04:15:16 +0000
Hola Ferdy,

Gracias por el Blog sobre OpenStack.

Que diferencia existe OpenStack con Adobe EC2

Saludos Gracias