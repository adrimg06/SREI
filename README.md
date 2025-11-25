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
Actividad 0.4 - Usando cUrl
https://curl.se/docs/manual.html

Busca información sobre el comando curl y muestra al menos cinco ejemplos de uso

El curl se conoce como una herramienta de la línea de comandos para transferir datos servidores usando los protocolos HTTP, HTTPS, FPT. Su sintaxis es (curl [opciones] [URL])
Ejemplos:
curl ejem -Descargar contenido
curl  -I ejem – Mostrar solo cabeceras
curl -o ejem – Guardar un archivo
curl -L ejem – Seguir redirecciones
curl -v ejem – Mostrar cabeceras mas el cuerpo

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


Para instalar apache devemos de hacer lo siguiente:
Hacemos un update e instalamos apache:
<img width="702" height="292" alt="image" src="https://github.com/user-attachments/assets/5858383d-301c-454a-b9c9-efc041c86d68" />

<img width="886" height="363" alt="image" src="https://github.com/user-attachments/assets/38e52fc5-5521-4022-a994-42489743cc93" />



Una vez que este instalado para poder enumerarlos le escribimos el siguiente comando:
 <img width="670" height="114" alt="image" src="https://github.com/user-attachments/assets/4e65d192-f7dd-4617-bc1d-d8e95b06c7d1" />

Después para que el tráfico este únicamente en el puerto 80 haremos lo siguiente:
 <img width="886" height="35" alt="image" src="https://github.com/user-attachments/assets/ca73b67d-5058-4d3c-8518-7b061c8dac82" />

Para comprobar que se han aplicado los cambios correctamente hacemos un status:
 
<img width="886" height="96" alt="image" src="https://github.com/user-attachments/assets/e1a7bd78-f38d-487b-a100-1b7f0b11f210" />


Nos aparece que esta inactivo por lo que hay que levantarlo de la siguiente forma:
 
<img width="886" height="269" alt="image" src="https://github.com/user-attachments/assets/4f6c0faf-4384-49d8-896f-147ba51ab17f" />

Una vez que este activo al poner el locaclhost nos saldrá lo siguiente:
 <img width="886" height="492" alt="image" src="https://github.com/user-attachments/assets/65725284-f5f2-4c78-9519-04cece355620" />


Para ver la dirección ip del servidor hay que utilizar el siguiente comando:
 <img width="886" height="64" alt="image" src="https://github.com/user-attachments/assets/4fbcb272-5aef-4e91-b0b3-aa2173adbefc" />

Para cambiarle la url lo haremos con el siguiente comando:
 

<img width="886" height="23" alt="image" src="https://github.com/user-attachments/assets/2778f80b-997b-4f0c-9e7f-be314dbc93fc" />







Instalación mysql-server

Para instalar hacemos un sudo apt de la siguiente forma:
 
<img width="886" height="149" alt="image" src="https://github.com/user-attachments/assets/66a38d47-f5f1-43f5-a39a-21868722fff6" />

Cuando la instalación se complete, se recomienda ejecutar una secuencia de comandos de seguridad que viene preinstalada en MySQL Con esta secuencia de comandos se eliminarán algunos ajustes predeterminados poco seguros y se bloqueará el acceso a su sistema de base de datos. Inicie la secuencia de comandos interactiva ejecutando lo siguiente:
 
<img width="886" height="248" alt="image" src="https://github.com/user-attachments/assets/c267ed7e-5df2-4f12-a747-de5861364d36" />

Para establecer la fuerza de la contraseña será la siguiente:
 <img width="886" height="141" alt="image" src="https://github.com/user-attachments/assets/5f21d565-f2e5-4b78-b8e5-225908ed7dd5" />


En la siguiente ventana nos pregunta que si queremos eliminar usuarios anónimos, le damos a que si:  
<img width="886" height="188" alt="image" src="https://github.com/user-attachments/assets/23b2fc67-18ba-410d-baa2-05d90624a90f" />

