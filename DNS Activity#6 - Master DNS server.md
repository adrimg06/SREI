# DNS Activity #6 - Master DNS Server

## 1. Configuración de Zonas

Para empezar, editaremos el archivo que define las zonas:

<img width="782" height="53" alt="image" src="https://github.com/user-attachments/assets/0052b2a7-4486-445a-9f8c-e127f6a05cbe" />


Creamos una zona inversa y una zona directa:

<img width="566" height="303" alt="image" src="https://github.com/user-attachments/assets/18179577-559c-46b0-b76c-c5491d44ea7d" />

---

## 2. Crear el Fichero de Zona Directa

Creamos el archivo de la zona directa:
<img width="782" height="105" alt="image" src="https://github.com/user-attachments/assets/d1d5b27f-d392-4516-96ae-b9673117e68f" />


Pegamos el siguiente contenido dentro del archivo:

<img width="608" height="257" alt="image" src="https://github.com/user-attachments/assets/dadd5241-a91b-45e5-a94c-3c96d580c4f9" />


---

## 3. Crear el Fichero de Zona Inversa

Creamos el fichero de zona inversa:

<img width="780" height="135" alt="image" src="https://github.com/user-attachments/assets/7fc3fea6-29ce-493e-a52a-05a7f08abae0" />


Metemos el siguiente contenido dentro del archivo:

<img width="783" height="250" alt="image" src="https://github.com/user-attachments/assets/b9e6e838-9d65-4255-aaf1-581efc07a2c5" />


---

## 4. Verificación y Pruebas

### Checkpoint de configuración

Hacemos el checkpoint de configuración:

<img width="772" height="79" alt="image" src="https://github.com/user-attachments/assets/4033d706-8504-4893-8ed8-38cacfe7732d" />


### Check de las zonas

Hacemos el check de las zonas:
```bash
sudo named-checkzone
```
<img width="778" height="88" alt="image" src="https://github.com/user-attachments/assets/ebd223f9-5585-4557-b857-f257a00666c5" />

<img width="782" height="61" alt="image" src="https://github.com/user-attachments/assets/4b3fe1ef-1278-4680-99fd-87765c137dc2" />


### Reinicio del servicio

Hacemos un restart:
```bash
sudo systemctl restart bind9
```
<img width="785" height="63" alt="image" src="https://github.com/user-attachments/assets/8297c3f4-3013-4686-8ab3-ad14dd12a44f" />


### Comprobación de registros

Comprobamos los registros:

<img width="782" height="291" alt="image" src="https://github.com/user-attachments/assets/5e623813-1e12-487d-a079-90d5c94318c0" />

<img width="785" height="345" alt="image" src="https://github.com/user-attachments/assets/b7102d59-b12a-4a69-9ef7-5786af4b5564" />

---

## 5. Configuración del Cliente

Para poder utilizar el servidor DNS, editaremos el siguiente archivo:
```bash
sudo nano /etc/resolv.conf
```
<img width="782" height="36" alt="image" src="https://github.com/user-attachments/assets/77a93297-4052-412f-9de6-59af45c90757" />


Cambiamos la línea de `nameserver` apuntando a nuestro servidor:
```bash
nameserver <IP_del_servidor>
```
<img width="782" height="398" alt="image" src="https://github.com/user-attachments/assets/7c744e0a-0299-41c4-b67d-b5e9aca57e81" />
