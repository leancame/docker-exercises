# Ejercicio 10 - Docker-compose

## Objetivos
- Creación de contenedores a través de un docker-compose.
- Manejo de redes y volúmenes en un docker-compose.
- DNS en contenedores.

## Consideraciones

En la carpeta `soluciones` se creará una carpeta con el siguiente formato `<vuestro nombre>-Ejercicio-10`, donde se incluirán los archivos generados, capturas del proceso de construcción y verificación, y un archivo `README_ej10.md` con las explicaciones de los pasos realizados.

## Tarea
Volver al proyecto dado de ejemplo para el Ejercicio 4. Ejecutarlo nuevamente, pero ahora aplicando todo lo aprendido sobre docker-compose. En cuanto al frontend, usar la imagen en la que se hizo multistage. Hacer que las imágenes se creen en el momento de ejecutar el docker-compose. Prestar atención a volúmenes y redes, si fuera necesario crearlos. 
- Ambos contenedores, para comunicarse entre sí, ¿usan el puerto interno propio de la red o el puerto desde el que nosotros accedemos a ellos desde nuestra PC?
- ¿Qué otro valor (más humanamente reconocible y de carácter permanente) puede ser usado en lugar de las IPs internas de los contenedores a la hora de comunicarlos entre sí?