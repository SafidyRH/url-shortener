# apps/frontend/Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app

# Copier les fichiers package.json
COPY package*.json ./
RUN npm ci

# Copier le code source
COPY . .

# Build de l'application
RUN npm run build

# Image de production avec nginx
FROM nginx:alpine AS production

# Copier les fichiers buildés
COPY --from=builder /app/dist /usr/share/nginx/html

# Configuration nginx pour les SPAs
RUN echo 'server { \
    listen 80; \
    server_name localhost; \
    location / { \
    root /usr/share/nginx/html; \
    index index.html index.htm; \
    try_files $uri $uri/ /index.html; \
    } \
    }' > /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]