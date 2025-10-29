# Ejercicio 4 - Creación de imagenes y despliegue de contenedor
## Objetivos
- Familiarse con comandos básicos de docker.
- Preparación básica de un dokerfile.
- Creación de una imagen de docker válida.
- Desplegar un contenedor.

## Consideraciones
 1. En la carpeta `soluciones` se creará una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-4`.
 2. En esa carpeta se dejará el dockerfile creado y en un archivo llamado `README_ej04.md` con los comandos utilizados y con sus salidas por pantalla. Ejemplo:
 ``` 
 > docker ps
 CONTAINER ID   IMAGE                                                  COMMAND                  CREATED        STATUS        PORTS                  NAMES
 1d5f6384f902   harbor.thelmalouise.ddns.net/docker_test/nginx:0.0.1   "/docker-entrypoint.…"   23 hours ago   Up 23 hours   0.0.0.0:8080->80/tcp   mi_nginx
 
 ```
 3. El ejercicio consta de dos proyectos por separado escritos en nodejs, uno actua de backend y el otro de fronend.
    
    1. ./datos/Ejercicio04/ui-web  -> Frontend
    1. ./datos/Ejercicio04/api-web -> Backend
    
    Dentro irá el dokerfile correspondiente, ajustado a las necesidades de cada proyecto. Os lo tenéis que traer en local y generar el dockerfile.
    >[!TIP] Instrucciones para poner en marcha el proyecto de ui-web
    ```
    > yarn
    > yarn dev --host
     ```
    >[!TIP] Instrucciones para poner en marcha el proyecto de api-web
    ```
    > npm install
    > node index.js
     ```

## Tarea
 1. Crear los fichero dockerfile en cada proyecto.

      Comenzamos con el fichero `Dockerfile` de api:

      ```bash
         # Usa una imagen base de Node.js
         FROM node:14

         # Establece el directorio de trabajo
         WORKDIR /app

         # Copia los archivos de proyecto
         COPY . .

         # Instala las dependencias
         RUN npm install

         # Expone el puerto que usará la aplicación
         EXPOSE 3000

         # Comando para iniciar la aplicación
         CMD ["node", "index.js"]   
      ```

      Empezamos con el `FROM` el cual saca la imagen base con la que vamos a trabajar siendo `Node.js en su versión 14`; establecemos los directorios de trabajo con `WORKDIR` y una ruta; copiamos los elementos que estimemos oportunos con `COPY`, en este supuesto todos con `. .` del proyecto desde el directorio actual en tu máquina local al directorio de trabajo /app en el contenedor; usamos `RUN` y tras este `npm install` con la finalidad de instalar las dependencias listadas en el archivo `package.json` al contenedor; mostramos el puerto por el que escuchará el contenedor con `EXPOSE` y por último con `CMD` ejecutaremos un comportamiento cuando el contenedor se inicie, aconteciendo en este caso `node index.js` mostrando el servidor definido en este archivo.

      Seguimos con el fichero `Dockerfile` de ui:

      ```bash
         # Usa una imagen base de Node.js
         FROM node:14

         # Establece el directorio de trabajo
         WORKDIR /app

         # Copia los archivos de proyecto
         COPY package*.json ./

         # Instala las dependencias
         RUN yarn install

         # Copiar el resto de archivos del proyecto
         COPY . . 

         # Expone el puerto que usará la aplicación
         EXPOSE 5173

         # Comando para iniciar la aplicación
         CMD ["yarn", "dev", "--host"]
      ```
      Seguimos pasos similares al anterior diferenciando los comandos de instalación de las dependencias y el comando para la iniciación del contenedor cuando ejecutemos el contenedor centrado este a aplicaciones fronted. Además, en este Dockerfile copiamos primero los archivos package.json y después el resto aprovechando mejor el caché porque estas dependencias solo se modificarán cuando cambie este archivo concreto y no cualquiera.

 2. Ejecutar los comandos necesarios para generar las imágenes.Realizar el retag de la imágenes para que sea con la siguiente nomenclatura `<vuestro nombre>/<nombre proyecto>:0.0.1`

      Para la generación de las imágenes he realizado el siguiente comando que permite generar la imagen con el nombre que desee:

      ```bash
      docker build -t LeandroCarbajoMendez/ui-web:0.0.1 .
      ```
      Con el `-t` añado una etiqueta a la propia imagen pudiendo nombrarla como quiera.
   
      ![Captura sobre el código](../../datos/Ejercicio04/build%20ui%20web.png)

      ![Captura sobre el código](../../datos/Ejercicio04/built%20api%20web.png)


 3. Sacar una captura de pantalla del listado de imágenes, con el objetivo de comprobar que la imagen se ha creado y nombrado de forma correcta.

      ```bash
      docker images
      ```

      ![Captura sobre el código](../../datos/Ejercicio04/mostrar%20imagenes.png)

 4. Desplegar 2 contenedores, uno el front y el otro el back.(!!ojo con los puertos )
 5. Listar mediante comandos los contenedores existentes.

      ```bash
      docker run -d -p puertoMaquinaLocal:puertoContenedor nombre_imagen
      ```
      Con este comando, desplegamos un contenedor en segundo plano `-d` y con `-p` añadimos los puertos de nuestra máquina local y nuestro contenedor para luego acceder desde el navegador con `localhost:puertoMaquinaLocal`.

      Posterior al despliegue de los contenedores en ambos uso `docker ps` para mostrar los contenedores en ejecución.

      ![Captura sobre el código](../../datos/Ejercicio04/run%20maquina%20api%20y%20mostrar%20si%20esta.png)

      ![Captura sobre el código](../../datos/Ejercicio04/run%20maquina%20ui%20y%20mostrar.png)

 6. Usar el navegador para verificar el funcionamiento.

      Verificamos su funcionamiento:

      ![Captura sobre el código](../../datos/Ejercicio04/ejecucion%20en%20localhost.png)


      ![Captura sobre el código](../../datos/Ejercicio04/ejecucion%20en%20localhost%20ui.png)

 7. Eliminar los contenedores.

       ```bash
      docker rm ID_contenedor|nombre_contenedor
      ```
      Eliminamos el contenedor correspondiente añadiendo el ID propio.

      ![Captura sobre el código](../../datos/Ejercicio04/eliminacion%20de%20contendores.png)

 8. Eliminar las imágenes.

      ```bash
      docker rmi ID_imagen|nombre_imagen
      ```
      Ese comando nos ayudará eliminar las imágenes aportando su Id o nombre.  

      ![Captura sobre el código](../../datos/Ejercicio04/eliminacion%20imagenes.png)


