# 🎉 Gestion des Événements Hybrides

---

## 📝 Introduction

Le projet **Gestion des événements hybrides** vise à développer une plateforme moderne et intuitive permettant la gestion d'événements hybrides — accessibles à la fois en ligne et en présentiel.

L'application cible deux types d'utilisateurs :

- 👩‍💼 **Les organisateurs** : peuvent créer et gérer leurs événements.  
- 👩‍🎓 **Les participants** : peuvent explorer les événements disponibles, s'inscrire, et choisir leur mode de participation.

👉 Cette plateforme met l’accent sur un **design moderne et responsive** grâce à **Tailwind CSS**.

  ![Screenshot 1](screenshots/1.png)

---

## 🎯 Objectifs du Projet

- **Fournir un outil de gestion d’événements** : création, modification, et suppression d’événements avec des détails complets.  
- **Offrir une interface intuitive** : consultation, recherche et filtrage d’événements.  
- **Faciliter les inscriptions** : gestion des modes de participation (en ligne ou présentiel).  
- **Proposer un tableau de bord analytique** : statistiques et graphiques sur la participation.

---

## 🧩 Bibliothèques Utilisées

### ⚙️ Backend

- **Express.js** — Framework backend  
- **Mongoose** — Modélisation MongoDB  
- **Jsonwebtoken (JWT)** — Authentification  
- **Bcryptjs** — Hashage de mots de passe  
- **Dotenv** — Variables d’environnement  

### 💻 Frontend

- **Axios** — Appels API  
- **React Router** — Navigation  
- **Recharts** — Graphiques  
- **Tailwind CSS** — Design responsive  

---

## 📦 Installation des dépendances

### Backend
    ```bash
    npm install express mongoose jsonwebtoken bcryptjs dotenv
    
### Frontend Installation
    ```bash
    npm install axios react-router-dom recharts tailwindcss


## 🧱 Plan de Réalisation

### Étape 1 : Configuration
- Initialisation des projets backend et frontend  
- Installation des dépendances nécessaires  

### Étape 2 : Développement Backend
- Création des modèles MongoDB  
- Implémentation des routes API REST  
- Tests avec Postman  

### Étape 3 : Développement Frontend
- Conception des pages principales  
- Intégration des API backend  
- Application du design avec Tailwind CSS  

### Étape 4 : Tests
- Tests API et vérification manuelle des fonctionnalités  

---

## 🏗️ Architecture du Projet

  ![Screenshot 1](screenshots/2.png)

### Backend
Le backend est construit avec **Express.js** et utilise **MongoDB**.

### Frontend
Le frontend utilise **React** avec **Tailwind CSS**.

---

## 📂 Structure du Backend

  ![Screenshot 1](screenshots/3.png)


### `controllers/`

#### `authController.js`
- Gère la logique d’authentification (connexion, inscription)  
- Génère un token JWT avec durée d’une heure
- Inscription d'un utilisateur
- Génération du token
- Gestion des erreurs avec `try...catch`

  ![Screenshot 1](screenshots/4.png)

#### `eventController.js`
CRUD complet pour les événements :
- `createEvent` : création d’un événement  
- `getEvents` : récupération de tous les événements  
- `getEventById` : récupération d’un événement spécifique  
- `updateEvent` : mise à jour  
- `deleteEvent` : suppression  
- `joinEvent` / `leaveEvent` : inscription et désinscription des participants  

  ![Screenshot 1](screenshots/5.png)

#### `participantController.js`
- `addParticipant` : ajoute un participant et met à jour l’événement  
- `getParticipantsByEvent` : retourne les participants d’un événement  

  ![Screenshot 1](screenshots/6.png)

---

### `middleware/`

#### `authMiddleware.js`
- `protect` : vérifie le token JWT et authentifie l’utilisateur  
- `authorize` : autorise selon le rôle (organisateur, participant)  
  ![Screenshot 1](screenshots/7.png)

---

### `models/`
- `Event.js` : Schéma d’événement
  ![Screenshot 1](screenshots/8.png)

- `Participant.js` : Schéma de participant  
  ![Screenshot 1](screenshots/9.png)

Avant sauvegarde (`pre save`) : hashage du mot de passe avec **bcrypt**  
Méthode `comparePassword` : compare le mot de passe entré et celui stocké.  

---

### `routes/`
- `authRoutes.js` : inscription & connexion (`/register`, `/login`)
    ![Screenshot 1](screenshots/10.png)
 
