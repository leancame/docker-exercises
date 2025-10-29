# Ejercicio Extra 2 - MultiArch Build

## Descripción

Un **MultiArch Build** permite crear imágenes de Docker que pueden ejecutarse en diferentes arquitecturas de procesador (por ejemplo, `amd64` y `arm64`). Docker utiliza manifestos para agrupar múltiples imágenes bajo un mismo tag, lo que permite seleccionar automáticamente la imagen adecuada según la arquitectura de la máquina donde se ejecuta el contenedor.

## Consideraciones

En la carpeta `soluciones` se creará una carpeta con el siguiente formato `<vuestro nombre>-Ejercicio-Extra-2`, donde se incluirán capturas del proceso de construcción y verificación, y un archivo `README_op02.md` con las explicaciones de los pasos realizados.

## Tarea

1. **Habilitar características experimentales de Docker:**
   - Editar el archivo `config.json` de Docker para habilitar las características experimentales.

2. **Crear directorios por arquitectura:**
   - Crear dos directorios:
     - Uno llamado `arm64`
     - Otro llamado `amd64`

3. **Crear Dockerfiles:**
   - En el directorio `arm64`, crear un Dockerfile que utilice la imagen base `alpine` y ejecute el comando `Hola mundo desde Linux 64bits`.
   - En el directorio `amd64`, crear un Dockerfile que utilice la imagen base `alpine` y ejecute el comando `Hola mundo desde Windows 64bits`.

4. **Crear y taggear imágenes:**
   - Construir ambas imágenes y etiquetarlas con el siguiente formato:
     - `<tu-repo-de-dockerhub>/<nombre-imagen>:arm64`
     - `<tu-repo-de-dockerhub>/<nombre-imagen>:amd64`
   - Asegúrate de que el nombre de las imágenes sea el mismo.

5. **Pushear imágenes a DockerHub:**
   - Subir ambas imágenes a DockerHub.

6. **Verificar imágenes en DockerHub:**
   - Comprobar que ambas imágenes han sido subidas correctamente a DockerHub.

7. **Construir el manifest:**
   - Crear un manifest que agrupe ambas imágenes bajo un solo tag con el formato:
     - `<tu-repo-de-dockerhub>/<nombre-imagen>:latest`

8. **Verificar MultiArch Build:**
   - Si tienes un dispositivo con un procesador ARM, como una tablet, móvil o Raspberry Pi, y puedes ejecutar Docker en él, descarga la imagen `<tu-repo-de-dockerhub>/<nombre-imagen>:latest`. Haz lo mismo en tu PC local y verifica que en cada caso se ha descargado la imagen correspondiente a la arquitectura del procesador de cada dispositivo.