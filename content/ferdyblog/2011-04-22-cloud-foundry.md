---
title: Cloud Foundry
author: ferdy
date: 2011-04-21T23:09:43+00:00
url: /ferdyblog/2011/04/22/cloud-foundry/
fb2011:
  - 04
fbcategories:
  - General
fbtags:
  - CloudFoundry
  - PaaS
  - SpringSource
  - VMWare

---
La compra hace 2 años de [SpringSource][1] por parte de [VMware][2] me pilló por sorpresa, ya que no entendia que hacia un proveedor de soluciones de virtualización comprando una empresa cuyo negocio era un framework para construir aplicaciones Java. Los analistas rápidamente comenzaron a elocubrar, que si VMware queria ampliar mercado ya que la cotización en bolsa estava estancada, que si significava la muerte de SpringSource (lo mismo dijeron de [Hyperic][3]), &#8230; Pero pocos se imaginaron entonces que su intención era ofrecer una solución <acronym title="Platform as a Service">PaaS</acronym>, a pesar de que en la [nota de prensa][4] lo decía muy claro y que a los pocos dias se [anunciara][5] [Cloud Foundry Enterprise Java Cloud][6], una especie de PaaS para aplicaciones Java corriendo en [AWS][7]. Pasado un tiempo, parecia además que no tenian una estrategia muy clara, que primero creo una [alianza][8] con [salesforce][9], que luego la [alianza][10] es también con Google. Pués bien, la semana pasada nos vuelven a sorprender y [anuncian][11] la creación de Cloud Foundry, un PaaS de código abierto.

