# deploiement-github
Appli 1 : Page HTML statique

-Technologie : Nginx

-Fichier : index.html

-But : Déployer automatiquement via GitHub Actions sur une VM locale (CI/CD).

-Test réussi : La page est accessible via http://192.168.1.116 avec le message :

"Déploiement GitHub Actions réussi"

Tests effectués:

Test de connexion à la VM en SSH avec GitHub Actions

Test du bon déploiement automatique à chaque commit

Visualisation de la page dans un navigateur local

Contraintes:

L’accès à la page HTML est uniquement local (à cause de l’absence de redirection de ports dans la box ou d’outil comme Ngrok)

Solution alternative:

Pour un accès public : utiliser Ngrok ou configurer un accès NAT dans la box (non fait ici pour raisons de sécurité)

Appli 2 : Stack LAMP (WordPress, MariaDB, Adminer)

Technologies :

WordPress (port 8080)

MariaDB (port 3306)

Adminer (port 8081)

Fichier : deploy-stack.yml

Lancement : docker compose up -d

Tests effectués:

Accès à WordPress via http://192.168.1.116:8080

Accès à Adminer via http://192.168.1.116:8081

Connexion à la base de données depuis Adminer avec les identifiants fournis dans les variables d’environnement du fichier Compose

Contraintes:

Aucun push vers Docker Hub n'a été configuré pour cette stack.

Solution possible (non réalisée ici):

Ajouter une étape dans le workflow GitHub pour construire l’image et la pousser sur Docker Hub avec docker build et docker push.

GitHub Actions
Fichier deploy.yml

Contient les étapes pour :

Déclencher le workflow à chaque push sur la branche principale

Se connecter en SSH à la VM locale

Copier les fichiers HTML

Relancer Nginx si besoin

Secrets configurés

SSH_HOST : adresse IP de la VM (ex : 192.168.1.116)

SSH_USER : utilisateur SSH de la VM (ex : root ou autre)

SSH_PRIVATE_KEY : clé privée SSH correspondant à la clé publique autorisée dans la VM

Problèmes rencontrés:

Plusieurs erreurs d’authentification SSH dues à un mauvais format ou contenu de la clé privée

Problèmes de noms de secrets (renommage ou suppression/recréation nécessaire)

Workflows en échec : erreurs visibles dans l’onglet "Actions" de GitHub

Solutions apportées:

Vérification du bon format de la clé privée (PKCS#1 ou OpenSSH selon config)

Mise à jour correcte des secrets

Test SSH manuel entre GitHub Actions et VM

Conclusion:

Le déploiement CI/CD a été partiellement réussi :

Appli 1 est bien déployée automatiquement et consultable localement

Appli 2 est fonctionnelle via Docker Compose mais n’est pas encore publiée sur un repository Docker

Le projet respecte donc les objectifs de mise en place d’un pipeline CI/CD avec GitHub Actions, démontrant l’intégration continue et un déploiement automatisé en pré-production.
