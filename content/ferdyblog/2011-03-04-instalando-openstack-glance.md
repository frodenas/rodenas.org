---
title: Instalando Openstack Glance
author: ferdy
date: 2011-03-04T19:20:19+00:00
url: /ferdyblog/2011/03/04/instalando-openstack-glance/
fb2011:
  - 03
fbcategories:
  - General
fbtags:
  - cloud
  - glance
  - guia
  - instalacion
  - openstack

---
Hoy toca jugar con un nuevo servicio de Openstack, liberado hace muy poco tiempo, y que todavia se encuentra en fase &#8220;experimental&#8221;: [Openstack Glance][1].

Podr&iacute;amos definir a este proyecto como un servicio de gesti&oacute;n de imagenes de m&aacute;quinas virtuales, con el objetivo de independizar el sistema de computaci&oacute;n o almacenamiento de la gesti&oacute;n de las imagenes. De esta forma, podr&iacute;amos llegar a instanciar imagenes que se encontrasen almacenadas en localizaciones diferentes (incluso en sistemas gestionados por terceros: ¿un proveedor especializado en imagenes?), o podr&iacute;amos guardar copias de seguridad de instant&aacute;neas en otro centro de datos (por temas de <acronym title="Disaster Recovery">DR</acronym>), o podr&iacute;amos almacenar nuestras imagenes en nuestro repositorio, y cambiar de proveedor de <acronym title="Infrastructure As A Service">IaaS</acronym> tantas veces como quisi&eacute;semos sin tener que estar ligado a ellos (_vendor lockin_), o podr&iacute;amos &#8230; siempre y cuando los proveedores adopten Glance, claro est&aacute; (que f&aacute;cil es so&ntilde;ar 🙂 ). En definitiva, un proyecto con mucho potencial, aunque a expensas de que se convierta en un est&aacute;ndard y los proveedores lo quieran adoptar.

El proyecto se divide en 2 servicios: 

  * &#8220;_glance-registry_&#8220;, un servicio que nos permite registrar y descubrir imagenes de m&aacute;quinas virtuales;
  * &#8220;_glance-api_&#8220;, un servicio que nos permite almacenar y recuperar imagenes de m&aacute;quinas virtuales en repositorios diversos. A dia de hoy los repositorios pueden ser: un almacen en [Amazon S3][2], un almacen en [Openstack Swift][3], un sistema de ficheros, o un almacen HTTP.

<div id="attachment_158" style="width: 645px" class="wp-caption aligncenter">
  <img src="/ferdyblog/images/2011/03/openstack-glance.png" alt="" title="Openstack Glance" width="635" height="347" class="size-full wp-image-158" srcset="/ferdyblog/images/2011/03/openstack-glance.png 635w, /ferdyblog/images/2011/03/openstack-glance-300x163.png 300w" sizes="(max-width: 635px) 100vw, 635px" />
  
  <p class="wp-caption-text">
    Fuente: <a href='http://glance.openstack.org/architecture.htm'>Glance Architecture</a>
  
</div>

Pues bien, una vez definido el proyecto, detallemos las instrucciones de instalaci&oacute;n. Como he dicho anteriormente, el proyecto todavia es experimental, con lo que nos encontraremos muchas cosas por pulir.

En primer lugar añadiremos el repositorio PPA de Launchpad donde se encuentra el proyecto y lo instalaremos con el metodo habitual:
  
```
~$ sudo add-apt-repository ppa:glance-core/trunk
~$ sudo apt-get update
~$ sudo apt-get install glance
```

Ahora debemos configurar los servicios. Desgraciadamente el paquete no lleva ning&uacute;n ejemplo de archivo de configuraci&oacute;n, por lo que lo tendremos que crearlo a mano:
  
```
~$ cd
~$ mkdir glance
~$ cd glance
```

A continuaci&oacute;n copiad el siguiente texto en vuestro editor preferido y guardarlo como _glance.conf_. Para vuestra comodidad, lo podeis descargar de [aqu&iacute;][4] (acordaos de renombrarlo como _glance.conf_):
  
