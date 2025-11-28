# HTTPS en el servidor web Apache
### Investigación
  1. Funcionamiento del protocolo HTTPS y su importancia en la seguridad web
  2. Tipos de certificados SSL/TLS (autofirmado vs. CA confiable)
  3. Módulos de Apache2 necesarios para habilitar SSL/TLS en Ubuntu

### Ejecución técnica
  1. Instalamos y verificamos el estado de Apache2 en Ubuntu. En mi caso como ya estaba instalado, muestro solo el estado:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/1.png)
  2. Habilitamos los módulos SSL y headers mediante los comandos `sudo a2enmod ssl`, `sudo a2enmod headers` y `sudo systemctl restart apache2`:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/2.png)
  3. Generamos un certificado SSL/TLS que en mi caso será autofirmado. Primero, creamos un directorio para los certificados con el comando `sudo mkdir -p /etc/apache2/ssl` y después generamos el certificado y la clave primaria mediante el comando `sudo openssl req -x509 -nodes -days 365 \ -newkey rsa:2048 \ -keyout /etc/apache2/ssl/mi_certificado.key \ -out /etc/apache2/ssl mi_certificado.crt`. El parámetro más importante es Common Name (CN), que debe ser nuestro dominio o IP:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/3.1.1.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/3.1.2.png)
  4. Configuramos un VirtualHost para escuchar en el puerto 443 usando HTTPS. Como estamos usando un certificado autofirmado, debemos crear o editar un archivo como `sudo nano /etc/apache2/sites-available/mi-sitio-ssl.conf` (El contenido del mismo se muestra en la captura). Después habilitamos el sitio mediante los comandos `sudo a2ensite mi-sitio-ssl.conf` y `sudo systemctl reload apache2`:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/4.1.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/4.2.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/4.3.png)
  5. Adaptamos las directivas necesarias para redireccionar HTTP a HTTPS. Editamos el VirtualHost del puerto 80 con el comando `sudo nano /etc/apache2/sites-available/mi-sitio.conf` y agregamos dentro de <VirtualHost *:80> `ServerName midominio` y `Redirect permanent / https://midominio/`. Finalmente activamos el sitio si no lo está ya con `sudo a2ensite mi-sitio.conf` y `sudo systemctl reload apache2`:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/5.1.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/5.2.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/5.3.png)
  6. Por último, reiniciamos Apache mediante el comando `sudo systemctl restart apache2` y validamos la correcta implementación desde el navegador con `https://tu-dominio.com`. Al haber trabajado con un certificado autofirmado, veremos una advertencia que nos impide el acceso en un principio pero pulsando en "Aceptar el riesgo y continuar", podremos avanzar:
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/6.1.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/6.2.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/6.3.png)
    ![](https://github.com/JavierMoralesSimon/apacheHttps/blob/main/Capturas/6.4.png)
