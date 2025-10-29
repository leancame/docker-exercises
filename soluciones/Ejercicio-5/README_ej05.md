# Ejercicio 5 - Gestión de volúmenes en un Contenedor NGINX

## Objetivo
El objetivo de este ejercicio es que los estudiantes aprendan a utilizar Docker para crear un contenedor que sirva archivos web mediante NGINX, explorando la gestión de volúmenes para permitir la sincronización de archivos entre el sistema host y el contenedor, de modo que los cambios realizados en el archivo index.html se reflejen automáticamente en el servidor web sin necesidad de reiniciar el contenedor.

## Consideraciones
 1. En la carpeta `soluciones` se creará una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-5`.
 2. En esa carpeta se dejará el dockerfile creado y en un archivo llamado `README_ej05.md` con los comandos utilizados con sus salidas por pantalla.

## Tarea
1. Crea un Dockerfile que use una imagen base de NGINX para crear un contenedor que sirva archivos web.
    ```bash
    # Usar la imagen base de NGINX
    FROM nginx

    # Exponer el puerto 80
    EXPOSE 80
    ```
    Un Dockerfile simple que usa la imagen y aporta un puerto usado por `NGINX`.

2. Crear un fichero index.html. El contenedor debe compartir con tu maquina local la carpeta donde se encuentra el fichero index.html.

    ```bash
        <!DOCTYPE html>
            <html lang="es">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>Mi Página Web</title>
                </head>
                <body>
                    <h1>¡Hola, mundo!</h1>
                    <p>Esta es mi página web servida por NGINX en un contenedor Docker por Leandro Carbajo Méndez.</p>
                </body>
            </html>
    ```

    Cuando ya poseemos los dos archivos, tanto el `Dockerfile` y el `index.html`, pasamos a crear la imagen y el contenedor correspondiente.

    La imagen la desarrollamos con el comando `build -t` para darle un nombre:

    ```bash
    docker build -t nginx_lcm .
    ```

    ![Captura sobre el código](../../datos/Ejercicio05/imagen%20build.png)

    Cuando desplegemos el `index.html` asignaremos el nombre con `--name`, con el `-v` montaremos un volumen siendo `${PWD}` el directorio actual del host y la ruta `/usr/share/nginx/html`, el puerto lo daremos con `-p` y por último `-d` ejecutando en segundo plano. Finalizamos con el nombre de la imagen. 

    ```bash
    docker run --name nginx_lcm -v "${PWD}:/usr/share/nginx/html" -p 8080:80 -d nginx_lcm
    ```
    ![Captura sobre el código](../../datos/Ejercicio05/ejecutar%20imagen%20y%20contenedor.png)
    
3. Cualquier cambio realizado en el archivo index.html , tanto desde dentro de la carpeta en tu máquina local como desde dentro del contenedor, debe reflejarse automáticamente en el servidor web del contenedor. Editar el archivo de ambas formas y verificar.

    Mostramos el index en el navegador:

    ![Captura sobre el código](../../datos/Ejercicio05/ejecucion%201.png)

    Lo modificamos por el visual añadiendo una nueva frase en el archvio index.html y mostramos el index en el navegador:

    ![Captura sobre el código](../../datos/Ejercicio05/ejecucion%202%20modificada%20de%20visual.png)

    Para modificarlo desde el contenedor, primero debemos adrentarnos en este con el siguiente comando:

    ```bash
        docker exec -it nginx_lcm /bin/bash
    ```
    Con el `exec` ejecutamos el contenedor, mientras que `-it` permite interactuar con el contenedor como si estuvieras usando una terminal normal. Añadimos el nombre del contenedor y finalizando utilizando `/bin/bash` pudiendo usar comandos en la terminal del propio contenedor. En esta terminal usamos el comando `echo "frase deseada" >> ruta (/usr/share/nginx/html/index.html)` para agregar una frase al final del todo. 

    ![Captura sobre el código](../../datos/Ejercicio05/contenedor%20frase.png)

    ![Captura sobre el código](../../datos/Ejercicio05/ejecucion%203%20modificada%20de%20contenedor.png)

    

   