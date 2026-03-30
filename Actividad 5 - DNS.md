# Actividad 5 - DNS

## 1. Instalación de Bind9

Primero instalaremos **bind9** en la máquina de AWS.
<img width="603" height="77" alt="image" src="https://github.com/user-attachments/assets/4e358eaa-7ed9-43a1-882a-24d65abdebd7" />

---

## 2. Configuración como Servidor Caché

Una vez instalado, configuramos el servidor como **servidor caché** accediendo a los archivos de configuración de Bind.

Añadimos lo siguiente en el bloque `options`:
```bash
<img width="603" height="15" alt="image" src="https://github.com/user-attachments/assets/aa57cc00-daef-46e6-a75e-bbc22233e0e2" />

```

---

## 3. Configuración como Servidor Forwarding

Configuramos el servidor como **forwarding** añadiendo lo siguiente en el mismo archivo de configuración.

Descomentamos la sección correspondiente y escribimos:
```bash
<img width="243" height="80" alt="image" src="https://github.com/user-attachments/assets/7ae879bd-ca67-4010-b774-ba571de99faf" />
```

El resultado debería quedar así:
```bash
<img width="605" height="484" alt="image" src="https://github.com/user-attachments/assets/fafeede0-f5eb-4a77-b4e5-850159f52186" />
```

---

## 4. Verificación y Logs

### Solución de errores

Al realizar la verificación, aparecieron un par de errores que se solucionaron reescribiendo la configuración:
```bash
<img width="439" height="368" alt="image" src="https://github.com/user-attachments/assets/26fe0fd9-4ada-4410-ae9d-6f513545d855" />

```

### Comprobación sin errores

Comprobamos que la configuración no devuelve ningún error:
```bash
<img width="603" height="38" alt="image" src="https://github.com/user-attachments/assets/837a5e5e-3298-40bf-9c21-dadaa505c002" />
```

### Reinicio del servicio

Reiniciamos el servicio y comprobamos que está levantado:
```bash
sudo systemctl restart bind9
sudo systemctl status bind9
```
```bash
<img width="600" height="147" alt="image" src="https://github.com/user-attachments/assets/956d6da6-d03e-4712-9786-5a44f902f28a" />

```

---

## 5. Revisión de Logs

Hacemos un `tail` para mostrar los últimos logs del servicio:
```bash
sudo tail -f /var/log/syslog
```
```bash
<img width="780" height="151" alt="image" src="https://github.com/user-attachments/assets/11e4e041-6d5c-44e2-b437-941bf9863928" />

```

---

## 6. Prueba Final

Por último, realizamos la **prueba de fuego** con un `dig` para verificar que el servidor responde correctamente:
```bash
dig @localhost google.com
```
```bash
<img width="783" height="505" alt="image" src="https://github.com/user-attachments/assets/a11e64b6-cd8c-4965-8c9c-8eb8dc6efb35" />

```
