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
2. Modificar el Dockerfile anterior para que la pausa por 10 segundos se haga con una instrucción CMD. Generar la imagen y el contenedor.
3. ¿Cuál fue la diferencia más notoria entre ambos casos?
4. Crear un Dockerfile que cree una imagen en base al proyecto django (Python) que se encuentra en datos/Ejercicio06. Levantar el contenedor y verificar que funcione.
5. Crear un Dockerfile que use una imagen base de Python y copie el archivo "hello.py" dentro. Generar la imagen. Debe ejecutar el fichero "hello.py", corriendo el contenedor de Python. (Ayuda: usar instrucción Entrypoint)
6. ¿Qué diferencias hay entre las instrucciones finales (RUN/CMD/Entrypoint)?
