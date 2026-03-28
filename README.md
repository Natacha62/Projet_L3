# MovieAddict - Déploiement CI/CD avec Docker & Windows Server

MovieAddict est une application web Node.js permettant de consulter des films, ajouter des commentaires et gérer un compte utilisateur.  
Ce dépôt contient **la version adaptée pour un déploiement automatisé** via un pipeline CI/CD complet utilisant :

- GitHub Actions
- Docker Windows Server
- IIS (reverse proxy)
- Tailscale (connexion sécurisée)
- Scripts Powershell (build & deploy)

---

## Fonctionnalités principales de l'application

 - Consultation de films (bandes-annonces)
 - Création de compte / Connexion
 - Ajout de commentaires
 - Notation des films
 - Gestion de sessions utilisateur
 - Base de données SQLite intégrée

---

## Architecture du déploiement

Le pipeline CI/CD fonctionne ainsi :

1. **Push sur la branche `main`**
2. GitHub Actions se connecte au serveur Windows via **Tailscale**
3. Exécution du script `build.ps1` :
    - Reconstruction de l'image Docker Windows
    - Push vers Docker Hub
4. Exécution du script `deploy.ps1` : 
    - Arrêt de l'ancien conteneur
    - Suppression de l'image précédente
    - Lancement du nouveau conteneur
5. IIS expose l'application sur le port **80**

---

# Installation locale (mode développement)

> Cette section concerne uniquement l'exécution locale.
> Le déploiement en production est entièrement automatisé.

## 1. Cloner le dépôt
```bash
git clone https://github.com/Natacha62/Projet_L3.git
cd Projet_L3
```

## 2. Installer les dépendances
```bash
npm install
```

## 3. Lancer l'application
```bash
node server.js
```

## 4. Accéder à l'application

http://localhost:3000

---

# Exécution via Docker (mode production)

L'image Docker Windows Server est disponible sur Docker Hub :
```bash
docker pull natacha6262/schoolproject-app:latest
```

Lancer le conteneur :
```bash
docker run -d -p 3000:3000 --name schoolproject-app natacha6262/schoolproject-app:latest
```

---

## Aperçu de l'application 

Voici comment se présente la consultation d'un film :

![Capture d'écran](Images/Films.png)

![Capture d'écran](Images/Modale.png)