```
[DEFAULT]
# Show more verbose log output (sets INFO log level output)
verbose = True
# Show debugging output in logs (sets DEBUG log level output)
debug = False
[app:glance-api]
paste.app_factory = glance.server:app_factory
# Directory that the Filesystem backend store
# writes image data to
filesystem_store_datadir=/var/lib/glance/images/
# Which backend store should Glance use by default is not specified
# in a request to add a new image to Glance? Default: 'file'
# Available choices are 'file', 'swift', and 's3'
default_store = file
# Address to bind the API server
bind_host = 0.0.0.0
# Port the bind the API server to
bind_port = 9292
# Address to find the registry server
registry_host = 0.0.0.0
# Port the registry server is listening on
registry_port = 9191
[app:glance-registry]
paste.app_factory = glance.registry.server:app_factory
# Address to bind the registry server
bind_host = 0.0.0.0
# Port the bind the registry server to
bind_port = 9191
# SQLAlchemy connection string for the reference implementation
# registry server. Any valid SQLAlchemy connection string is fine.
# See: http://www.sqlalchemy.org/docs/05/reference/sqlalchemy/connections.html#sqlalchemy.create_engine
sql_connection = sqlite:///glance.sqlite
# Period in seconds after which SQLAlchemy should reestablish its connection
# to the database.
#
# MySQL uses a default `wait_timeout` of 8 hours, after which it will drop
# idle connections. This can result in 'MySQL Gone Away' exceptions. If you
# notice this, you can lower this value to ensure that SQLAlchemy reconnects
# before MySQL can drop the connection.
sql_idle_timeout = 3600
```

El siguiente paso es arrancar los servicios, tanto el _registry_ como el servidor _api_. Podemos arrancarlos de forma independiente, pero en este caso vamos a hacerlo de forma conjunta:
  
```
~/glance$ sudo glance-control all start
```

Si todo ha ido bien, el sistema nos dir&aacute; que ha arrancado los 2 servicios y que ha utilizado el archivo de configuraci&oacute;n _glance.conf_:
  
```
Starting glance-api with /home/ferdy/glance/glance.conf
Starting glance-registry with /home/ferdy/glance/glance.conf
```

Para comprobar que todo est&aacute; correcto, vamos a lanzar una consulta al servidor _api_. Para ello utilizaremos [curl][5], aunque podemos realizar la misma prueba desde nuestro navegador:
  
```
~/glance$ curl http://localhost:9292
```

Y el servidor nos devolver&aacute; las imagenes registradas (en este caso, ninguna):
  
```
{"images": []}
```

Ahora vamos a almacenar una imagen de una m&aacute;quina virtual. En primer lugar nos descargamos una imagen de Ubuntu (si ya ten&eacute;is una imagen, podeis saltaos este paso), y luego la almacenaremos y registraremos en el sistema:
  
```
~/glance$ wget http://uec-images.ubuntu.com/maverick/current/maverick-server-uec-amd64.tar.gz
~/glance$ glance-upload --type raw maverick-server-uec-amd64.tar.gz "Ubuntu Maverick 10.10"
```

Como respuesta recibiremos los metadatos de la imagen:
  
```
Stored image. Got identifier: {u'created_at': u'2011-03-04T23:47:58.145889',
 u'deleted': False,
 u'deleted_at': None,
 u'id': 1,
 u'is_public': True,
 u'location': u'file:///var/lib/glance/images/1',
 u'name': u'Ubuntu Maverick 10.10',
 u'properties': {},
 u'size': 187634470,
 u'status': u'active',
 u'type': u'raw',
 u'updated_at': None}
```

Ahora volvemos a realizar la consulta sobre el servidor _api_, y veremos que ya tenemos registrada nuestra imagen:
  
```
~/glance$ curl http://localhost:9292
{"images": [
   {"type": "raw",
    "id": 1,
    "name": "Ubuntu Maverick 10.10",
    "size": 187634470}
  ]
}
```

Incluso podemos pedirle que nos devuelva los metadatos completos de las imagenes registradas:
  
