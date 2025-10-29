#ETAPA 1
#Constructor de la aplicación
FROM node:14 AS build
 
#Establecer el directorio de trabajo
WORKDIR /app
 
#Copiar los archivos de dependencias
COPY package*.json ./
 
#Copiar el resto del código fuente
COPY . .

#Instalar todas las dependencias
RUN yarn install

#Construir la aplicación para producción
RUN yarn run build
 
#ETAPA 2
#Imagen de producción
FROM nginx AS production
 
#Establecer el directorio de trabajo
WORKDIR /app
 
#Copiar solo los archivos necesarios desde construcción
COPY --from=build /app/dist /usr/share/nginx/html
 
#Exponer el puerto en el que la aplicación se ejecutará
EXPOSE 80

