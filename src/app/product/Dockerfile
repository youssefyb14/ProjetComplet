# Utiliser une image Node.js officielle pour la construction de l'application Angular
FROM node:18-alpine AS build

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers de configuration pour installer les dépendances
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier tout le reste des fichiers du projet dans l'image Docker
COPY . .

# Construire l'application Angular en mode production
RUN npm run build --prod

# Étape pour déployer l'application avec un serveur Nginx
FROM nginx:alpine

# Copier le contenu de la construction dans le dossier d'accueil de Nginx
COPY --from=build /app/dist/ /usr/share/nginx/html

# Exposer le port 80 (par défaut pour Nginx)
EXPOSE 80

# Démarrer Nginx pour servir l'application
CMD ["nginx", "-g", "daemon off;"]