```
~/glance$ curl http://localhost:9292/images/detail
{"images": [
   {"status": "active",
    "name": "Ubuntu Maverick 10.10",
    "deleted": false,
    "created_at": "2011-03-04T23:47:58.145889",
    "updated_at": "2011-03-04T23:48:02.011583",
    "id": 1,
    "location": "file:///var/lib/glance/images/1",
    "is_public": true,
    "deleted_at": null,
    "type": "raw",
    "properties": {},
    "size": 187634470}
   ]
}
```

Y en el caso de que tengamos varias imagenes y queramos obtener los metadatos de una imagen en concreto, podemos utilizar el siguiente comando (aunque en este caso nos los devuelve en forma de _headers de HTTP_):
  
```
~/glance$ curl -I http://localhost:9292/images/1
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 0
X-Image-Meta-Type: raw
X-Image-Meta-Id: 1
X-Image-Meta-Deleted: False
X-Image-Meta-Location: file:///var/lib/glance/images/1
X-Image-Meta-Properties: {}
X-Image-Meta-Deleted_at: None
X-Image-Meta-Created_at: 2011-03-04T23:47:58.145889
X-Image-Meta-Size: 187634470
X-Image-Meta-Status: active
X-Image-Meta-Is_public: True
X-Image-Meta-Updated_at: 2011-03-04T23:48:02.011583
X-Image-Meta-Name: Ubuntu Maverick 10.10
Date: Fri, 04 Mar 2011 23:57:05 GMT
```

Y nada m&aacute;s, ya que de momento las opciones por l&iacute;nia de comando son muy limitadas. De igual forma, a dia de hoy no hay integraci&oacute;n con el sistema de computaci&oacute;n nova, por lo que tendremos que esperar a que un futuro no muy lejano se vayan ampliando las funcionalidades de este proyecto.

Y como siempre, antes de acabar, acordaos de apagar los servicios:
  
```
~/glance$ sudo glance-control all stop
Stopping glance-api  pid: 3518  signal: 15
Stopping glance-registry  pid: 3519  signal: 15
```

 [1]: https://launchpad.net/glance
 [2]: https://s3.amazonaws.com/
 [3]: http://www.openstack.org/projects/storage/
 [4]: /ferdyblog/images/2011/03/glance.conf_.txt
 [5]: http://curl.haxx.se/

## Comments

### Comment by Diego Parrilla on 2011-03-05 09:38:55 +0000
Gran post. Glance está verde todavía, pero la posibilidad de tener un registros distribuidos de imágenes por la red es algo muy potente.

En el Roadmap futuro el registro también realizará conversiones entre diferentes formatos de disco virtual y de contenedor (ovf, vmx, ami&#8230;). En ese punto lo incorporaremos a la distro de StackOps.

Diego Parrilla
  
StackOps CEO

### Comment by ferdy on 2011-03-06 00:52:44 +0000
Gracias Diego. Coincido contigo que este proyecto promete bastante, y creo adem&aacute;s, que favorecer&aacute; que aparezcan negocios relacionados con el almacenamiento y provisioning de imagenes.

### Comment by Armando on 2011-03-21 10:46:16 +0000
pero donde esta el paquete de instalación!!
  
eske tengo al profe aquí al lado i no para!!

### Comment by ferdy on 2011-03-21 23:47:24 +0000
Armando, ejecuta:
  
```
~$ sudo add-apt-repository ppa:glance-core/trunk
~$ sudo apt-get update
~$ sudo apt-get install glance
```
  
Y te instalará el paquete.

### Comment by Francisco on 2011-04-05 02:17:15 +0000
Que tal, esta muy bueno el blog, me ha ayudado mucho.

Podrían por favor colocar mas referencias a servidores que podemos cargar usando glance?

Estamos experimentando con esta aplicación, pero me gustaria probarla lo mas que sea posible.

Muchas gracias.

### Comment by daniel on 2014-03-04 18:32:39 +0000
alguien me puede ayudar a subir imagenes ISO a openstack lo tengo instalado pero no he podido subir nada aun, la maquina de cirros funciona super bien