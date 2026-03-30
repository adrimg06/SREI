# Activity #8 - Subdominios

## 1. Declarar la Zona Principal

Para empezar, declaramos la zona principal accediendo a la siguiente ruta:

<img width="781" height="54" alt="image" src="https://github.com/user-attachments/assets/927cd54e-c555-403f-80e5-b225eb2cc507" />


Como podemos ver, ya la teníamos configurada de la práctica anterior, así que dejamos el archivo como estaba:

<img width="611" height="306" alt="image" src="https://github.com/user-attachments/assets/350916a4-ed5e-42e0-87b2-ea78127e0c46" />



---

## 2. Definir Hosts y Subdominios

Una vez hecho lo anterior, pasamos a definir los hosts del dominio principal junto con los subdominios. Creamos el siguiente archivo con su ruta correspondiente:
 
 <img width="781" height="66" alt="image" src="https://github.com/user-attachments/assets/7885c9d9-f9ac-4703-935e-2a9dcb77da63" />



Añadimos la siguiente configuración al archivo creado:

<img width="781" height="347" alt="image" src="https://github.com/user-attachments/assets/85a6d90d-e66a-461d-9f52-db1d3e24c521" />


---

## 3. Verificación y Pruebas

### Comprobación de sintaxis

Comprobamos que la sintaxis es correcta. Como podemos ver, no hay errores:
```bash
sudo named-checkconf
```
<img width="785" height="54" alt="image" src="https://github.com/user-attachments/assets/8aca6f4c-6b99-4cfc-bbdf-e3aa0dc7a443" />


### Validación de zona

Validamos la zona con un `checkzone`:
```bash
sudo named-checkzone
```
<img width="780" height="83" alt="image" src="https://github.com/user-attachments/assets/196dbe36-b78c-4ef6-8e9f-e64f252f389e" />


### Reinicio del servicio

Como todo está correcto, reiniciamos el servicio:
```bash
sudo systemctl restart bind9
```
<img width="784" height="70" alt="image" src="https://github.com/user-attachments/assets/ba367d3c-b59d-40f9-a080-eaf098780e88" />


---

## 4. Verificación con dig

Utilizamos `dig` para verificar que los dos niveles de dominio se resuelven correctamente:
```bash
dig dominio.com
dig subdominio.dominio.com
```

<img width="782" height="216" alt="image" src="https://github.com/user-attachments/assets/3475951c-6e44-4860-bcfe-3e40258338ed" />

<img width="782" height="303" alt="image" src="https://github.com/user-attachments/assets/93a95c52-4c33-4d0e-851a-13551c161e7d" />

---

## 5. Configuración de nsswitch.conf

Pasamos a la configuración del archivo `nsswitch.conf`, el cual se encarga de definir las fuentes de búsqueda para los servicios instalados en el servidor.

La verificación la realizamos con `dig` en lugar de `ping`, ya que `ping` no funciona en este caso por ser **Multicast DNS**. Para arreglarlo, ejecutamos el siguiente comando:

<img width="782" height="113" alt="image" src="https://github.com/user-attachments/assets/e5eddd81-75c6-4f3a-9a8d-1dcc9319a6b0" />