¿En que se diferencia esta de otras soluciones como [Google AppEngine][12], [Heroku][13] o [Engine Yard][14]? Pués basicamente en 2 aspectos:

  * El primero es que es la primera plataforma PaaS liberada como open-source y que no está ligada a ningún entorno cloud concreto. Puedes descargarte el codigo, modificarlo, e instalarlo donde quieras (en local, en AWS/RackSpace/OpenStack, bajo una infraestructura VMware, &#8230;).
  * Y la segunda es que no está limitada ni a un lenguaje ni a un framework concreto, sino que admite algunos de los lenguajes y frameworks más populares actualmente, como Spring for Java, Grails, Ruby on Rails, Sinatra for Ruby y Node.js, además de soportar 3 motores de BD diferentes, MongoDB, MySQL y Redis.

En definitiva, que es la primera plataforma PaaS completamente gratuita y que no nos liga a una tecnologia en concreto (_vendor lock-in_). Como esta estrategia es bastante disruptiva, seguramente dinamizará el mercado y pronto veremos otras soluciones parecidas.

El servico se ofrecerá en 4 sabores, 2 de los cuales ya estan disponibles:

  * [CloudFoundry.com][15]: en entorno PaaS operado por Vmware, completamente montado y listo para usar. De momento este servicio está en beta y, por tanto, se ofrece de forma gratuita, aunque en un futuro está previsto que este entorno sea explotado comercialmente.
  * [CloudFoundry.org][16]: la comunidad open-source donde podremos participar en su desarrollo, y/o [descargar][17] e instalar la plataforma donde te plazca
  * Cloud Foundry Micro Cloud: una imagen gratuita para VMware Fusion o Player y lista para ser usada en tu escritorio. La idea es que puedas desarrollar y probar en tu propia estación de trabajo y luego despliegues contra un entorno de producción que se comporta exactamente igual al de tu escritorio. El servicio estará disponible durante el 2do trimestre de este año.
  * Cloud Foundry for the Enterprise and Service Providers: una versión comercial para ser utilizada en un entorno empresarial o por parte de proveedores de servicios que quieran ofrecer por si mismos un PaaS.

Si no lo has hecho ya, te recomiendo que pruebes la primera opción y te apuntes a la beta de [CloudFoundry.com][15]. Las invitaciones para probar el servicio se estan entregando con cuentagotas, pero con un poco de suerte te llegará una en breve. Como yo ya he recibido la mia, os voy a explicar mis experimentos.

En primer lugar instalamos [Ruby][18] y [RubyGems][19], ya que la interficie de comandos para interactuar con los servicios está basada en este lenguaje y viene empaquetada como una _gema_. Acto seguido procedemos a instalar _vmc_:

> ~$ sudo gem install vmc
  
> Fetching: vmc-0.3.10.gem (100%)
  
> Successfully installed vmc-0.3.10
  
> 1 gem installed
  
> Installing ri documentation for vmc-0.3.10&#8230;
  
> Installing RDoc documentation for vmc-0.3.10&#8230; 

Una vez instalada correctamente, indicamos que servidor nos va a dar servicio. En este caso escogeremos el servidor beta de cloudfoundy.com (aunque nos podemos descargar e instalar nuestro propio servidor):

> ~$ vmc target api.cloudfoundry.com
  
> Succesfully targeted to [http://api.cloudfoundry.com] 

Ahora le indicamos al servidor nuestras credenciales:

> ~$ vmc login
  
> Email: xxx@xxx.xxx
  
> Password: \***\***\***\***\*****
  
> Successfully logged into [http://api.cloudfoundry.com] 

Acto seguido nos creamos una aplicación de pruebas. Vamos con ejemplo sencillo usando Ruby y el framework de [Sinatra][20]:

> ~$ cd repos
  
> ~/repos$ mkdir test-frodenas
  
> ~/repos$ cd test-frodenas/
  
> ~/repos/test-frodenas$ vi test-frodenas.rb 
> 
> require &#8216;sinatra&#8217;
  
> get &#8216;/&#8217; do
    
> &#8220;Hello Ferdy from Cloud Foundry&#8221;
  
> end 

Y ahora vamos a desplegar nuestra aplicación. Dejaremos todas las opciones por defecto excepto el nombre de la aplicación:

> ~/repos/test-frodenas$ vmc push
  
> Would you like to deploy from the current directory? [Yn]:
  
> Application Name: test-frodenas
  
> Application Deployed URL: &#8216;test-frodenas.cloudfoundry.com&#8217;?
  
> Detected a Sinatra Application, is this correct? [Yn]:
  
> Memory Reservation \[Default:128M\] (64M, 128M, 256M, 512M, 1G or 2G)
  
> Creating Application: OK
  
> Would you like to bind any services to &#8216;test-frodenas&#8217;? [yN]:
  
> Uploading Application:
    
> Checking for available resources: OK
    
> Packing application: OK
    
> Uploading (0K): OK
  
> Push Status: OK
  
> Staging Application: OK
  
> Starting Application: OK 

Comprobamos que la aplicación se ha levantado correctamente:

> ~/repos/test-frodenas$ vmc instances test-frodenas
> 
> +&#8212;&#8212;-+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;+
  
> | Index | State | Start Time |
  
> +&#8212;&#8212;-+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;+
  
> | 0 | RUNNING | 04/21/2011 09:56PM |
  
> +&#8212;&#8212;-+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;+
> 
> ~/repos/test-frodenas$ vmc stats test-frodenas
> 
> +&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;&#8211;+
  
> | Instance | CPU (Cores) | Memory (limit) | Disk (limit) | Uptime |
  
> +&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;&#8211;+
  
> | 0 | 0.1% (4) | 22.0M (128M) | 44.0K (2G) | 0d:0h:2m:50s |
  
> +&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;&#8211;+

Y solo nos queda acceder a la URL de la aplicación para comprobar que responde:

<img src="/ferdyblog/images/2011/04/CloudFoundry-Test.png" alt="" title="CloudFoundry" width="1024" height="181" class="aligncenter size-full wp-image-193" srcset="/ferdyblog/images/2011/04/CloudFoundry-Test.png 1024w, /ferdyblog/images/2011/04/CloudFoundry-Test-300x53.png 300w" sizes="(max-width: 1024px) 100vw, 1024px" />

En caso de tener algún problema, podemos revisar los logs

> ~/repos/test-frodenas$ vmc logs test-frodenas
  
> ====> logs/stderr.log < ==== 172.30.8.253 - - [21/Apr/2011 19:57:27] "GET / HTTP/1.0" 200 30 0.0008 172.30.8.253 - - [21/Apr/2011 19:57:28] "GET / HTTP/1.0" 200 30 0.0003 172.30.8.253 - - [21/Apr/2011 19:57:28] "GET /favicon.ico HTTP/1.0" 404 18 0.0003 ====> logs/stdout.log < ==== == Sinatra/1.2.1 has taken the stage on 33248 for production with backup from Thin >> Thin web server (v1.2.11 codename Bat-Shit Crazy)
  
> >> Maximum connections set to 1024
  
> >> Listening on 0.0.0.0:33248, CTRL+C to stop 

Vamos a explorar que otras opciones tenemos disponibles:

> ~/repos/test-frodenas$ vmc help
> 
> Usage: vmc \[options] command [<args>\] \[command_options\]
  
> Try &#8216;vmc help [command]&#8217; or &#8216;vmc help options&#8217; for more information.
> 
> Currently available vmc commands are:
> 
> Getting Started
      
> target [url] Reports current target or sets a new target
      
> login \[email\] \[&#8211;email, &#8211;passwd\] Login
      
> info System and account information
> 
> Applications
      
> apps List deployed applications
> 
> Application Creation
      
> push [appname] Create, push, map, and start a new application
      
> push [appname] &#8211;path Push application from specified path
      
> push [appname] &#8211;url Set the url for the application
      
> push [appname] &#8211;instances <N> Set the expected number <n> of instances
      
> push [appname] &#8211;mem M Set the memory reservation for the application
      
> push [appname] &#8211;no-start Do not auto-start the application
> 
> Application Operations
      
> start <appname> Start the application
      
> stop <appname> Stop the application
      
> restart <appname> Restart the application
      
> delete <appname> Delete the application
      
> rename <appname> <newname> Rename the application
> 
> Application Updates
      
> update <appname> [&#8211;path] Update the application bits
      
> mem <appname> [memsize] Update the memory reservation for an application
      
> map <appname> <url> Register the application to the url
      
> unmap <appname> <url> Unregister the application from the url
      
> instances <appname> <num|delta> Scale the application instances up or down
> 
> Application Information
      
> crashes <appname> List recent application crashes
      
> crashlogs <appname> Display log information for crashed applications
      
> logs <appname> [&#8211;all] Display log information for the application
      
> files <appname> \[path\] \[&#8211;all\] Display directory listing or file download for [path]
      
> stats <appname> Display resource usage for the application
      
> instances <appname> List application instances
> 
> Application Environment
      
> env <appname> List application environment variables
      
> env-add <appname> <variable[=]value> Add an environment variable to an application
      
> env-del <appname> <variable> Delete an environment variable to an application
> 
> Services
      
> services Lists of services available and provisioned
      
> create-service <service> [&#8211;name,&#8211;bind] Create a provisioned service
      
> create-service <service> <name> Create a provisioned service and assign it <name>
      
> create-service <service> <name> <app> Create a provisioned service and assign it <name>, and bind to <app>
      
> delete-service [servicename] Delete a provisioned service
      
> bind-service <servicename> <appname> Bind a service to an application
      
> unbind-service <servicename> <appname> Unbind service from the application
      
> clone-services <src-app> <dest-app> Clone service bindings from <src-app&ft; application to <dest-app>
> 
> Administration
      
> user Display user account information
      
> passwd Change the password for the current user
      
> logout Logs current user out of the target system
      
> add-user [&#8211;email, &#8211;passwd] Register a new user (requires admin privileges)
      
> delete-user <user> Delete a user and all apps and services (requires admin privileges)
> 
> System
      
> runtimes Display the supported runtimes of the target system
      
> frameworks Display the recognized frameworks of the target system
> 
> Misc
      
> aliases List aliases
      
> alias <alias[=]command&lg; Create an alias for a command
      
> unalias <alias> Remove an alias
      
> targets List known targets and associated authorization tokens
> 
> Help
      
> help [command] Get general help or help on a specific command
      
> help options Get help on available options

Así pues una de las opciones es ver que entornos de ejecución tenemos disponibles:

> ~/repos/test-frodenas$ vmc runtimes
> 
> +&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8211;+
  
> | Name | Description | Version |
  
> +&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8211;+
  
> | node | Node.js | 0.4.5 |
  
> | java | Java 6 | 1.6 |
  
> | ruby18 | Ruby 1.8 | 1.8.7 |
  
> | ruby19 | Ruby 1.9 | 1.9.2p180 |
  
> +&#8212;&#8212;&#8211;+&#8212;&#8212;&#8212;&#8212;-+&#8212;&#8212;&#8212;&#8211;+ 

Los frameworks:

> ~/repos/test-frodenas$ vmc frameworks
> 
> +&#8212;&#8212;&#8212;+
  
> | Name |
  
> +&#8212;&#8212;&#8212;+
  
> | spring |
  
> | node |
  
> | grails |
  
> | sinatra |
  
> | rails3 |
  
> +&#8212;&#8212;&#8212;+

E incluso conocer los servicios que podemos utilizar:

> ~/repos/test-frodenas$ vmc services
> 
> ============== System Services ==============
> 
> +&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+
  
> | Service | Version | Description |
  
> +&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+
  
> | mysql | 5.1 | MySQL database service |
  
> | mongodb | 1.8 | MongoDB NoSQL store |
  
> | redis | 2.2 | Redis key-value store service |
  
> +&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-+
> 
> =========== Provisioned Services ============ 

Y ya solo nos queda parar o eliminar la aplicación para dejar el entorno limpio:

> ~/repos/test-frodenas$ vmc delete test-frodenas
  
> Deleting application [test-frodenas]: OK 

Si esto de trabajar con línea de comandos os parece \*anticuado\* y preferis utilizar un <acronym title="Integrated Development Environment">IDE</acronym>, teneis a vuestro disposición la [SpringSource Tool Suite][21], un editor completo para construir aplicaciones bajo Spring, o simplemente el [plugin][22] de CloudFoundry en el Marketplace de Eclipse. Os dejo algunas imagenes del plugin:

<img src="/ferdyblog/images/2011/04/CloudFoundry-STS-servers.png" alt="" title="CloudFoundry STS: Servers view" width="902" height="111" class="aligncenter size-full wp-image-197" srcset="/ferdyblog/images/2011/04/CloudFoundry-STS-servers.png 902w, /ferdyblog/images/2011/04/CloudFoundry-STS-servers-300x36.png 300w" sizes="(max-width: 902px) 100vw, 902px" />
  
<img src="/ferdyblog/images/2011/04/CloudFoundry-STS-remote-view.png" alt="" title="CloudFoundry STS: Remote View" width="896" height="263" class="aligncenter size-full wp-image-198" srcset="/ferdyblog/images/2011/04/CloudFoundry-STS-remote-view.png 896w, /ferdyblog/images/2011/04/CloudFoundry-STS-remote-view-300x88.png 300w" sizes="(max-width: 896px) 100vw, 896px" />

Tiene buena pinta ¿verdad? En un próximo post explicaré como instalar el entorno en tu propio servidor, ¿o alguien lo ha hecho ya y nos cuenta su experiencia?

 [1]: http://www.springsource.com/
 [2]: http://www.vmware.com/
 [3]: http://www.hyperic.com/
 [4]: http://www.vmware.com/company/news/releases/springsource.html
 [5]: http://www.springsource.com/newsevents/springsource-launches-enterprise-java-c
 [6]: http://classic.cloudfoundry.com/
 [7]: http://aws.amazon.com/
 [8]: https://www.vmware.com/company/news/releases/vmforce.html
 [9]: http://www.salesforce.com/
 [10]: http://www.vmware.com/company/news/releases/vmware-google.html
 [11]: http://www.vmware.com/company/news/releases/cloud-foundry-apr2011.html
 [12]: http://code.google.com/appengine/
 [13]: http://www.heroku.com
 [14]: http://www.engineyard.com/
 [15]: http://cloudfoundry.com/
 [16]: http://cloudfoundry.org/
 [17]: https://github.com/cloudfoundry
 [18]: http://www.ruby-lang.org/es/
 [19]: http://rubygems.org/
 [20]: http://www.sinatrarb.com/
 [21]: http://www.springsource.com/developer/sts
 [22]: http://marketplace.eclipse.org/content/cloud-foundry-integration

## Comments

### Comment by ialcazar on 2011-05-03 14:48:44 +0000
Buena entrada. Me ha quedado bastante claro las diferentes soluciones que van a plantear. Sin duda tiene una pinta excelente. Hoy mismo he hecho una prueba con la invitación que me han enviado.

Espero el siguiente post sobre como montar un servidor propio que seguro que le sacamos mucha utilidad.

Un saludo