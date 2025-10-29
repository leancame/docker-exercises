# Ejercicio 2 - DockerHub
## Objetivos
Familiarizarse con la documentación de Dockerhub

## Consideraciones
 En la carpeta `soluciones` se creara una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-2`.

## Tarea
 Responded a las siguientes cuestiones leyendo la documentación de DockerHub y razonando

 1. ¿Qué significa que una imagen sea "oficial"? ¿Cuáles son las ventajas de utilizar imágenes oficiales?

    >Una publicación oficial es aquella realizada por el propio Docker y sus ventaja son completa compatibilidad ya que es el mismo Docker el encargado de esta, seguridad por parte de esta ya que no es un tercero el que ha realizado la imagen y aporta soporte al ser mantenidas por esta empresa.
 
 2. Elige una imagen que te interese y revisa su documentación en Docker Hub. ¿Qué información proporciona la documentación?

    > En mi caso he buscado la imagen oficial dada por Ubuntu. Al interactuar con esta nos da usa serie de datos. En primer lugar una rápida referencia de quien la mantiene y dónde podemos encontrar ayuda. Además, nos aporta diversas etiquetas compatibles y Dockerfile con sus enlaces. Para descargar la imagen podemos usar `Docker Pull Ubuntu`. Además posee información sobre la imagen, en este caso sobre Ubuntu. También aparece la licencia de la imagen.  
 
 3. ¿Cómo puede influir la versión de una imagen en su uso? ¿Qué estrategia usarías para seleccionar una versión específica?

    > Desde este punto de vista es necesario saber que versión de la imagen vamos a usar, debiéndose esto a que dependiendo de las necesidades de nuestro proyecto sabremos que imagen es más a acorde al caso. Como estrategias, debemos conocer nuesto proyecto y sus cualidades adaptando eso a la imagen concreta. Si el poyecto es novedoso no vas a usar un linux versión 18 por ejemplo. Además debes ver conceptos como la compatibilidad de tu proyecto a esa imagen y la seguridad que esta pueda aportar.
    
 4. En la imagen de MySQL, ¿qué variables de entorno se pueden configurar? ¿Hay alguna que sea obligatoria?

    >Las variables de entorno en MySQL son MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER,MYSQL_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD. La obligatoria es MYSQL_ROOT_PASSWORD que especifica la contraseña que se establecerá para la rootcuenta de superusuario de MySQL.
 
 5. En la imagen de Postgres, ¿cómo puedes establecer la contraseña para el usuario postgres utilizando una variable de entorno?

    >Usando la variable POSTGRES_PASSWORD.
 
 6. En la imagen de NGINX, ¿es posible configurar variables de entorno para personalizar el comportamiento del servidor? Si es así, ¿qué opciones están  disponibles y qué efecto tienen?

    >De fábrica, nginx no admite variables de entorno en la mayoría de los bloques de configuración. Sin embargo, esta imagen tiene una función que las extrae antes de que nginx se inicie. 

    >NGINX_ENVSUBST_TEMPLATE_DIR: Contiene un directorio que contiene archivos de plantillas y si no existe no hará funciones.

    >NGINX_ENVSUBST_TEMPLATE_SUFFIX: Un sufijo de archivos de plantilla.

    >NGINX_ENVSUBST_OUTPUT_DIR: Un directorio donde se muestra el resultado de ejecutar envsubst.
  
 7. ¿Qué puerto expone la imagen oficial de NGINX por defecto? ¿Cómo puedes mapear este puerto a uno diferente en tu máquina local cuando ejecutas el contenedor?

    >El puerto por defecto en NGINX es 80 y para mapear este puerto a uno diferente en tu máquina local cuando ejecutas el contenedor, puedes usar la opción `-p` de Docker. Por ejemplo, si quieres mapear el puerto 80 del contenedor al puerto 9000 en tu máquina local, puedes ejecutar el siguiente comando:

    ```bash
    docker run --name some-nginx -d -p 9000:80 some-content-nginx
    ```

 8. En la imagen de NGINX, ¿dónde debes montar un volumen para reemplazar el archivo index.html por defecto y servir tu propio contenido?
    
    Observando el comando siguiente:
    ```bash
    docker run --name some-nginx -v /some/content:/usr/share/nginx/html:ro -d nginx
    ````
    > Para montar NGINX usaremos el volumen /usr/share/nginx/html.
 
 9. Para la imagen de Postgres, ¿dónde puedes montar un volumen para persistir las bases de datos que se generen en el contenedor?¿Qué pasa si no configuras un volumen y el contenedor se reinicia o se elimina?

    >Se debe montar en /var/lib/postgresql/data, ya que si no configuras un volumen y el contenedor se reinicia o se elimina, los datos de la base de datos no se persistirán. Esto significa que cualquier información almacenada en la base de datos se perderá, ya que los datos dentro del contenedor son efímeros y se eliminan junto con el contenedor.