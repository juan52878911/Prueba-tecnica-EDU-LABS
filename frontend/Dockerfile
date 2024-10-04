FROM node:16-alpine as build

WORKDIR /app

# Copia los archivos package.json y package-lock.json
COPY package*.json ./

# Instala dependencias
RUN npm install

# Copia el resto del código
COPY . .

# Compila la aplicación Angular
RUN npm run build --prod

# Configura nginx para servir la aplicación
FROM nginx:alpine

COPY --from=build /app/dist/tu-nombre-app /usr/share/nginx/html

# Exponer el puerto 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
