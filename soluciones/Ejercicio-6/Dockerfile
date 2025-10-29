# Usar una imagen base de Python
FROM python:3.9-slim

# Establecer el directorio de trabajo en el contenedor
WORKDIR /app

# Copiar el archivo hello.py al contenedor
COPY hello.py .

# Usar ENTRYPOINT para ejecutar el script hello.py
ENTRYPOINT ["python", "hello.py"]