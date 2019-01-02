---
title: Instalando el Dashboard de Openstack
author: ferdy
date: 2011-03-04T00:26:03+00:00
url: /ferdyblog/2011/03/04/instalando-el-dashboard-de-openstack/
fb2011:
  - 03
fbcategories:
  - General
fbtags:
  - cloud
  - dashboard
  - guia
  - instalacion
  - openstack

---
Como lo prometido es deuda, aqu&iacute; teneis las instrucciones para manejar openstack desde una consola web en vez de la línea de comandos.

Lo primero que deb&eacute;is hacer es instalar el sistema de control de versiones [bazaar][1], ya que el dashboard de Openstack todavia no est&aacute; disponible en forma de paquete:

```
~$ sudo apt-get install bzr
```

A continuaci&oacute;n vamos a instalar el m&oacute;dulo que contiene la interfaz para actuar con el controlador de openstack ([django-nova][2]):

```
~$ mkdir src
~$ cd src
~/src$ mkdir django-nova
~/src$ cd django-nova
~/src/django-nova$ bzr init-repo .
~/src/django-nova$ bzr branch lp:django-nova/trunk
```

Ahora instalaremos el m&oacute;dulo que contiene el dashboard ([openstack-dashboard][3]). Este m&oacute;dulo es una referencia que ha de servir de ejemplo para que otras empresas creen sus propios dashboards, y a dia de hoy no esta claro que en futuro se convierta en oficial, aunque a efectos de este tutorial ya nos vale:

```
~/src/django-nova$ cd ..
~/src$ mkdir openstack-dashboard
~/src$ cd openstack-dashboard
~/src/openstack-dashboard$ bzr init-repo .
~/src/openstack-dashboard$ bzr branch lp:openstack-dashboard trunk
```

Antes de arrancar la consola, debemos ajustar algunos parametros. En primer lugar creamos y editamos el archivo de configuraci&oacute;n (_local_settings.py_):

```
~/src/openstack-dashboard$ cd trunk/local
~/src/openstack-dashboard/trunk/local$ cp local_settings.py.example local_settings.py
~/src/openstack-dashboard/trunk/local$ vi local_settings.py
```

En este archivo debemos especificar los siguientes par&aacute;metros:

  * NOVA\_ACCESS\_KEY: debemos especificar el contenido de la variable EC2\_ACCESS\_KEY que encontrareis en el archivo _novarc_
  * NOVA\_SECRET\_KEY: debemos especificar el contenido de la variable EC2\_SECRET\_KEY que encontrareis en el archivo _novarc_
  * NOVA\_ADMIN\_USER: debemos especificar el contenido de la variable NOVA_USERNAME que encontrareis en el archivo _novarc_
  * NOVA_PROJECT: debemos especificar el nombre de un proyecto sobre el que el usuario indicado anteriormente tengo permisos

Ahora ya podemos seguir con el proceso de configuraci&oacute;n:

```
~/src/openstack-dashboard/trunk/local$ apt-get install -y python-setuptools
~/src/openstack-dashboard/trunk/local$ cd ..
~/src/openstack-dashboard/trunk$ sudo easy_install virtualenv
~/src/openstack-dashboard/trunk$ python tools/install_venv.py ../../django-nova/trunk
~/src/openstack-dashboard/trunk$ tools/with_venv.sh dashboard/manage.py syncdb
```

En este punto, el proceso de instalaci&oacute;n nos pedir&aacute; si queremos crear un usuario administrador de la consola. Indicamos que si queremos crearlo, y nos preguntar&aacute; por un nombre de usuario, nuestro email y una contrase&ntilde;a para el usuario a crear:

```
You just installed Django's auth system, which means you don't have any superusers defined.
Would you like to create one now? (yes/no): yes
Username (Leave blank to use 'ferdy'):
E-mail address: YOUR_EMAIL
Password: PASSWORD
Password (again): PASSWORD
```

Una vez instalados y configurados todos los m&oacute;dulos, vamos a arrancar el servidor web:

