# Servidor de Hosting Multi-Servicio con Ubuntu Server 24.04

Documentación completa para desplegar un servidor de hosting con Apache, PHP, MariaDB, FTP (FTPS), DNS (Bind9), Python/WSGI y Docker, sobre una máquina virtual en Proxmox.

---

## Índice

1. [Punto de partida](#1-punto-de-partida)
2. [Instalación de la base del servidor](#2-instalación-de-la-base-del-servidor)
3. [Configuraciones](#3-configuraciones)
   - 3.1 [Asegurar el FTP con certificados TLS](#31-asegurar-el-ftp-con-certificados-tls)
   - 3.2 [Preparar las zonas del DNS (Bind9)](#32-preparar-las-zonas-del-dns-bind9)
   - 3.3 [Habilitar Python en Apache](#33-habilitar-python-en-apache)
4. [Script de automatización](#4-script-de-automatización)
   - 4.1 [Comprobaciones](#41-comprobaciones)
5. [Docker](#5-docker)

---


## 1. Punto de partida

Se crea una máquina virtual en Proxmox con **Ubuntu Server 24.04 LTS**, asignándole un disco de **60 GB** y una **IP estática** para facilitar la administración posterior.

Pasos realizados:
- Creación de la MV en Proxmox.
- Selección de Ubuntu Server durante el arranque.
- Configuración del perfil de usuario.
- Instalación del servidor SSH durante el proceso de setup.
- Reinicio y acceso con las credenciales configuradas.

En este primer apartado vamos a crear la máquina virtual y darle una IP estática para facilitarnos la vida más adelante. Nos vamos a nuestro Proxmox y creamos una MV con Ubuntu Server 24.04 LTS: 

<img width="587" height="129" alt="image" src="https://github.com/user-attachments/assets/3a560ec7-7306-4c6a-be6b-f4eb31bc55c1" />

<img width="590" height="209" alt="image" src="https://github.com/user-attachments/assets/c693179f-9c29-46fb-8c18-1da8233568a4" />

Le asignamos un disco de 60 gigas: 

<img width="480" height="357" alt="image" src="https://github.com/user-attachments/assets/d07eb87b-0983-4cdb-a372-ad9220d503c8" />

Por último creamos la maquina:  
<img width="470" height="360" alt="image" src="https://github.com/user-attachments/assets/2dcd45c5-a33f-41f8-8899-18165e505d79" />

Encedemos la maquina y actualizamos el software:

<img width="466" height="289" alt="image" src="https://github.com/user-attachments/assets/1a9c2aa3-6a4c-48bd-9949-02288bb2e1ef" />

seleccionamos ubuntu server:

<img width="596" height="367" alt="image" src="https://github.com/user-attachments/assets/b2feb743-0415-46d4-a9ef-098246e04f24" />

Terminamos con toda la configuración y le damos a done:

<img width="501" height="308" alt="image" src="https://github.com/user-attachments/assets/4a4a1c1b-61d1-4c13-b848-caf30e11264a" />

Ponemos la siguiente configuracion de perfil: 

<img width="595" height="155" alt="image" src="https://github.com/user-attachments/assets/6e4b5a6c-28a9-4ccd-a525-8d2b200d085f" />

nstalamos el ssh:

<img width="387" height="237" alt="image" src="https://github.com/user-attachments/assets/ea62ba39-660f-4cb4-a862-d43907aaf42a" />

Una vez que terminemos reiniciamos la maquina y accedemos al login con las credenciales que hemos configurado: 

<img width="600" height="374" alt="image" src="https://github.com/user-attachments/assets/f12d4e37-f00a-4a28-9015-61f12fe42480" />

---

## 2. Instalación de la base del servidor

Instalación de todos los paquetes necesarios en un único comando:

```bash
sudo apt install apache2 php libapache2-mod-php php-mysql mariadb-server phpmyadmin vsftpd bind9 bind9utils dnsutils python3 libapache2-mod-wsgi-py3 -y
```

### Paquetes instalados y su función

| Paquete | Función |
|---|---|
| `apache2` | Servidor web principal |
| `php` + `libapache2-mod-php` | Soporte para páginas dinámicas PHP en Apache |
| `php-mysql` | Conexión de PHP con MariaDB/MySQL |
| `mariadb-server` | Motor de base de datos relacional (compatible con MySQL) |
| `phpmyadmin` | Interfaz web para administrar bases de datos desde el navegador |
| `vsftpd` | Servidor FTP seguro (Very Secure FTP Daemon) |
| `bind9` + `bind9utils` + `dnsutils` | Servidor DNS para resolución de nombres y subdominios |
| `python3` + `libapache2-mod-wsgi-py3` | Soporte para ejecutar aplicaciones Python a través de Apache (WSGI) |

### Durante la instalación

- Se selecciona **Apache2** como servidor web para phpMyAdmin.

  <img width="598" height="201" alt="image" src="https://github.com/user-attachments/assets/2ab57d73-d7e5-4a1b-8c92-5470261aebdf" />

- Se configura la base de datos de phpMyAdmin y se le asigna una contraseña.

<img width="525" height="141" alt="image" src="https://github.com/user-attachments/assets/9c0be474-d1b3-4c0f-8777-2dd76daaff36" />

Le asignamos una contraseña a base de datos: 

<img width="596" height="127" alt="image" src="https://github.com/user-attachments/assets/5fb1fd4f-09c2-4c7e-af43-b140d5283f63" />

Vemos como se crea todo correctamente: 

<img width="590" height="148" alt="image" src="https://github.com/user-attachments/assets/51efeab7-95d6-4690-928f-d3618a7cbabb" />

### Verificación de servicios

```bash
# Apache
sudo systemctl status apache2
```
<img width="595" height="201" alt="image" src="https://github.com/user-attachments/assets/cc570bd5-5aac-4c31-8ca0-9cc5d909f083" />

```bash
# MariaDB
sudo systemctl status mariadb
```
<img width="598" height="228" alt="image" src="https://github.com/user-attachments/assets/766ac43f-8a9c-4792-a45e-67ec55432c34" />

```bash
# FTP
sudo systemctl status vsftpd
```
<img width="595" height="120" alt="image" src="https://github.com/user-attachments/assets/9bdb755b-bc49-44c5-8d52-a386b604e339" />

```bash
# DNS
sudo systemctl status bind9
```
<img width="601" height="228" alt="image" src="https://github.com/user-attachments/assets/d522c867-7e4d-4698-8801-5066a4daa509" />

---

## 3. Configuraciones

El objetivo de esta sección es dejar todos los servicios configurados correctamente antes de ejecutar el script de automatización, para no tener que hacerlo manualmente cada vez.

### 3.1 Asegurar el FTP con certificados TLS

Se convierte el FTP estándar en **FTPS** generando un certificado TLS autofirmado:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/vsftpd.key \
  -out /etc/ssl/certs/vsftpd.crt \
  -subj "/C=ES/ST=Andalusia/L=Huelva/O=Hosting/CN=192.168.193.110"
```

<img width="600" height="138" alt="image" src="https://github.com/user-attachments/assets/7d52fa59-620e-4ec7-a5f8-2e63a4700388" />


Después se edita el archivo de configuración de vsftpd (`/etc/vsftpd.conf`):

<img width="599" height="35" alt="image" src="https://github.com/user-attachments/assets/f23c4ef1-352f-41b4-b0ca-6234477acd46" />


- Se descomenta `write_enable=YES` para permitir subida de archivos.
  
<img width="514" height="248" alt="image" src="https://github.com/user-attachments/assets/79a8784b-6051-4fac-b7f5-817f927e7a0b" />


- Se añade la configuración TLS apuntando a los certificados generados.
  
eliminamos esta configuracion y ponemos la siguiente: 


<img width="592" height="78" alt="image" src="https://github.com/user-attachments/assets/1ae6f7c6-0d3e-40ba-9b37-e7eef0df2d75" />

Ponemos esta: 

 <img width="467" height="198" alt="image" src="https://github.com/user-attachments/assets/36cceed2-beea-4a17-a55a-b2dfe910ecb7" />

Se guarda el archivo y se reinicia el servicio. Para verificar que el certificado funciona:

```bash
openssl s_client -connect 127.0.0.1:21 -starttls ftp
```


<img width="601" height="355" alt="image" src="https://github.com/user-attachments/assets/acf49f4f-1dd0-421b-b590-cb8d4e3d6613" />

---

### 3.2 Preparar las zonas del DNS (Bind9)

El dominio principal configurado es: `dominioadrian.local`

Se declaran las zonas en el archivo de configuración de Bind9 y se crean los archivos de zona directa e inversa.
Ponemos esta: 


<img width="598" height="102" alt="image" src="https://github.com/user-attachments/assets/396a62da-5035-4cf0-9bbf-345b6f2ecc56" />

**Zona directa** (`/etc/bind/db.dominioadrian.local`): traduce nombres de dominio a IPs.

<img width="599" height="168" alt="image" src="https://github.com/user-attachments/assets/7ac4aeec-12b5-4526-bda7-0a57e728b255" />

La comprobamos:

<img width="598" height="53" alt="image" src="https://github.com/user-attachments/assets/df9fe930-89ca-4591-80d7-8b970cb50a0a" />

**Zona inversa** (`/etc/bind/db.4`): traduce IPs a nombres de dominio.


<img width="598" height="179" alt="image" src="https://github.com/user-attachments/assets/f4f41a07-9b16-4680-96d9-968cb377df7f" />

Comprobamos la inversa: 

<img width="597" height="74" alt="image" src="https://github.com/user-attachments/assets/6f3f6596-22c0-43da-adf8-e2cb9aa7dc30" />

Reiniciamos el dominio: 

<img width="619" height="131" alt="image" src="https://github.com/user-attachments/assets/a103961a-0593-410c-a198-054f521b8072" />


Tras configurar ambas zonas se reinicia Bind9 y se comprueba con:

```bash
dig dominioadrian.local
```

<img width="603" height="48" alt="image" src="https://github.com/user-attachments/assets/395b0ffe-2bc1-4bda-8d0e-cd3b2dd30e63" />


---

### 3.3 Habilitar Python en Apache

El módulo `libapache2-mod-wsgi-py3` ya fue instalado previamente. Solo hay que habilitarlo:

```bash
sudo a2enmod wsgi
sudo systemctl restart apache2
```

<img width="543" height="84" alt="image" src="https://github.com/user-attachments/assets/b33ad6e0-7a49-4b03-b3ff-c4cbd68bf28e" />

Lo comprobamos de la siguiente forma: 

Se verifica que el módulo está activo consultando los módulos cargados en Apache.

<img width="597" height="84" alt="image" src="https://github.com/user-attachments/assets/56e82186-37ca-4752-bc72-0844b120d222" />

---

## 4. Script de automatización

El script `nuevo_cliente.sh` automatiza la creación completa de un cliente en el servidor: usuario del sistema, directorio web, base de datos, virtual host en Apache y registros DNS.

### Uso

```bash
sudo ./nuevo_cliente.sh <usuario> <contraseña>

# Ejemplo:
sudo ./nuevo_cliente.sh nerea 1234
```

### Contenido del script

```bash
#!/bin/bash

if [ "$#" -ne 2 ]; then
  echo "Introduzca los parámetros cliente y contraseña, por ese orden."
  echo "Ejemplo: sudo ./nuevo_cliente.sh cliente1 password123"
  exit 1
fi

USUARIO=$1
PASS=$2

DOMINIO="${USUARIO}.dominioadrian.local"
IP_SERVIDOR="10.4.0.183"
OCTETO_FINAL="183"

echo "*** Iniciando despliegue para el usuario: $USUARIO ***"

# [1/5] Crear usuario del sistema y directorio web
echo "[1/5] Creando usuario del sistema y directorio web..."
useradd -m -s /bin/bash $USUARIO
echo "$USUARIO:$PASS" | chpasswd

DIR_WEB="/home/$USUARIO/public_html"
mkdir -p $DIR_WEB

cat <<EOF > $DIR_WEB/index.php
<!DOCTYPE html>
<html>
<head><title>Bienvenido $USUARIO</title></head>
<body>
  <h1>Hosting configurado correctamente para $DOMINIO</h1>
  <?php echo "<p>Soporte PHP activado. ¡Hola mundo!</p>"; ?>
</body>
</html>
EOF

chown -R $USUARIO:www-data /home/$USUARIO
chmod -R 755 /home/$USUARIO

# [2/5] Crear base de datos y usuario SQL
echo "[2/5] Creando base de datos y usuario SQL..."
DB_NAME="${USUARIO}_db"
mysql -u root -e "CREATE DATABASE ${DB_NAME};"
mysql -u root -e "CREATE USER '${USUARIO}'@'localhost' IDENTIFIED BY '${PASS}';"
mysql -u root -e "GRANT ALL PRIVILEGES ON ${DB_NAME}.* TO '${USUARIO}'@'localhost';"
mysql -u root -e "FLUSH PRIVILEGES;"

# [3/5] Configurar Virtual Host en Apache
echo "[3/5] Configurando Virtual Host en Apache..."
VHOST_FILE="/etc/apache2/sites-available/${DOMINIO}.conf"

cat <<EOF > $VHOST_FILE
<VirtualHost *:80>
  ServerName $DOMINIO
  DocumentRoot $DIR_WEB

  <Directory $DIR_WEB>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>

  WSGIScriptAlias /python $DIR_WEB/app.wsgi
  <Directory $DIR_WEB>
    <Files app.wsgi>
      Require all granted
    </Files>
  </Directory>

  ErrorLog \${APACHE_LOG_DIR}/${USUARIO}_error.log
  CustomLog \${APACHE_LOG_DIR}/${USUARIO}_access.log combined
</VirtualHost>
EOF

cat <<EOF > $DIR_WEB/app.wsgi
def application(environ, start_response):
  status = '200 OK'
  output = b'Hola! La aplicacion Python funciona en tu hosting.\n'
  response_headers = [('Content-type', 'text/plain'),
                      ('Content-Length', str(len(output)))]
  start_response(status, response_headers)
  return [output]
EOF

chown $USUARIO:www-data $DIR_WEB/app.wsgi

a2ensite ${DOMINIO}.conf
systemctl reload apache2

# [4/5] Configurar registros DNS en Bind9
echo "[4/5] Configurando registros DNS en Bind9..."

ZONA_DIRECTA="/etc/bind/db.dominioadrian.local"
ZONA_INVERSA="/etc/bind/db.4"

echo "${USUARIO} IN A ${IP_SERVIDOR}" >> $ZONA_DIRECTA
echo "${OCTETO_FINAL} IN PTR ${DOMINIO}." >> $ZONA_INVERSA

systemctl restart bind9

# [5/5] Resumen final
echo "[5/5] ¡Proceso completado con éxito!"
echo "-----------------------------------------------------"
echo "Resumen de acceso:"
echo "- Web (PHP):        http://$DOMINIO"
echo "- Web (Python):     http://$DOMINIO/python"
echo "- Base de datos:    $DB_NAME (Usuario: $USUARIO)"
echo "- FTP/SSH/SFTP:     Usuario $USUARIO"
```

### Dar permisos y ejecutar

```bash
chmod +x nuevo_cliente.sh
sudo ./nuevo_cliente.sh nerea 1234
```

<img width="568" height="30" alt="image" src="https://github.com/user-attachments/assets/0b8c4218-50d9-4dd7-81fb-ae9bbd7fb99f" />

Para probar el script voy a crear el usuario llamado Nerea y de contraseña 1234: 

<img width="594" height="282" alt="image" src="https://github.com/user-attachments/assets/0c1742cc-65e2-4bd9-9972-71d811e8c7c4" />


### Lo que hace el script por cada cliente

1. Crea el usuario del sistema con su directorio `/home/<usuario>/public_html`.
2. Genera una página `index.php` de bienvenida con soporte PHP.
3. Crea una base de datos MariaDB y un usuario SQL exclusivo.
4. Configura un Virtual Host en Apache con soporte PHP y Python (WSGI).
5. Crea un script `app.wsgi` básico para probar Python.
6. Añade los registros DNS (A y PTR) en Bind9 y reinicia el servicio.

---

### 4.1 Comprobaciones

**Verificar resolución DNS del cliente:**

```bash
dig nerea.dominioadrian.local
```

<img width="595" height="51" alt="image" src="https://github.com/user-attachments/assets/6e8dda84-8a2f-4885-ab10-4065ed5607f6" />


**Actualizar el DNS del servidor para que use localhost** editando `/etc/netplan/*.yaml` y añadiendo:

```yaml
nameservers:
  addresses: [127.0.0.1, 8.8.8.8]
```


Aplicar cambios:

```bash
sudo netplan apply
```

**Probar la web PHP:**

```bash
curl http://nerea.dominioadrian.local
```

<img width="717" height="122" alt="image" src="https://github.com/user-attachments/assets/131e35f2-eb77-477d-923a-fac132a4578a" />

Después probamos la de python de la misma forma. Nos da fallos porque tenemos que introducir lo siguiente en el script que hemos creado con anterioridad: 


También se puede comprobar desde un cliente en la misma subred accediendo al dominio desde el navegador.


<img width="724" height="155" alt="image" src="https://github.com/user-attachments/assets/8151b336-96d6-422a-b972-a4146b66cefb" />

Creamos un nuevo usuario y lo comprobamos: 

<img width="709" height="301" alt="image" src="https://github.com/user-attachments/assets/17a30308-cee3-4fc3-aa84-0bb93c6ccfa9" />

Ahora lo comprobaremos desde un cliente en la misma subred:

<img width="721" height="171" alt="image" src="https://github.com/user-attachments/assets/e1673d07-5399-458e-bd40-705d346fff24" />

Posteriormente vamos al navegador a ver las páginas que hemos escrito: 

<img width="719" height="194" alt="image" src="https://github.com/user-attachments/assets/02537677-6574-4432-9cb7-c2c87500bdfa" />


<img width="721" height="104" alt="image" src="https://github.com/user-attachments/assets/f27e3e19-bdd0-4ffa-bb39-e557bbc42643" />

---

## 5. Docker

El servidor ya tiene los puertos **80** (Apache) y **53** (Bind9) ocupados. Para evitar conflictos, los contenedores Docker se configuran en puertos alternativos:

- **Apache en Docker**: puerto `8080`
- **Bind9 en Docker**: puerto `5353`

### Instalación de Docker y Docker Compose

```bash
sudo apt install docker.io docker-compose-plugin -y
sudo usermod -aG docker $USER
```

<img width="715" height="205" alt="image" src="https://github.com/user-attachments/assets/614370d2-28eb-461f-a723-7c9bf1cc8747" />


### Estructura de directorios

```
~/docker-project/
├── html/
│   └── index.html
└── docker-compose.yml
```

### Archivo docker-compose.yml

```yaml
services:
  web:
    image: httpd:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/local/apache2/htdocs

  dns:
    image: internetsystemsconsortium/bind9:9.18
    ports:
      - "5353:53/udp"
      - "5353:53/tcp"
    volumes:
      - ./bind:/etc/bind
```


<img width="646" height="310" alt="image" src="https://github.com/user-attachments/assets/5fb1763e-acf0-4d88-9a58-fca35e404497" />


### Script de arranque automático (`arranca_docker.sh`)

```bash
#!/bin/bash
cd ~/docker-project
docker compose up -d
echo "Contenedores levantados."
echo "Web disponible en: http://<IP>:8080"
```

<img width="715" height="283" alt="image" src="https://github.com/user-attachments/assets/f76a9909-6ff3-44e1-8cb1-a6e1045d6b9a" />

```bash
chmod +x arranca_docker.sh
./arranca_docker.sh
```

<img width="703" height="52" alt="image" src="https://github.com/user-attachments/assets/260a06a7-2d0b-4f83-966f-d4b74ae2485b" />


### Comprobación desde cliente

Desde cualquier equipo en la misma subred, acceder en el navegador a:

```
http://<IP_SERVIDOR>:8080
```

<img width="717" height="161" alt="image" src="https://github.com/user-attachments/assets/ca2684e0-05d2-4d53-b972-aa4dc6ce84a1" />

---

## Resumen de servicios y puertos

| Servicio | Puerto |
|---|---|
| Apache (host) | 80 |
| Apache (Docker) | 8080 |
| Bind9 (host) | 53 |
| Bind9 (Docker) | 5353 |
| MariaDB | 3306 |
| vsftpd (FTPS) | 21 |
| SSH | 22 |
