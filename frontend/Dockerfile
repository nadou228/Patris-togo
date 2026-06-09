# frontend/Dockerfile
FROM node:20-alpine AS build

WORKDIR /app

# Copier les fichiers de dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm ci

# Copier tout le code source
COPY . .

# Donner les permissions d'exécution à node_modules/.bin
RUN chmod -R +x node_modules/.bin

# Construire l'application (en utilisant le chemin direct vers vite)
RUN ./node_modules/.bin/vite build

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