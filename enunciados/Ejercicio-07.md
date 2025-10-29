# Ejercicio 7 - Gestión de permisos y usuarios

## Objetivo
El objetivo de este ejercicio es que los estudiantes aprendan a gestionar permisos y usuarios en un contenedor de Docker, creando un script que imprime un mensaje y configurando los permisos adecuados para el script y el usuario que lo ejecuta, lo que les permitirá comprender la importancia de la seguridad y el control de acceso en entornos de contenedores.

## Consideraciones
 1. En la carpeta `soluciones` se creará una carpeta con el siguiente formato  `<vuestro nombre>-Ejercicio-7`.
 2. En esa carpeta se dejará el dockerfile creado y en un archivo txt llamado `README_ej07.md` con los comandos utilizados con sus salidas por pantalla.

## Tarea
1. Crea un shell script que imprima un mensaje por consola. 
2. Crea un Dockerfile con una imagen base de ubuntu, donde se copie el shell script creado y lo ejecute (al levantar el contenedor). y asegúrate de que los permisos del script se establezcan en lectura, escritura y ejecución para el usuario root, y solo lectura para otros.
1. Crea la imagen y levanta el contenedor. Comprueba que funciona.
1. Crea un usuario con UID 1500 (y nombre a tu elección) en el Dockerfile. Cambia el usuario bajo el cual se ejecutarán los siguientes comandos, al usuario creado.
1. Crea la nueva imagen y levanta el nuevo contenedor. ¿Qué ha ocurrido?
1. Ingresa al contenedor. Corrobora que el usuario es el que has creado. Ahora, comprueba si es posible cambiar de usuario a root. ¿Qué ha pasado?
1. Reflexiona sobre lo siguiente: si logras acceder como root, ¿qué problemas o riesgos podrían surgir al permitir accesos con privilegios elevados? Si no logras acceder como root, ¿qué beneficios tiene esta restricción desde el punto de vista de la seguridad y estabilidad del contenedor? 
1. Adjunta capturas del desarrollo y resultado final del ejercicio.
