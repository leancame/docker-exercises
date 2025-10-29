# Ejercicio 6 - Instrucciones RUN, CMD y Entrypoint

## Objetivos
- Practicar el uso de RUN, CMD y Entrypoint.
- Reconocer las diferencias.
- Probar diferentes usos.

## Consideraciones
 1. En la carpeta `soluciones` se creará una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-6`.
 2. En esa carpeta se dejará el dockerfile creado y en un archivo llamado `README_ej06.md` con los comandos utilizados con sus salidas por pantalla.

## Tarea
1. Crear un Dockerfile que corra una instrucción RUN que pause la ejecución por 10 segundos. Generar la imagen y el contenedor.

    ```bash
    # Usar una imagen base de Ubuntu
    FROM ubuntu:latest

    # Ejecutar una instrucción que pause la ejecución por 10 segundos
    RUN sleep 10

    # Comando por defecto
    CMD ["echo", "La ejecución se ha pausado por 10 segundos"]

    ```
    ![Captura sobre el código](../../datos/Ejercicio06/apartado%201.png)

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%201-1.png)

    Usamos los comandos que hemos ido realizando en los demás ejercicios con el `build` y el `run`, y como observamos en la construcción de la imagen existe un `RUN sleep 10` dando una espera de 10 segundos. Si es verdad que añadí una frase en el `CMD`, pero es algo secundario que no afecta al caso.

2. Modificar el Dockerfile anterior para que la pausa por 10 segundos se haga con una instrucción CMD. Generar la imagen y el contenedor.

    ```bash
    # Usar una imagen base de Ubuntu
    FROM ubuntu:latest

    # Comando por defecto que pausa la ejecución por 10 segundos
    CMD ["sleep", "10"]
    ```

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%202.png)

    Al hacer lo mismo, pero añadiendo la espera en el `CMD` se da esta en la ejecución del contenedor afectando al comando `run` y por tanto no en la construcción de la imagen.

3. ¿Cuál fue la diferencia más notoria entre ambos casos?
    
    Cuando usamos `RUN` esta se ejecuta durante la construcción de la imagen siendo solo una vez y sin afectar a la ejecución del contenedor. El `CMD` se ejecuta cada vez que iniciamos el contenedor por lo que la espera será cada vez que lo ejecutamos.

4. Crear un Dockerfile que cree una imagen en base al proyecto django (Python) que se encuentra en datos/Ejercicio06. Levantar el contenedor y verificar que funcione.

    ```bash
    # Usar una imagen base de Python
    FROM python:3.9-slim

    # Establecer el directorio de trabajo en el contenedor
    WORKDIR /app

    # Copiar los archivos de requisitos
    COPY requirements.txt .

    # Instalar las dependencias
    RUN pip install --no-cache-dir -r requirements.txt

    # Copiar el resto de los archivos del proyecto
    COPY . .

    # Exponer el puerto 8000
    EXPOSE 8000

    # Comando por defecto para ejecutar el servidor de desarrollo de Django
    CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
    ```
    Seguimos con el comando `build` y `run` para crear la imagen y levantar el contendor. En este supuesto del contenedor hemos añadido también el `--name` para el nombre, `-p` para indicar los puertos y `-d` para la ejecución en segundo plano.

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%204.png)

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%204-1.png)

    Mostramos el resultado:

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%204-2.png)

5. Crear un Dockerfile que use una imagen base de Python y copie el archivo "hello.py" dentro. Generar la imagen. Debe ejecutar el fichero "hello.py", corriendo el contenedor de Python. (Ayuda: usar instrucción Entrypoint)

    ```bash
    # Usar una imagen base de Python
    FROM python:3.9-slim

    # Establecer el directorio de trabajo en el contenedor
    WORKDIR /app

    # Copiar el archivo hello.py al contenedor
    COPY hello.py .

    # Usar ENTRYPOINT para ejecutar el script hello.py
    ENTRYPOINT ["python", "hello.py"]
    ```

    Al usar `ENTRYPOINT` hacemos que se ejecute el archivo `hello.py` cada vez ejecutemos el contenedor mostrando el contenido de este.

    Realizando los comandos de creación de imagen y levantar el contenedor observamos el resultado:

    ```bash
    docker build -t hello-python-lcm .
    ```
    ```bash
    docker run --name hello-python-container hello-python-lcm
    ```

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%205.png)

    ![Captura sobre el código](../../datos/Ejercicio06/apartado%205-2.png)

6. ¿Qué diferencias hay entre las instrucciones finales (RUN/CMD/Entrypoint)?

    Como aporté en el apartado 3, `RUN` afecta a la construcción de la imagen no afectando en ningún momento a la ejecución del contenedor. En el caso contrario, `CMD` y `ENTRYPOINT` afectan a la ejecución del contenedor, sin embargo, `CMD` es un comando por defecto que puede ser sobrescrito y `ENTRYPOINT` suele cumplirse siempre por lo que no se tiende a sobrescribir.