Para entrar dentro del servicio ponemos el comando siguiente:
 <img width="886" height="285" alt="image" src="https://github.com/user-attachments/assets/455f074a-089d-4682-a1ab-4494241bfe0a" />


Para salir ponemos exit : 
 <img width="886" height="161" alt="image" src="https://github.com/user-attachments/assets/00397d6f-967a-4f5a-b35f-97fc2ea3d4a1" />


Instalación php:

Para instalar php ponemos el siguiente comando:
 <img width="886" height="40" alt="image" src="https://github.com/user-attachments/assets/b24633ac-f48f-405d-af24-09a9a3fa7f1a" />

Para ver nuestra versión de PHP ponemos el siguiente comando:
 <img width="859" height="39" alt="image" src="https://github.com/user-attachments/assets/5c801356-7d04-443f-bfbd-14ea0827c4cf" />

Aquí tenemos la versión:
 <img width="886" height="97" alt="image" src="https://github.com/user-attachments/assets/e3dd6898-0a8d-4022-bcdf-e47df9739981" />

Creamos el directorio para nuestro dominio de la siguiente manera:
 <img width="886" height="40" alt="image" src="https://github.com/user-attachments/assets/0a9b9d24-7bcd-476e-8920-1ac10b90dd90" />


Ahora le pondremos propiedades de usuario al servicio PHP de la siguiente manera:
 
<img width="886" height="48" alt="image" src="https://github.com/user-attachments/assets/a7739a07-445a-49e7-a476-28c67397e035" />

Se nos creara un archivo el cual lo abriremos con un nano:
 <img width="886" height="23" alt="image" src="https://github.com/user-attachments/assets/d2190187-b585-44bb-b010-93c26495f876" />

Una vez que estemos dentro del nano ponemos esta configuración básica:
 
<img width="886" height="315" alt="image" src="https://github.com/user-attachments/assets/fef65eaa-0f8c-494a-9fed-4e78ee60f68f" />

Ahora hacemos un a2ensite para habilitar el host virtual:
 
<img width="886" height="95" alt="image" src="https://github.com/user-attachments/assets/5dcf0990-c787-479c-a717-4874d04c01ed" />

Para desactivar el html por defecto de apache pondremos lo siguiente:
 <img width="886" height="102" alt="image" src="https://github.com/user-attachments/assets/96b98359-9012-4820-acc0-06d3f7b0a379" />

Para asegurarnos de que no tiene errores ejecutaremos lo siguiente:
 
<img width="886" height="54" alt="image" src="https://github.com/user-attachments/assets/ab0e4bcc-8a0b-4eac-81b1-1e3d99a910bf" />

Para poder cargar apache tenemos que hacer el siguiente systemctl:
 <img width="886" height="31" alt="image" src="https://github.com/user-attachments/assets/bffe4271-cc3d-4132-9f63-dae67658e3af" />

En el siguiente apartado crearemos un html para sustituir el que teníamos antes por defecto de apache:
 
<img width="886" height="37" alt="image" src="https://github.com/user-attachments/assets/b53b6c26-46f0-4ba9-a7a9-d2699306bbd4" />



Por último podemos ver que ya nos muestra por defecto el html:
<img width="886" height="496" alt="image" src="https://github.com/user-attachments/assets/5436ae1c-0a51-461a-a3e1-98d321378264" />




Actividad #2.1
 Para empezar vamos a cambiar el puerto de escucha el cual lo haremos con el siguiente comando:
    <img width="886" height="91" alt="image" src="https://github.com/user-attachments/assets/4b721198-c980-4e5b-8b3b-8e131c6f2730" />

Añadimos esta línea a continuación:
<img width="886" height="401" alt="image" src="https://github.com/user-attachments/assets/fe16c7df-d34f-4112-a7c7-9b8ead59b662" />

después pasaremos a editar el virtual host el cual podremos acceder de la siguiente forma:
<img width="886" height="31" alt="image" src="https://github.com/user-attachments/assets/999d331b-1f89-46e7-9dc0-ae0e45a3d0aa" />

Una vez aquí cambiamos la primera línea por el 81:
<img width="886" height="234" alt="image" src="https://github.com/user-attachments/assets/453c43fd-ca35-4b9a-b656-39826ad1c8aa" />

