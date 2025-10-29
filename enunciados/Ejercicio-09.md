# Ejercicio 9 - Multistage

## Objetivos
- Entendimiento de qué es Multistage.
- Creación del primer Multistage.
- Comparación en el consumo de recursos de un contenedor con y sin Multistage.

## Consideraciones
 Multistage permite crear imágenes optimizadas y más pequeñas al dividir el proceso de construcción de imágenes en varias etapas dentro de un solo Dockerfile. Cada etapa puede usar una imagen base diferente, y los artefactos (por ejemplo, binarios o archivos compilados) de una etapa se pueden copiar a una etapa posterior. Esto ayuda a evitar que las herramientas de compilación y otros archivos innecesarios queden en la imagen final. 
 
En la carpeta `soluciones` se creará una carpeta con el siguiente formato `<vuestro nombre>-Ejercicio-9`, donde se incluirán el `Dockerfile`, capturas del proceso de construcción y verificación, y un archivo `README_ej09.md` con las explicaciones de los pasos realizados.

## Tarea
1. Reusar el proyecto frontend del Ejercicio 4 (carpeta "ui-web") y crear un nuevo Dockerfile usando la funcionalidad de Multistage. Crear la imagen y el contenedor (atención a los puertos).
2. Levantar el contenedor de la imagen original, creada en el ejercicio2.
3. Comparar el uso de recursos de ambos contenedores (Ayuda: ejecutar comando "docker stats" o a través de la aplicación Docker Desktop en Windows).
