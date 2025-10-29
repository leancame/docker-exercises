# Ejercicio 7 - Gestión de permisos y usuarios

## Objetivo
El objetivo de este ejercicio es que los estudiantes aprendan a gestionar permisos y usuarios en un contenedor de Docker, creando un script que imprime un mensaje y configurando los permisos adecuados para el script y el usuario que lo ejecuta, lo que les permitirá comprender la importancia de la seguridad y el control de acceso en entornos de contenedores.

## Consideraciones
 1. En la carpeta `soluciones` se creará una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-7`.
 2. En esa carpeta se dejará el dockerfile creado y en un archivo txt llamado `README_ej07.md` con los comandos utilizados con sus salidas por pantalla.

## Tarea
1. Crea un shell script que imprima un mensaje por consola. 

    ```bash
        #!/bin/bash

        # Imprimir un mensaje por consola
        echo "¡Hola, mi nombre es Leandro Carbajo Méndez nakamas!"
    ```

2. Crea un Dockerfile con una imagen base de ubuntu, donde se copie el shell script creado y lo ejecute (al levantar el contenedor). y asegúrate de que los permisos del script se establezcan en lectura, escritura y ejecución para el usuario root, y solo lectura para otros.

    ```bash
    # Usar la imagen base de Ubuntu
    FROM ubuntu:latest

    # Establecer el directorio de trabajo
    WORKDIR /app

    # Copiar el script de shell al contenedor
    COPY mensaje.sh .

    # Establecer permisos: lectura, escritura y ejecución para root; solo lectura para otros
    RUN chmod 744 mensaje.sh

    # Ejecutar el script al iniciar el contenedor
    CMD ["./mensaje.sh"]
    ```
    
    En este Dockerfile añadimos en el `RUN` los permisos oportunos solicitados `744` (todos para root y lectura para el resto).   

3. Crea la imagen y levanta el contenedor. Comprueba que funciona.

    Usaremos los comandos claves `built` y `run` de docker, concretando:

    ```bash
    docker built -t ubuntu_lcm .
    ```
    ```bash
    docker run --name contenedor_ubuntu_lcm ubuntu_lcm
    ```

    ![Captura sobre el código](../../datos/Ejercicio07/apartado%202.png)


4. Crea un usuario con UID 1500 (y nombre a tu elección) en el Dockerfile. Cambia el usuario bajo el cual se ejecutarán los siguientes comandos, al usuario creado.

    ```bash
    # Usar la imagen base de Ubuntu
    FROM ubuntu:latest

    # Establecer el directorio de trabajo
    WORKDIR /app

    # Crear un usuario con UID 1500
    RUN useradd -m -u 1500 Lean

    # Copiar el script de shell al contenedor
    COPY mensaje.sh .

    # Establecer permisos: lectura, escritura y ejecución para root; solo lectura para otros
    RUN chmod 744 mensaje.sh

    # Cambiar al usuario creado
    USER Lean

    # Ejecutar el script al iniciar el contenedor
    CMD ["sh", "-c", "./mensaje.sh"]
    ```
    En este Dockerfile añadimos en el `CMD` la ejecución  del script con el usuario `Lean` (el creado en el `RUN` anterior). 

5. Crea la nueva imagen y levanta el nuevo contenedor. ¿Qué ha ocurrido?

    El principal suceso es que no nos va a permitir acceder al archivo sh al no tener los permisos necesarios por parte del usuario dado ya que el usuario creado no tiene permisos de ejecución para el archivo cocretamente. Por lo tanto, el contenedor no se levanta.

    ![Captura sobre el código](../../datos/Ejercicio07/apartado%20erroneo.png)


6. Ingresa al contenedor. Corrobora que el usuario es el que has creado. Ahora, comprueba si es posible cambiar de usuario a root. ¿Qué ha pasado?

    Para poder entrar al contenedor, debemos realizar un nuevo Dockerfile ya que el anterior no inicia el contenedor muriéndose al momento. En este Dockerfile he usado el comando `ENNTRYPOINT` añadiendo `sleep infinity` para poder dejar el contenedor durmiendo e ingresar en este.  

    ```bash
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
    ``` 

    ![Captura sobre el código](../../datos/Ejercicio07/apartado%20sleep.png)

    Tras esto creamos la imagen y levantamos el contenedor, intentando posteriormente introducirnos en este con el comando `exec`.

    ![Captura sobre el código](../../datos/Ejercicio07/ir%20a%20root.png)

    Al entrar buscamos cual es nuestro usuario actual con `whoami` e intentamos ir a root con `su -` pidiendo una contraseña que desconocemos lo que significa el fallo en la autentificación. Por lo tanto, no podemos cambiar a root.

7. Reflexiona sobre lo siguiente: si logras acceder como root, ¿qué problemas o riesgos podrían surgir al permitir accesos con privilegios elevados? Si no logras acceder como root, ¿qué beneficios tiene esta restricción desde el punto de vista de la seguridad y estabilidad del contenedor?

    Si damos los privilegios de primeras nos aportará una gran exposición a vulnerabilidades, ya que podremos modificar lo que queramos además que si se da un acceso no autorizado y consiguen el usuario root significa comprometer todos nuestros datos. Las modificaciones que haga el root puede crear confictos con el propio contenedor y modificaciones no controladas. Restringir los permisos nos ayuda a acotar las posibles filtraciones o daños en caso de posibles ataques al reducir el acceso aportando estabilidad al sistema, luego nos permite porteger la integridad de datos al no permitir a los usuarios a hacer cosas no deseadas como borrar datos por ejemplo.

8. Adjunta capturas del desarrollo y resultado final del ejercicio.