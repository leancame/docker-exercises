# Ejercicio Extra 1 - Docker Swarm

## Objetivos

Crear un clúster de Docker Swarm con un nodo manager y varios workers, desplegar servicios, escalar réplicas y verificar la correcta distribución de los contenedores entre los nodos.

## Consideraciones

En la carpeta `soluciones` se creará una carpeta con el siguiente formato `<vuestro nombre>-Ejercicio-Extra-1`, donde se incluirán capturas del proceso de construcción y verificación, y un archivo `README_op01.md` con las explicaciones de los pasos realizados.

Se utilizarán las herramientas `docker-machine` y `virtualbox`. 

## Tarea

1. **Crear las máquinas Docker:**
   - Crear 4 máquinas Docker: 
     - 1 manager (`manager1`)
     - 3 workers (`worker1`, `worker2`, `worker3`)
   - Si surgen problemas de virtualización, agregar la opción `--virtualbox-no-vtx-check`.

2. **Listar las máquinas creadas:**
   - Verificar que las 4 máquinas han sido creadas correctamente.

3. **Inicializar Docker Swarm:**
   - Inicializar un Swarm en Docker, seleccionando el nodo `manager1` como manager.

4. **Agregar los nodos workers al Swarm:**
   - Unir los nodos `worker1`, `worker2` y `worker3` al Swarm.

5. **Listar los nodos:**
   - Comprobar que todos los nodos están correctamente unidos al Swarm.

6. **Crear un servicio con NGINX:**
   - Crear un servicio que utilice la imagen `nginx`, con una sola réplica.

7. **Listar los servicios creados:**
   - Verificar que el servicio de NGINX ha sido creado correctamente.

8. **Verificar el nodo del contenedor NGINX:**
   - Comprobar en qué nodo fue desplegado el contenedor de NGINX.
   - Si el contenedor fue desplegado en el nodo `manager`, detenerlo con el comando correspondiente.
   - Volver a verificar en qué nodo fue desplegado el contenedor. ¿Qué ocurrió?

9. **Escalar el servicio a 2 réplicas:**
   - Escalar el servicio de NGINX a 2 réplicas.

10. **Crear un nuevo servicio de NGINX:**
    - Eliminar el servicio anterior.
    - Crear un segundo servicio de NGINX con 2 réplicas y donde se publique el puerto `8080` del host, apuntando al puerto `80` del servicio NGINX.

11. **Verificar el nodo del contenedor NGINX:**
    - Comprobar en qué nodo fue desplegado el contenedor del nuevo servicio de NGINX.
    - Si el contenedor fue desplegado en el nodo `manager`, detenerlo con el comando correspondiente.

12. **Comprobar acceso desde localhost:**
    - Verificar que, a pesar de que el nodo `manager` no tiene contenedores corriendo, el servicio sigue siendo accesible desde `localhost:8080` (por ejemplo, con el comando `curl`).