Reiniciamos apache:
<img width="886" height="28" alt="image" src="https://github.com/user-attachments/assets/f7077c3c-7c26-425a-b48b-19133e6040e9" />
después le añadimos el dominio de la siguiente forma:
 <img width="886" height="37" alt="image" src="https://github.com/user-attachments/assets/760e57b8-f08a-4aa1-9010-ee560315972a" />

Le ponemos el dominio de la marisma:
 <img width="886" height="234" alt="image" src="https://github.com/user-attachments/assets/a930994d-6124-43c8-a239-35c553339e70" />


Después pasamos a cambiar la directiva Server Tokens:
Vamos a editar la configuración de seguridad de la siguiente forma:
 <img width="886" height="25" alt="image" src="https://github.com/user-attachments/assets/44c457d9-6b80-446b-a7bd-063b7ea6ea51" />

Una vez dentro cambiamos esta línea :
<img width="886" height="88" alt="image" src="https://github.com/user-attachments/assets/6fbdbf93-1ab3-4e41-8a67-b42becd06b26" />


Por esto para que se muestre con el nombre del producto:
 <img width="886" height="232" alt="image" src="https://github.com/user-attachments/assets/2927c70f-2c8e-4aa4-a23d-5e39f0b08175" />

Activamos la configuración por si acaso no está activada:
 <img width="886" height="35" alt="image" src="https://github.com/user-attachments/assets/0f13eb9f-9bd0-40d3-88fa-bbe48aa4f2f7" />

Para cambiar ServerSignature debemos hacer lo siguiente, utilizamos el comando anterior y buscamos los siguiente:
 <img width="886" height="25" alt="image" src="https://github.com/user-attachments/assets/7b777742-f515-480e-ad06-68b0c31d2a38" />



Buscamos lo siguiente:
 <img width="434" height="148" alt="image" src="https://github.com/user-attachments/assets/a2d29354-d379-4262-a71e-027d505af93f" />

Lo cambiamos por lo siguiente:
 <img width="886" height="185" alt="image" src="https://github.com/user-attachments/assets/731a816e-a52c-4b69-9ce2-5b2b98d5597a" />

Reiniciamos apache:
 <img width="886" height="31" alt="image" src="https://github.com/user-attachments/assets/c0f5bea0-219c-4971-af16-6dbacde04fa9" />

Crear directorios “prueba” y “prueba2” con páginas
Lo haremos de la siguiente forma:
 <img width="886" height="33" alt="image" src="https://github.com/user-attachments/assets/a65aa7fd-ff39-4065-9139-bc1216f049de" />
<img width="886" height="30" alt="image" src="https://github.com/user-attachments/assets/16b1bbfa-90f2-4469-81a3-5a5f8b380962" />

 
Añadimos algún contenido:
 <img width="886" height="141" alt="image" src="https://github.com/user-attachments/assets/e9d61643-c985-47f3-b28b-6624a732083d" />

Redirecciona todo el contenido de “prueba” a “prueba2”
Editamos el virtual host:
 <img width="886" height="19" alt="image" src="https://github.com/user-attachments/assets/f9346ee4-82cd-40f8-ae85-0eadd5c21dad" />

Dentro del virtual host añadimos lo siguiente:  
<img width="715" height="270" alt="image" src="https://github.com/user-attachments/assets/937a394a-fc49-4e5d-907f-101a88f8f7b7" />

Redirigir solo una página específica
Creamos la página destino:
 <img width="886" height="19" alt="image" src="https://github.com/user-attachments/assets/634645e0-789d-458f-9f5f-95ef3a2e5206" />

después hacemos lo mismo en el virtual host:
 
<img width="855" height="33" alt="image" src="https://github.com/user-attachments/assets/bc084729-4c40-4e02-b5ac-19ec9eb57988" />

Usar la directiva userdir:
Para ello debemos de habilitar el modulo de la siguiente forma:
 <img width="886" height="39" alt="image" src="https://github.com/user-attachments/assets/e668dfba-3cae-4d5c-853a-35e2b3cf9877" />

