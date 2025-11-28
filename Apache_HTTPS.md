# HTTPS en el servidor web Apache
### Investigación
  1. Funcionamiento del protocolo HTTPS y su importancia en la seguridad web
  2. Tipos de certificados SSL/TLS (autofirmado vs. CA confiable)
  3. Módulos de Apache2 necesarios para habilitar SSL/TLS en Ubuntu

### Ejecución técnica
  1. Instalamos y verificamos el estado de Apache2 en Ubuntu. En mi caso como ya estaba instalado, muestro solo el estado:
     ![]()
  3. Habilitar los módulos SSL y headers.
  4. Generar un certificado autofirmado SSL/TLS
  5. Configurar un VirtualHost para escuchar en el puerto 443 usando HTTPS.
  6. Adaptar las directivas necesarias para redirección HTTP → HTTPS (opcional pero recomendado).
  7. Reiniciar/recargar Apache y validar la correcta implementación mediante navegador o curl.
