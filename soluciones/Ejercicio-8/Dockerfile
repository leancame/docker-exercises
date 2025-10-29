# Definir el argumento para la versión de Ubuntu
ARG VERSION=latest

# Usar una imagen base de Ubuntu
FROM ubuntu:${VERSION}

# Definir una variable de entorno
ENV ESCUDO="Raimon"

# Establecer el directorio de trabajo
WORKDIR /app

# Recibir un argumento para el paquete a instalar
ARG PACKAGE

# Instalar el paquete especificado
RUN apt-get update && apt-get install -y ${PACKAGE}

# Comando por defecto
CMD ["bash"]