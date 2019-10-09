# Configuración de acceso

## Configuración de los puertos
Fichero: /etc/apache2/ports.conf
Directiva: Listen

> Ejemplo: Virtual Host basado en IP

~~~
<VirtualHost 172.2.30.40:80>
	ServerAdmin webmaster@example.com
	DocumentRoot "/www/vhost/www2"
	ServerName www2.example.org
	ErrorLog "/www/logs/www2/error_log"
	CustomLog "/www/logs/www2/access_log" combined
</VirtualHost>
~~~

> Ejemplo: Servir el mismo contenido en varias IP

~~~
<VirtualHost 172.2.30.40:80 192.168.1.1>
	DocumentRoot "/www/server1"
	ServerName server.example.com
	ServerAlias server
</VirtualHost>
~~~

> Ejemplo: sirviendo distintos sitios en distintos puertos

Hay que configurar /etc/apache2/ports.conf

~~~
<VirtualHost *:80>
	DocumentRoot "/www/domain-80"
	ServerName www.example.com
</VirtualHost>
~~~
	
~~~
<VirtualHost *:8080>
	DocumentRoot "/www/domain-8080"
	ServerName www.example.com
</VirtualHost>
~~~
	

Nosotros vamos a utilizaar siempre los basados por nombre.


## Opciones del direcorio
Directiva: options
- All
- FollowSymLinks. Los ficheros que están en otro direcotrio que no esté configurado no se pueden ver. Pero, si en uno de los ficheros tengo un link simbólico que me lleve a ese lugar, con esta opción te permite ver ese fichero. 
- Indexes. Si el cliente solicita un directorio en el que no exista ninguno de los ficheros especificados en **DirectoryIndex**, el servidor ofrecerá un listado de los archivos del directorio.
- MultiViews (este ya no se utiliza) Hay determinadas opciones de la cabecera que según lo que aparezca muestra un fichero u otro. Ejemplo: Muestra la página en inglés si tu navegador está en inglés y en español si está en español. 
- SymLinksIfOwnerMatch. Esto es como FollowSymLinks pero más restrictivo, puesto que para que se vean los ficheros ambos ficheros (el que está dentro y el que está fuera, deben ser del mismo propietario.
- ExecCGI (este ya no se utiliza) Para el uso de programas CGI, pero esto está en desuso. 

En /etc/apache2/apache2.conf

~~~
<Directory /var/www/>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory>
~~~

O en /etc/apache2/sites-available/000-default.conf, donde especifica que el fichero va a tener las mismas opciones que el padre, más determinadas opciones o - determinadas opciones.

~~~
<Directory /var/www/default>
	Options +Multiviews
	AllowOverride None
	Require all granted
</Directory>
~~~

~~~
<Directory /var/www/default>
	Options -Indexes
	AllowOverride None
	Require all granted
</Directory>
~~~

Si tenemos una página web en un hosting y, en él, un servidor web Apache y queremos cambiar las opciones, pero no eres el administrador, puedes configurarlo. Esto es una opción única de Apache. Se configura en **.htaccess**, que está ubicado en el documentRoot donde puedes poner las mismas opciones que en los casos anteriores. Pero tiene que estar permitida con **AllowOverride** All/None.

~~~
<Directory /var/www/default>
	Options -Indexes
	AllowOverride All
	Require all granted
</Directory>
~~~

> Lo lógico es que en el fichero de configuración general /etc/apache2/apache2.conf no tenga esta opción activada y que se active en los direcotrios específicos donde se quieran activar. 


## Mapeo de URL
	**URL**				**Fichero**
http://172.2.22.1	 	  /var/www/html/index.html
http://172.2.22.1/entrada	  /var/www/html/entrada/index.html
http://172.2.22.1/entrada/ima.jpg /var/www/html/entrada/index.html/img.jpg

El ejemplo anterior es lo normal pero en algunos casos se utilizan los alias. Los alias nos permite que el servidor sirva ficheros desde cualquier ubicación del sistema de archivo aunque esté fuera del direcotrio indicado en el DocumentRoot. Cuando creamos un alias, a continuación debemos crear un directory para darle los permisos oportunos.

~~~
Alias "/image" "/ftp/pub/image"
<Directory "/ftp/pub/image">
	Require all granted
</Directory>
~~~

**AliasMatch** es para usar expresiones irregulares.

~~~
AliasMatch "^/image/(.*)$" "/ftp/pub/image/$1"