Para editar la configuración de modulo nos devemos ir adonde esta ubicado el userdir.conf:
 <img width="886" height="26" alt="image" src="https://github.com/user-attachments/assets/27e966ec-35db-4dc4-9b6f-792295fd45c6" />


Creamos la carpeta para el usuario de la siguiente forma y reiniciamos apache:
 <img width="886" height="60" alt="image" src="https://github.com/user-attachments/assets/984221a4-43dd-485d-b73d-129dd0d66936" />


Usar la directiva Alias para redirigir a una carpeta en tu directorio de usuario:
Volvemos a editar el archivo de configuración :
 <img width="886" height="19" alt="image" src="https://github.com/user-attachments/assets/5ed2e225-8bf3-448d-bec4-54e9c797f6ca" />


Dentro de virtualhost añadimos esto:
 <img width="886" height="192" alt="image" src="https://github.com/user-attachments/assets/c3708af0-05bd-4002-bd29-85204c506658" />

Creamos la carpeta y un archivo:
 <img width="886" height="55" alt="image" src="https://github.com/user-attachments/assets/fcef0460-4eb6-45c0-8d46-642cd6e30762" />

Directiva Options: ¿qué hace y cómo desactivar el listado de directorios?
Nos metemos otra vez en el virtual host y buscamos lo siguiente:
 <img width="886" height="170" alt="image" src="https://github.com/user-attachments/assets/adfe23d6-53a3-4aa8-968f-31a0f7ab070b" />


Lo cambiamos por lo siguiente y reiniciamos apache:
 <img width="786" height="178" alt="image" src="https://github.com/user-attachments/assets/fb436fe6-077d-4864-a735-bc8423a35683" />

Y hacemos el ultimo script el cual nos permita crear una página web con un título, una cabecera y un mensaje:
<img width="1221" height="687" alt="image" src="https://github.com/user-attachments/assets/d3ac6a7f-118d-416b-adbc-2d713cd8cb8c" />
Le damos permisos de ejecución:
<img width="708" height="52" alt="image" src="https://github.com/user-attachments/assets/cf733db2-84ba-4124-b6d5-3615d5dfe1b3" />

Actividad#3- Directiva directory

Primero creamos los directorios de la siguiente forma: <br>
<img width="582" height="45" alt="image" src="https://github.com/user-attachments/assets/c3c2cf78-9db8-4eba-b7f0-830b4b35a136" />
Explica qué diferencia existe entre ambos y muestra su equivalencia con la directiva Require:

En este primer bloque se aplican primero las reglas de DENY y luego las de ALLOW consiguiendo denegar todo solo permitiendo a 192.168.1.100
<Directory /var/www/example1>
Order Deny,Allow
Deny from All
Allow from 192.168.1.100
</Directory>
En este bloque se aplican de la forma contraria pero al final pone DENY from all lo que hace que se ignore todo lo anterior prohibiendo la entrada a todos.
<Directory /var/www/example1>
Order Allow,Deny
Deny from All
Allow from 192.168.1.100
</Directory>

Para dir1
Entramos en el archivo de configuración con el siguiente comando:<br>
<img width="582" height="72" alt="image" src="https://github.com/user-attachments/assets/efd3e1bd-848a-4077-b157-de8b2f49cadd" />

Permite el acceso de las peticiones provenientes de 10.3.0.100<br>
<img width="340" height="48" alt="image" src="https://github.com/user-attachments/assets/46ea0106-a1ad-4c93-80b0-049b9e2dfd2f" /><br>
Permite el acceso desde "marisma.intranet"<br>
<img width="470" height="50" alt="image" src="https://github.com/user-attachments/assets/ba60bb4b-4c1a-4403-acfa-3c58feae584b" /><br>
Permite el acceso desde cualquier subdominio de "marisma.intranet"<br>
<img width="577" height="53" alt="image" src="https://github.com/user-attachments/assets/6a9ae6b6-8137-44ae-8149-d7308bad5774" /><br>
ermite el acceso Pde las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"
<img width="501" height="51" alt="image" src="https://github.com/user-attachments/assets/a852a414-77ff-4123-b58a-f79b0bb68d79" /><br>

