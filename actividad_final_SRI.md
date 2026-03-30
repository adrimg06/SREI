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
- Se configura la base de datos de phpMyAdmin y se le asigna una contraseña.

### Verificación de servicios

```bash
# Apache
sudo systemctl status apache2

# MariaDB
sudo systemctl status mariadb

# FTP
sudo systemctl status vsftpd

# DNS
sudo systemctl status bind9
```

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

Después se edita el archivo de configuración de vsftpd (`/etc/vsftpd.conf`):

- Se descomenta `write_enable=YES` para permitir subida de archivos.
- Se añade la configuración TLS apuntando a los certificados generados.

Se guarda el archivo y se reinicia el servicio. Para verificar que el certificado funciona:

```bash
openssl s_client -connect 127.0.0.1:21 -starttls ftp
```

---

### 3.2 Preparar las zonas del DNS (Bind9)

El dominio principal configurado es: `dominioadrian.local`

Se declaran las zonas en el archivo de configuración de Bind9 y se crean los archivos de zona directa e inversa.

**Zona directa** (`/etc/bind/db.dominioadrian.local`): traduce nombres de dominio a IPs.

**Zona inversa** (`/etc/bind/db.4`): traduce IPs a nombres de dominio.

Tras configurar ambas zonas se reinicia Bind9 y se comprueba con:

```bash
dig dominioadrian.local
```

---

### 3.3 Habilitar Python en Apache

El módulo `libapache2-mod-wsgi-py3` ya fue instalado previamente. Solo hay que habilitarlo:

```bash
sudo a2enmod wsgi
sudo systemctl restart apache2
```

Se verifica que el módulo está activo consultando los módulos cargados en Apache.

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

**Probar la app Python:**

```bash
curl http://nerea.dominioadrian.local/python
```

También se puede comprobar desde un cliente en la misma subred accediendo al dominio desde el navegador.

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

### Script de arranque automático (`arranca_docker.sh`)

```bash
#!/bin/bash
cd ~/docker-project
docker compose up -d
echo "Contenedores levantados."
echo "Web disponible en: http://<IP>:8080"
```

```bash
chmod +x arranca_docker.sh
./arranca_docker.sh
```

### Comprobación desde cliente

Desde cualquier equipo en la misma subred, acceder en el navegador a:

```
http://<IP_SERVIDOR>:8080
```

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
