# Usar la imagen base de Ubuntu
FROM ubuntu:latest

# Establecer el directorio de trabajo
WORKDIR /app

# Crear un usuario con UID 1500
RUN useradd -m -u 1500 Lean

# Copiar el script de shell al contenedor
COPY mensaje.sh .

# Cambiar temporalmente al usuario root para establecer permisos
RUN chmod 744 mensaje.sh

# Cambiar al usuario creado
USER Lean

# Dormir el contenedor para mantenerlo activo
ENTRYPOINT ["sleep", "infinity"]