Quedaria asi:<br>
<img width="682" height="289" alt="image" src="https://github.com/user-attachments/assets/7f5a59de-68b5-4775-bb92-64f39771fd7b" />

Modifica la configuración de forma que el acceso a dir1:<br>
        1. Se permita a "marisma.intranet" y no se permita desde 10.3.0.101"<br>
		<img width="1016" height="320" alt="image" src="https://github.com/user-attachments/assets/bfc96c70-c940-4b48-b3d0-52527b2fa14a" /> <br>
Modifica la configuración de forma que el acceso a dir2:<br>
        1. Se permita a "10.3.0.100/8" y no a "marisma.intranet"<br>
<img width="330" height="146" alt="image" src="https://github.com/user-attachments/assets/d120d039-192c-4ea2-9cc9-61644ae638e2" /><br>
<br>

Actividad #4
1. Directorios en /www/ con 3 dígitos
<img width="893" height="39" alt="image" src="https://github.com/user-attachments/assets/f4e6295f-330c-4418-b67c-0e02fc583b71" />
2. Ficheros de imagen (*.gif, *.jpeg, *.jpg, *.png)
<img width="820" height="38" alt="image" src="https://github.com/user-attachments/assets/67fe6fbe-1cae-40d5-a673-f9afe6e4e294" />
El fichero de documentos nos debe de dar error:
<img width="948" height="108" alt="image" src="https://github.com/user-attachments/assets/08ffe41f-83c6-4b5e-ae89-0d5bac79549f" />
<br>
2. Creamos un archivo con los siguientes datos dentro:
 <img width="342" height="263" alt="image" src="https://github.com/user-attachments/assets/e580a275-fe17-4be1-a72a-26a63fdc0295" /> <br>
 1. Directorios en /www/ con 3 dígitos
    <img width="905" height="84" alt="image" src="https://github.com/user-attachments/assets/5515959e-0ba2-4d59-82ea-e0eee664a90d" /> <br>
	2. Ficheros de imagen (*.gif, *.jpeg, .jpg, .png)
  <img width="666" height="85" alt="image" src="https://github.com/user-attachments/assets/60657f52-9fd9-4bc4-bcde-0032b53406bb" />
  3. Números enteros y decimales
     <img width="663" height="80" alt="image" src="https://github.com/user-attachments/assets/ec67f08c-bfc9-44f8-b923-8bea8c6a6e05" />

4. Teléfonos formato americano
<img width="675" height="98" alt="image" src="https://github.com/user-attachments/assets/560a93d7-ae45-43c6-bcc4-f3474348e2fc" />

5. Palabras (letras)
<img width="670" height="188" alt="image" src="https://github.com/user-attachments/assets/63a11f36-7155-40f0-9f7f-604b3ff6366a" />

6. Códigos hexadecimales (Color)
   <img width="664" height="58" alt="image" src="https://github.com/user-attachments/assets/403b3ee1-4dbd-42b7-9bd0-080d13852032" />

7. Palabras de 4 letras
<img width="660" height="116" alt="image" src="https://github.com/user-attachments/assets/8caab064-5dda-482f-9d1d-222bda367a36" />

8. Número entero con signo
   <img width="666" height="149" alt="image" src="https://github.com/user-attachments/assets/181788ee-513a-494b-96c0-44c3c0931776" />

9. Números reales con exponente
    <img width="663" height="152" alt="image" src="https://github.com/user-attachments/assets/c7fc9e91-a2a6-4d9a-8dfb-661294b594bc" />

10. Email
<img width="663" height="152" alt="image" src="https://github.com/user-attachments/assets/a686f253-d562-4499-ab14-9b14b5f2e6ab" />

11. Números del 0 a 255
<img width="662" height="78" alt="image" src="https://github.com/user-attachments/assets/42244e8c-3521-4a0d-9204-725a040aa200" />



