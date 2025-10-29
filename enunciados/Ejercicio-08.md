# Ejercicio 8 - Dockerfile con ARG y ENV

## Objetivos

Aprender a utilizar las instrucciones `ARG` y `ENV` en un `Dockerfile` para configurar una imagen de Docker y gestionar variables de entorno y argumentos en el momento de la construcción.

## Consideraciones

En la carpeta `soluciones` se creará una carpeta con el siguiente formato `<vuestro nombre>-Ejercicio-8`, donde se incluirán el `Dockerfile`, capturas del proceso de construcción y verificación, y un archivo `README_ej08.md` con las explicaciones de los pasos realizados.

## Tarea

**Instrucciones a seguir para crear el `Dockerfile`:**

   - Definir una variable de entorno utilizando `ENV`, la cual será accesible dentro del contenedor en tiempo de ejecución.
   - Utilizar la instrucción `ARG` para recibir un argumento en el momento de la construcción de la imagen. Este argumento permitirá la instalación de un paquete (a elección) en el contenedor.
   - Crear la imagen y el contenedor. Verificar que la variable de entorno esté disponible y que el paquete haya sido instalado. Adjuntar capturas de todo el proceso.