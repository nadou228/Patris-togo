# frontend/Dockerfile
FROM node:20-alpine AS build

WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm ci

# Copier tout le code source
COPY . .

# Construire l'application
RUN npm run build

# Étape 2 : Serveur de production
FROM node:20-alpine

WORKDIR /app

# Installer un serveur statique simple
RUN npm install -g serve

# Copier les fichiers construits depuis l'étape précédente
COPY --from=build /app/dist ./dist

# Exposer le port
EXPOSE 3000

# Démarrer le serveur
CMD ["serve", "-s", "dist", "-l", "3000"]