- `eventRoutes.js` : routes CRUD des événements
    ![Screenshot 1](screenshots/11.png)

- `participantRoutes.js` : récupération des participants d’un événement  
    ![Screenshot 1](screenshots/12.png)

---

### `utils/db.js`
Contient la logique de connexion à **MongoDB**.
    ![Screenshot 1](screenshots/13.png)

---

### `.env`
Stocke les variables d’environnement : URL de la base de données, clé JWT, etc.
    ![Screenshot 1](screenshots/14.png)

---

### `server.js`
- Point d’entrée du backend  
- Configure **Express**, **CORS**, **dotenv**, et **body-parser**  
- Connecte la base de données et lie les routes  
    ![Screenshot 1](screenshots/15.png)

---

## 🧪 Tests Backend avec Postman

### 🔐 Authentification
- `POST /auth/register` : inscription
      ![Screenshot 1](screenshots/16.png)

- `POST /auth/login` : connexion  
    ![Screenshot 1](screenshots/17.png)

### 📅 Événements
- `POST /events` : créer un événement
      ![Screenshot 1](screenshots/18.png)
    ![Screenshot 1](screenshots/19.png)


- `GET /events` : liste complète
        ![Screenshot 1](screenshots/21.png)

- `PUT /events/:id` : modifier
        ![Screenshot 1](screenshots/22.png)

- `DELETE /events/:id` : supprimer  
      ![Screenshot 1](screenshots/23.png)

> ⚠️ Si un **participant** tente d’accéder à une route d’organisateur, la requête est refusée.
      ![Screenshot 1](screenshots/20.png)



---

## 💅 Structure du Frontend
      ![Screenshot 1](screenshots/24.png)

### `components/`
- `AddParticipant.jsx`, `CreateEvent.jsx`, `EditEventParticipant.jsx` — gestion des événements  
- `EventDetails.jsx` — affichage détaillé  
- `Navbar.jsx` — barre de navigation  
- `PrivateRoute.jsx` — protège les routes privées  

### `context/AuthContext.js`
- Gestion globale de l’état d’authentification (JWT, utilisateur connecté)

### `pages/`
- `Dashboard.jsx` — tableau de bord organisateur  
- `Home.jsx`, `Homep.jsx` — pages d’accueil  
- `Login.js`, `Register.js` — formulaires d’authentification  

### `services/`
- Gestion des appels API (non détaillée ici)

### Fichiers principaux :
- `App.js` : définit les routes  
- `App.css`, `index.css` : styles globaux  
- `index.js` : point de montage React  

---

## 🧪 Tests Frontend

- Page d’inscription
        ![Screenshot 1](screenshots/25.png)

- Vérification de la création dans la base de données
        ![Screenshot 1](screenshots/26.png)

- Page de connexion
        ![Screenshot 1](screenshots/27.png)

- Création d’un événement
        ![Screenshot 1](screenshots/28.png)

- Vérification de la présence dans la base de données  
      ![Screenshot 1](screenshots/29.png)

---

## 🐳 Déploiement avec Docker

### Fichiers :
- `Dockerfile` Backend
        ![Screenshot 1](screenshots/30.png)

- `Dockerfile` Frontend
        ![Screenshot 1](screenshots/31.png)

- `docker-compose.yml`  
      ![Screenshot 1](screenshots/32.png)

### Étapes :
1. **Création des containers**
         ![Screenshot 1](screenshots/33.png)

3. **Lancement des containers**
            ![Screenshot 1](screenshots/34.png)
            ![Screenshot 1](screenshots/35.png)

5. **Connexion à la base de données**
            ![Screenshot 1](screenshots/36.png)

7. **Vérification du frontend :**
   ```bash
   http://localhost:3000

  ![Screenshot 1](screenshots/37.png)

---

## 🏁 Conclusion

Ce projet de **gestion des événements hybrides** constitue une solution complète combinant un **backend robuste** et un **frontend moderne**.

Grâce à **Node.js**, **Express**, **MongoDB** *(backend)* et **React + Tailwind CSS** *(frontend)*, il propose :

- 🔐 **Une gestion sécurisée des utilisateurs** (authentification, rôles)  
- 📅 **Une gestion fluide des événements** (création, mise à jour, participation)  
- 📊 **Une interface responsive et ergonomique**

Le code suit une **architecture claire et modulaire**, facilitant la **maintenance** et l’**évolution** du projet.

---

**Réalisée par :**  
Firdawsse Ahchouche & Zineb Feth-Eddine  
