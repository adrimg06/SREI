# Actividad 5 - DNS

## 1. Instalación de Bind9

Primero instalaremos **bind9** en la máquina de AWS.

---

## 2. Configuración como Servidor Caché

Una vez instalado, configuramos el servidor como **servidor caché** accediendo a los archivos de configuración de Bind.

Añadimos lo siguiente en el bloque `options`:
```bash
# [captura de pantalla]
```

---

## 3. Configuración como Servidor Forwarding

Configuramos el servidor como **forwarding** añadiendo lo siguiente en el mismo archivo de configuración.

Descomentamos la sección correspondiente y escribimos:
```bash
# [captura de pantalla]
```

El resultado debería quedar así:
```bash
# [captura de pantalla del archivo completo]
```

---

## 4. Verificación y Logs

### Solución de errores

Al realizar la verificación, aparecieron un par de errores que se solucionaron reescribiendo la configuración:
```bash
# [captura de pantalla del error y solución]
```

### Comprobación sin errores

Comprobamos que la configuración no devuelve ningún error:
```bash
# [captura de pantalla]
```

### Reinicio del servicio

Reiniciamos el servicio y comprobamos que está levantado:
```bash
sudo systemctl restart bind9
sudo systemctl status bind9
```
```bash
# [captura de pantalla]
```

---

## 5. Revisión de Logs

Hacemos un `tail` para mostrar los últimos logs del servicio:
```bash
sudo tail -f /var/log/syslog
```
```bash
# [captura de pantalla]
```

---

## 6. Prueba Final

Por último, realizamos la **prueba de fuego** con un `dig` para verificar que el servidor responde correctamente:
```bash
dig @localhost google.com
```
```bash
# [captura de pantalla del resultado]
```
