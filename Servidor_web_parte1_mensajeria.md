SERVIDOR WEB

El servidor web no guarda ningún recuerdo de quien ha hecho una petición, no tiene memoria.

FUNCIONAMIENTO DE PROTOCOLO
- Línea inicial del mensaje: Petición (GET), respuesta (HTTP)
- Cabecera del mensaje
- Cuerpo del mensaje

Métodos de envío de datos utilizados:
- GET: solicita un documento al servidor.
- HEAD: Similar a GET, pero solo pide las cabeceras HTTP. Pide información de un recurso, pero no el recurso en sí, sino la caberas.
- POST: Manda datos al servidor para su procesado, como GET pero enviando información (formulario).
- PUT: Permite subir un fichero al servidor. Almacena el documento enviado en el cuerpo del mensaje.
- DELETE: Elimina el cocumento referenciado en la URL.

CODIGOS DE ESTADOS:
- 1xx: mensaje iformativo.
- 2xx: éxito
	* 200 OK
- 3xx redirección
- 4xx: error del cliente
	* 400 bad request
	* 401 No tenemos autorización
- 5xx: error en el servidor


CABECERAS
- Host
- User-agent: tiene mucha información como el navegador que está accediendo a nuestra página, etc.
- Server
- Cache-control: información sobre la cache. 
- Content-type
- Content-encoding
- Expires: pide la fecha de expiración al servidor. Esto lo utiliza el proxy que tiene páginas cacheadas y las tiene guardadas para ver si han cambiado. 
- Location: muy importante para las redirecciones. Pide un contenido, pero no está, luego se envía la nueva dirección en el location. 
- Set-cookie.

COOKIES: las cookies son información que el navegagor guarda en memoria o en el disco duro dentro de ficheros de texto, a solicitud del servidor. Lo guarda el cliente, el servidor busca si cada cliente tiene esta información guardada (por ejemplo, el carrito de la compra).

SESION: es lo mismo que las cookies pero la información la guarda en el servidor. HTTP es un protocolo sin manejo de estado. Las sesiones nos permiten definir estados, para ello el servidor almacenará la información necesaria para llevar el seguimiento de la sesión. 

AUTENTIFICACIÓN: características de los servidores web que cada vez se usa menos.Es el servidor web el que pide la autentificación, no la aplicación web. Esto es una de las cosas que antes era muy común de los servodores web y ya no.

CONEXIONES PERSISTENTES: permite que varias peticiones y respuestas sean tranferidas usando la misma conexión TCP. 


-----------------------------------------------------------------------
Hacer una petición get:
GET http//josedom24.org...

Hacer un head:
HEAD http//josedom24.org...
Se ve la primera línea de la cabecera y toda la información de la cabecera. 
200 ok
cache-control: max-age=600 -- Indica cuando expira
Connection: close
Date: Mon, 07 Oct 2019 07:01:55 GMT
Via: 1.1 varnish, 1.1 f0.41011038.41.andared.ced.junta-andalucia.es:3128 (squid/2.7.STABLE9)
Accept-Ranges: bytes
Age: 0
ETag: "5ad8334e-16db"
Server: GitHub.com
Vary: Accept-Encoding
Content-Length: 5851
Content-Type: text/html; charset=utf-8
Expires: Mon, 07 Oct 2019 07:11:55 GMT
Last-Modified: Thu, 19 Apr 2018 06:12:30 GMT
Access-Control-Allow-Origin: *
Client-Date: Mon, 07 Oct 2019 07:01:56 GMT
Client-Peer: 185.199.109.153:80
Client-Response-Num: 1
X-Cache: MISS
X-Cache: MISS from f0.41011038.41.andared.ced.junta-andalucia.es
X-Cache-Hits: 0
X-Cache-Lookup: MISS from f0.41011038.41.andared.ced.junta-andalucia.es:3128
X-Fastly-Request-ID: de262206d9a8d2c07542d7d56e697e768cf61a82
X-GitHub-Request-Id: 3860:3FB2:4BC154:65CEF0:5D9AE2E3
X-Proxy-Cache: MISS
X-Served-By: cache-mad22035-MAD
X-Timer: S1570431716.516475,VS0,VE464