```
~/src/openstack-dashboard/trunk$ tools/with_venv.sh dashboard/manage.py runserver 0.0.0.0:8000
```

Y ahora nos conectaremos al dashboard utilizando la URL <http://localhost:8000>. Lo primero que nos aparecer&aacute; ser&aacute; la pantalla de login, donde introduciremos el usuario y contrase&ntilde;a que hemos creado anteriormente:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-login.png" alt="" title="Openstack Dashboard - Login" width="961" height="638" class="aligncenter size-full wp-image-133" srcset="/ferdyblog/images/2011/03/openstack-dashboard-login.png 961w, /ferdyblog/images/2011/03/openstack-dashboard-login-300x199.png 300w" sizes="(max-width: 961px) 100vw, 961px" />

Una vez conectados nos aparece una pantalla con la relaci&oacute;n de nuestros proyectos:

<img src="/ferdyblog/images/2011/03/openstack-dashboard.png" alt="" title="Openstack Dashboard" width="987" height="528" class="aligncenter size-full wp-image-136" srcset="/ferdyblog/images/2011/03/openstack-dashboard.png 987w, /ferdyblog/images/2011/03/openstack-dashboard-300x160.png 300w" sizes="(max-width: 987px) 100vw, 987px" />

Si consultamos &#8220;_Miproyecto_&#8221; os aparece el dashboard con las acciones que podeis realizar sobre el:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-project.png" alt="" title="Openstack Dashboard - Project" width="977" height="505" class="aligncenter size-full wp-image-134" srcset="/ferdyblog/images/2011/03/openstack-dashboard-project.png 977w, /ferdyblog/images/2011/03/openstack-dashboard-project-300x155.png 300w" sizes="(max-width: 977px) 100vw, 977px" />

En primer lugar vamos a consultar las imagenes publicadas. Pulsamos sobre el enlace de &#8220;_Images_&#8221; situado en el menu de la izquierda y nos aparece la relaci&oacute;n de imagenes disponibles:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-images.png" alt="" title="Openstack Dashboard - Images" width="976" height="754" class="aligncenter size-full wp-image-127" srcset="/ferdyblog/images/2011/03/openstack-dashboard-images.png 976w, /ferdyblog/images/2011/03/openstack-dashboard-images-300x231.png 300w" sizes="(max-width: 976px) 100vw, 976px" />

Si pulsamos en el identificador de la imagen emi (campo _ID_), nos aparecen los detalles de la imagen:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-image-detail.png" alt="" title="Openstack Dashboard- Image detail" width="974" height="765" class="aligncenter size-full wp-image-126" srcset="/ferdyblog/images/2011/03/openstack-dashboard-image-detail.png 974w, /ferdyblog/images/2011/03/openstack-dashboard-image-detail-300x235.png 300w" sizes="(max-width: 974px) 100vw, 974px" />

Ahora vamos a instanciarla. Pulsamos sobre &#8220;_Launch_&#8220;, y nos aparece una pantalla donde podremos indicar las caracter&iacute;sticas de la instancia que queremos arrancar. Escogemos que solo queremos arrancar _1_ instancia, indicamos el tipo de instancia (_m1.small_ – Memory: 2048MB, VCPUS: 1) y le asignamos la credencial _miclave_:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-launch-instance.png" alt="" title="Openstack Dashboard - Launch instance" width="982" height="796" class="aligncenter size-full wp-image-132" srcset="/ferdyblog/images/2011/03/openstack-dashboard-launch-instance.png 982w, /ferdyblog/images/2011/03/openstack-dashboard-launch-instance-300x243.png 300w" sizes="(max-width: 982px) 100vw, 982px" />

