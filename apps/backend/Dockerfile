# apps/backend/Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app

# Copier les fichiers package.json
COPY package*.json ./
RUN npm ci --only=production

# Copier le code source
COPY . .

# Build de l'application
RUN npm run build

# Image de production
FROM node:18-alpine AS production

WORKDIR /app

# Copier les dépendances de production
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package.json ./package.json

EXPOSE 3000

CMD ["node", "dist/main"]