composer create-project symfony/skeleton:"^6.3" .

# Install additional Symfony components
composer require symfony/webapp-pack
composer require symfony/security-bundle
composer require symfony/orm-pack
composer require symfony/form
composer require symfony/validator
composer require symfony/twig-bundle
composer require symfony/asset
composer require symfony/security-csrf
composer require symfony/rate-limiter
composer require --dev symfony/maker-bundle
composer require symfony/debug-bundle --dev
composer require symfony/web-profiler-bundle --dev

# Install Bootstrap
composer require symfony/webpack-encore-bundle
npm install
npm install bootstrap
npm run build


-----------------------------------------------REALISATION----------------------------------------



# symfonyProject
💼 Projet Symfony : InvoicePro – Gestion de Factures et Clients
🔧 Installation et Préparation de l’Environnement
1. Clonage du projet
Le projet est hébergé sur GitHub. Pour le cloner :


git clone https://github.com/LOUKCH/symfonyProject.git
cd symfonyProject/projet
2. Installation des dépendances PHP
On utilise Composer pour installer toutes les bibliothèques Symfony et les bundles nécessaires :


composer install
3. Installation des dépendances front-end
L’application utilise Webpack Encore. Il faut donc installer les paquets NPM :
npm install
npm run build
5. Création de la base de données et exécution des migrations
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
🧩 Structure du Projet
🧑‍💼 Entité User
L’entité User représente les utilisateurs. Chaque utilisateur a :

nom, prénom, email, identifiant, mot de passe.

Une relation OneToMany avec Client (chaque user peut avoir plusieurs clients).

Authentification gérée via Symfony Security.

Validation avec Assert et #[UniqueEntity] pour éviter les doublons d’identifiant.

🧾 Entité Client
Chaque client appartient à un utilisateur (relation ManyToOne). Les champs :

nom du gérant, raison sociale, ville, pays, téléphone...

Relation OneToMany avec Facture.

Un client ne peut pas être supprimé s’il possède des factures (sécurité gérée dans le contrôleur).

📄 Entité Facture
Une facture contient :

numéro (unique), date, montant, état (Payée, Non payée...), note.

Chaque facture appartient à un Client.

🔐 Authentification & Sécurité
Utilisation de Symfony Security :

Système d’inscription (RegistrationController)

Connexion via formulaire (SecurityController)

Chaque utilisateur ne peut voir que ses propres clients et factures

Routes sécurisées avec #[IsGranted('ROLE_USER')] dans les contrôleurs

🎮 Contrôleurs
🔑 SecurityController
Gère la connexion

Redirige vers la page client après login

👤 RegistrationController
Formulaire d’inscription d’un nouvel utilisateur

Hash du mot de passe avec UserPasswordHasherInterface

Redirection automatique vers login

📋 ClientController
Liste des clients d’un utilisateur connecté

CRUD complet (ajout, édition, suppression)

Vérifie que le client appartient bien au user avant chaque action

Affiche les factures d’un client (via bouton)

📜 FactureController
Liste toutes les factures de tous les clients de l’utilisateur

Ajout, édition, suppression d’une facture

Génère automatiquement un numéro de facture unique

Filtrage des clients possibles selon l’utilisateur

🎨 Vues (Twig)
Toutes les vues sont personnalisées et modernes grâce à Bootstrap :

base.html.twig : Template principal, avec navbar conditionnelle (connexion/déconnexion)

login.html.twig et register.html.twig : formulaire utilisateur

client/index.html.twig : tableau des clients avec options (voir, modifier, supprimer, facturer)

facture/index.html.twig : liste des factures avec états et montants

facture/by_client.html.twig : affichage des factures pour un seul client

home.html.twig : page d’accueil publique, style marketing avec hero section, features, pricing, etc.

🐳 Docker

docker compose up --build


📈 Fonctionnalités Clés Réalisées
✅ Authentification sécurisée

✅ Inscription avec validation des champs

✅ Création de clients

✅ Gestion des factures

✅ Relations entité User → Client → Facture

✅ Sécurité sur les routes

✅ Interface moderne avec Bootstrap

✅ Intégration Docker pour déploiement

✅ Navbar dynamique (selon login/logout)

✅ Page d'accueil publique responsive

🚀 Conclusion
Le projet InvoicePro est une application Symfony robuste et modulaire, conçue pour gérer les factures et les clients d’un utilisateur connecté, avec une sécurité renforcée et un design moderne. Il est prêt pour être déployé dans un environnement Docker ou intégré à une chaîne DevOps (SonarQube, Jenkins, DockerHub, Ansible...).