Ya tenemos la instancia lanzada. La aplicaci&oacute;n nos dirigir&aacute; a la pantalla de instancias donde podre&iacute;s ver todas las instancias junto con el estado de las mismas (campo _State_) y la direcci&oacute;n IP asignada:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-instance-launched.png" alt="" title="Openstack Dashboard - Instance launched" width="984" height="592" class="aligncenter size-full wp-image-129" srcset="/ferdyblog/images/2011/03/openstack-dashboard-instance-launched.png 984w, /ferdyblog/images/2011/03/openstack-dashboard-instance-launched-300x180.png 300w" sizes="(max-width: 984px) 100vw, 984px" />

Si pulsamos en el identificador de una instancia (camp _ID_), nos aparecen los detalles de la instancia:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-instance-detail.png" alt="" title="Openstack Dashboard - Instance detail" width="983" height="585" class="aligncenter size-full wp-image-128" srcset="/ferdyblog/images/2011/03/openstack-dashboard-instance-detail.png 983w, /ferdyblog/images/2011/03/openstack-dashboard-instance-detail-300x178.png 300w" sizes="(max-width: 983px) 100vw, 983px" />

Mientras esperamos a que la instancia est&eacute; disponible (estado _running_), nos vamos a ver las credenciales disponibles. Pulsamos sobre el enlace de _Keys_ situado en el menu de la izquierda y nos aparece la relaci&oacute;n de claves disponibles:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-keys.png" alt="" title="Openstack Dashboard - Keys" width="979" height="710" class="aligncenter size-full wp-image-131" srcset="/ferdyblog/images/2011/03/openstack-dashboard-keys.png 979w, /ferdyblog/images/2011/03/openstack-dashboard-keys-300x217.png 300w" sizes="(max-width: 979px) 100vw, 979px" />

Si pulsamos sobre el enlace de _Volumes_ en el menu de la izquierda, podremos ver la relaci&oacute;n de volumenes de almacenamiento disponibles:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-volumes.png" alt="" title="Openstack Dashboard - Volumes" width="977" height="756" class="aligncenter size-full wp-image-135" srcset="/ferdyblog/images/2011/03/openstack-dashboard-volumes.png 977w, /ferdyblog/images/2011/03/openstack-dashboard-volumes-300x232.png 300w" sizes="(max-width: 977px) 100vw, 977px" />

Ahora volvemos a las instancias para comprobar si ya esta disponible:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-instances.png" alt="" title="Openstack Dashboard - Instances" width="976" height="521" class="aligncenter size-full wp-image-130" srcset="/ferdyblog/images/2011/03/openstack-dashboard-instances.png 976w, /ferdyblog/images/2011/03/openstack-dashboard-instances-300x160.png 300w" sizes="(max-width: 976px) 100vw, 976px" />

En caso de que as&iacute; sea, podeis abrir una sesi&oacute;n de terminal y conectaros via SSH a vuestra instancia. Y como siempre, una vez os hay&aacute;is cansado de jugar, no os olvideis de apagar la instancia pulsando sobre &#8220;_Terminate_&#8220;:

<img src="/ferdyblog/images/2011/03/openstack-dashboard-instace-terminated.png" alt="" title="Openstack Dashboard - Instance terminated" width="982" height="567" class="aligncenter size-full wp-image-145" srcset="/ferdyblog/images/2011/03/openstack-dashboard-instace-terminated.png 982w, /ferdyblog/images/2011/03/openstack-dashboard-instace-terminated-300x173.png 300w" sizes="(max-width: 982px) 100vw, 982px" />

Para pr&oacute;ximos posts, intentar&eacute; explicar como configurar la gesti&oacute;n de almacenamiento.

 [1]: http://bazaar.canonical.com/en/
 [2]: https://launchpad.net/django-nova
 [3]: https://launchpad.net/openstack-dashboard

## Comments

### Comment by rmacian on 2011-04-28 17:45:11 +0000
Hola,

Primero de todos felicitarte por la cantidad de contenido por la brevedad de proyecto. 

He seguido la entrada de instalación y este y cuando ya estoy intentando arrancar la instancia se me queda en scheduling. Mirando los logs veo que aparece un error

Error: libvirt version is too old (does not support getVersion). Los paquetes instalados son los propios de launchpad excepto uno

