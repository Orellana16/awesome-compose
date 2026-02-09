# --- STAGE 1: Build ---
# Usamos una versión específica de Node para control de versiones
FROM node:18-alpine AS build
WORKDIR /app

# Instalamos dependencias
COPY package*.json ./
RUN npm install

# Copiamos código y compilamos para producción
COPY . .
RUN npm run build

# --- STAGE 2: Runtime ---
# Usamos una imagen ligera de Nginx para servir los archivos estáticos
FROM nginx:1.25-alpine

# Copiamos los archivos compilados desde la etapa anterior
COPY --from=build /app/build /usr/share/nginx/html

# Exponemos el puerto interno (3000 o 80 según tu preferencia)
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]