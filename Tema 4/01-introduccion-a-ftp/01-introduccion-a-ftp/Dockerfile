FROM alpine:latest

# Instalación de proftpd
RUN apk update && \
    apk add --no-cache proftpd

# Crear usuario ftpuser con home y shell bloqueado
RUN adduser -D -h /home/ftpuser -s /bin/false ftpuser && \
    echo "ftpuser:ftpuser" | chpasswd && \
    chown -R ftpuser:ftpuser /home/ftpuser

# Crear directorios necesarios para proftpd y asignar permisos
RUN mkdir -p /run/proftpd /var/run/proftpd /var/log/proftpd && \
    chmod 755 /run/proftpd /var/run/proftpd

# Copiar archivo de configuración
COPY ./ftp/conf/proftpd.conf /etc/proftpd/proftpd.conf

# Puertos de FTP y FTP PASIVO
EXPOSE 21
EXPOSE 21000-21010

# Ejecutar proftpd en modo no-daemon
CMD ["proftpd", "-n"]