\# dpkg -l | grep libvirt
  
ii libvirt-bin 0.8.8-1ubuntu3~ppalucid1 the programs for the libvirt library
  
ii libvirt0 0.8.8-1ubuntu3~ppalucid1 library for interfacing with different virtu
  
ii python-libvirt 0.7.5-5ubuntu27.9 libvirt Python bindings

Alguna idea ?

### Comment by ferdy on 2011-04-29 03:44:27 +0000
Hola, el problema lo tienes precisamente en el paquete del binding de Python para libvirt (python-libvirt), ya que, tal como dice el error, la version que tienes es obsoleta. Esta comprobación se <a href="https://code.launchpad.net/~justin-fathomdb/nova/libvirt-getversion-whackamole/+merge/54475" rel="nofollow">introdujo</a> en nova hace 1 mes aprox . 

Has probado a actualizar solo este paquete?

### Comment by chetan on 2011-06-24 15:33:25 +0000
Hello ,
  
We testing Openstack with single node environment , alll is going well , however having problem installing openstack-dashboard end up with error :
  
Installing custom SQL &#8230;
  
Installing indexes &#8230;
  
No fixtures found.

next we able to run WebUserInterFace however no way to login :shows erro 1110 [connection refused].

: my local_setttng.py :

import os

DEBUG = True
  
TEMPLATE_DEBUG = DEBUG
  
PROD = False
  
USE_SSL = False

LOCAL\_PATH = os.path.dirname(os.path.abspath(\\_\_file\_\_))
  
DATABASES = {
      
&#8216;default&#8217;: {
          
&#8216;ENGINE&#8217;: &#8216;django.db.backends.sqlite3&#8217;,
          
&#8216;NAME&#8217;: os.path.join(LOCAL\_PATH, &#8216;dashboard\_openstack.sqlite3&#8217;),
      
},
  
}

CACHE_BACKEND = &#8216;dummy://&#8217;

\# Send email to the console by default
  
EMAIL_BACKEND = &#8216;django.core.mail.backends.console.EmailBackend&#8217;
  
\# Or send them to /dev/null
  
#EMAIL_BACKEND = &#8216;django.core.mail.backends.dummy.EmailBackend&#8217;

\# django-mailer uses a different settings attribute
  
MAILER\_EMAIL\_BACKEND = EMAIL_BACKEND
  
EMAIL_HOST = &#8216;localhost&#8217;
  
EMAIL_PORT = 25
  
\# Configure these for your outgoing email host
  
\# EMAIL_HOST = &#8216;smtp.my-company.com&#8217;
  
\# EMAIL_PORT = 25
  
\# EMAIL\_HOST\_USER = &#8216;djangomail&#8217;
  
\# EMAIL\_HOST\_PASSWORD = &#8216;top-secret!&#8217;

OPENSTACK\_ADMIN\_TOKEN = &#8220;999888777666&#8221;
  
OPENSTACK\_KEYSTONE\_URL = &#8220;http://localhost:5000/v2.0/&#8221;

TOTAL\_CLOUD\_RAM_GB = 30

NOVA\_DEFAULT\_ENDPOINT = &#8216;http://localhost:8773/services/Cloud&#8217;
  
NOVA\_DEFAULT\_REGION = &#8216;nova&#8217;
  
NOVA\_ACCESS\_KEY = &#8216;261c1aac-398c-4f5d-9b1e-0b6a58d8d90d:nubeblog&#8217;
  
NOVA\_SECRET\_KEY = &#8216;8dec5030-11a2-4569-b7a9-8ffbcc7f2c5d&#8217;
  
NOVA\_ADMIN\_USER = &#8216;diego&#8217;
  
NOVA_PROJECT = &#8216;nubelog&#8217;

### Comment by ferdy on 2011-06-25 14:57:43 +0000
Chetan, I suggest you to open a ticket at the <a href="https://answers.launchpad.net/openstack-dashboard" rel="nofollow">Dashboard for OpensStack</a> Launchpad site.