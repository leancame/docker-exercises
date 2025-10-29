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