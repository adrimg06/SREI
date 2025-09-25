# SREI
------------------------------------------------------------------------------------------
Actividad 0.1 - HTTP Introduction
https://www.youtube.com/watch?v=eesqK59rhGA
https://www.youtube.com/watch?v=DuSURHrZG6I

¿Quién, dónde y cuándo se crea el primer servidor web?
El creador del primer servidor web creado fue obra de Tim Berners-Lee,  fue desarrollado en Suiza y entro en servicio el 6 de agosto de 1991.
¿Qué es pila de protocolos usados por http?
básicamente el http junta 4 protocolos los cuales son los siguientes:
Primero a nivel de aplicación es el propio http/https, En la capa de transporte en la cual actúa el TCP que se encarga de transportar la información. En la capa de red actúa la que todos conocemos como IP y por último la física o como mejor la conocemos “Enlace” es la que se encarga de que los protocolos de la capa física funcionen.
¿Componentes de una URL?
Los componentes de una URL son los siguientes:
El primer protocolo es el HTTP o el HTTPS que lo hemos explicado anteriormente, después pero no menos importante viene el dominio de la pagina web que es como el DNI de un ciudadano (Tiene que ser único porque o si no se solaparían). El siguiente componente es el puerto por el que se ve la pagina web, el siguiente es la ruta donde se encuentra los archivos los cuales e muestran la página web.
¿Pasos en la recuperación de una página web mediante HTTP?
Los pasos a seguir son los siguientes:
1. Entra en acción la DNS permitiendo que el navegador obtenga la dirección ip del servidor
2. Se conecta al servidor mediante los protocolos https y tcp
3. El protocolo http entra en acción pidiéndole la página al servidor
4. El servidor envía el contenido el cual le hemos pedido anteriormente
5. Por ultimo el navegador obtiene la página y la muestra al usuario que la halla solicitado.
	


Diferencia entre páginas dinámicas y estáticas
La diferencia entre una web dinámica es aquella que muestra el contenido según como se ha guardado en el servidor, la cual no cambia si alguien navega en ella. En cambio la dinámica genera su contenido de una manera flexible y personalizada según el usuario


¿Cómo usar telnet para acceder a un servidor web?
Se hace de la siguiente forma:
Se escribe “telnet nombre_del_servidor  80”
Telnet seria el comando que vamos a utilizar.
La siguiente parte es la URL con cual queremos establecer la conexión.
El 80 es el puerto para el http ya que el https no funciona por que va cifrado.
------------------------------------------------------------------------------------------
Actividad 2:

¿Diferencias entre udp y tcp? (min 2:46 y 4:15)
La principal diferencia es que TCP es confiable ya que esta diseñado para dar una conexión la cual asegura entrega y orden, esto hace que sea más lento. En cambio, el UPD es todo lo contrario al TCP,  siendo más rápido e ideal para los videojuegos y los video en directo (streaming)
¿Qué aplicaciones usan tcp?  http, smtp, pop, imap, ssh
	En cuanto el servicio https/https lo mas común que se utilicen las navegaciones web. El SMPT se utiliza para el envío de los correos electrónicos como puede ser Gmail. POP/IMAC pueden entra en la misma categoría ya que se encargan de la entrega del correo electrónico y por último el SSH se utiliza para el acceso remoto a los servidores.

¿Qué aplicaciones usan udp?
Como he comentado antes, este protocolo lo suelen utilizar aplicaciones que necesiten una buena velocidad de entrega como pueden ser los streaming de videos, videollamadas, videojuegos entre otros más.

¿Qué capa almacena el puerto?
La capa que almacena el puerto es la de transporte ya que se encarga de identificar aplicaciones y servicios del dispositivo.
¿Qué capa almacena la dirección IP?
La capa a la que corresponde la dirección ip es la de red, es decir, la de red ya que se encarga del enrutamiento y también de identificar los dispositivos que se conecten a la red.
¿Qué es three-way handshake?
Es un Sistema mediante 3 pasos que usa el protocolo TCP para iniciar una conexión solida entre el cliente y el servidor.



------------------------------------------------------------------------------------------
Actividad 0.5 - Práctica servidor web
Visita los siguientes enlaces:
Simple web server (ejemplo 1)
https://docs.python.org/3/library/http.server.html
python -m http.server 8000
http server (ejemplo 2)
https://github.com/python/cpython/blob/main/Lib/http/server.py
dummy web server (ejemplo 3)
https://gist.github.com/kabinpokhrel/6fd1275603e9d5f1e284be717cbd1bff


Instala Python.<br>
<br>
<img src="cmd.png" alt="Logo" width="200"/>
<br>
<br>
Ejecuta los ejemplos mostrados con anterioridad.<br>
<br>
<img src="vscode.png" alt="Logo" width="200"/>
<br>
<br>
Publica en GitHub los ejemplos llevados a cabo. Los ejemplos se acompañaran con capturas de pantalla en las que se muestre su funcionamiento.<br>
<br>
<img src="web.png" alt="Logo" width="200"/>
