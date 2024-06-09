# Projet wild-series3

## 02 - Harmonia : Installation et initialisation d'un projet full-stack
### Résumé

Pour créer et utiliser un nouveau projet Harmonia, tu dois respecter les étapes suivantes :

* Créer le projet avec la commande npm create harmonia@latest my-project où my-project est le nom de ton projet.
* Te rendre dans le dossier de ton projet avec la commande cd my-project.
* Lancer l'installation des dépendances avec la commande npm install.
* Créer un fichier .env à la racine du dossier server et y ajouter les variables d'environnement nécessaires.
* Lancer les applications React et Express en parallèle avec la commande npm run dev.

## 03 - Harmonia : Routing
### Résumé

Pour ajouter des routes au server de ton projet Harmonia, tu dois respecter le SRP (Single Responsability Principle) :

* Déclarer tes routes dans un fichier router.js dans le dossier server/app/routers/api.
* Déclarer l'action associée à ta route dans un fichier séparé dans le dossier server/app/controllers.

## 04 - Harmonia : Routing avancé
### Résumé

Pour récupérer des informations depuis l'URL, Express te fournit 2 objets :

* L'objet req.query te donne accès aux paires clé-valeur de la query string. Tu peux l'utiliser pour récupérer le "Eleanor" dans /api/programs?q=Eleanor.
* L'objet req.params te donne accès aux valeurs des segments dynamiques de ta route. Tu peux l'utiliser pour récupérer le "1" dans /api/programs/1.
* Utilise req.query quand tu veux récupérer une partie d'une liste (toutes les séries dont la catégorie est "Comédie", tous les utilisateurs dont le nom commence par un "A"...) et req.params quand tu veux récupérer un seul objet (la série pour une page dédiée, mon profil utilisateur...).

## 05 - Harmonia : Mettre en place une base de données
### Résumé

Pour mettre en place ta base de données :

* La bonne pratique est d'automatiser le processus à l'aide de scripts, ce qui garantit la reproductibilité et la cohérence.
* Tu dois protéger les informations sensibles telles que les noms d'utilisateur et les mots de passe en utilisant des variables d'environnement dans des fichiers .env.
* Tu peux gérer le schéma de ta base de données dans un projet Harmonia depuis le fichier server/database/schema.sql.
* Tu peux mettre ta base de données à partir de ton schéma avec la commande npm run db:migrate.

## 06 - Harmonia : Créer ton premier Repository
### Résumé

Pour fournir un accès à tes données dans Harmonia, tu dois créer un repository :

* Déclare tes classes Repository dans le dossier server/database/models.
* Enregistre les dans le fichier server/database/tables.js.

## 07 - Harmonia : Les fixtures
### Résumé

Pour fournir un accès à tes données dans Harmonia, tu dois créer un repository :

* Déclare tes classes Seeder dans le dossier server/database/fixtures.
* Exécute tes fixtures avec la commande npm run db:seed.
* Le système de "refs" te permet de gérer les clés étrangères dans tes fixtures.

## 08 - Harmonia : Mettre en place un CRUD / BREAD
### Résumé

À ce stade, tu as mis en place un CRUD / BREAD complet pour gérer les catégories de ton application. Tu as appris les conventions REST, configuré CORS, activé le parsing de JSON, et implémenté chaque opération avec une structure cohérente entre le client et le serveur.

Voici un récapitulatif des opérations effectuées :

1.Browse : Récupérer et afficher la liste des ressources.
2.Add : Ajouter une nouvelle ressource.
3.Read : Lire et afficher les détails d'une ressource spécifique.
4.Edit : Modifier une ressource existante.
5.Destroy : Supprimer une ressource existante.

## 09 - Harmonia : Validation
### Résumé

Dans cette quête, tu as appris l'importance de la validation des données saisies par l'utilisateur et comment la mettre en œuvre dans ton application Express en utilisant des middlewares. Tu as également vu comment implémenter une validation manuelle et comment utiliser des bibliothèques tierces pour faciliter ce processus.

La validation des données est essentielle pour garantir la sécurité et la cohérence des informations traitées par ton application.

## License
[WildCodeSchool](https://www.wildcodeschool.com/fr-fr/)

__________________________________________

# wild-series

This project uses Harmonia. Harmonia is a framework meant to serve as a foundation for every project following the React-Express-MySQL stack, as learned in Wild Code School.
It's pre-configured with a set of tools which'll help students produce industry-quality and easier-to-maintain code, while staying a pedagogical tool.

## Setup & Use

**Windows users:** be sure to run these commands in a git terminal to avoid [issues with newline formats](https://en.wikipedia.org/wiki/Newline#Issues_with_different_newline_formats):

```
git config --global core.eol lf
git config --global core.autocrlf false
```

- In VSCode, install plugins **Prettier - Code formatter** and **ESLint** and configure them
- Clone this repo, enter it
- Run command `npm install`
- Create environment files (`.env`) in both `server` and `client`: you can copy `.env.sample` files as starters (**don't** delete them)

### Available Commands

- `db:migrate` : Run the database migration script
- `db:seed` : Run the database seed script
- `dev` : Starts both servers (client + server) in one terminal
- `dev:client` : Starts the React client
- `dev:back` : Starts the Express server
- `lint` : Runs validation tools (will be executed on every _commit_, and refuse unclean code)

## FAQ

### Tools

- _Concurrently_ : Allows for several commands to run concurrently in the same CLI
- _Husky_ : Allows to execute specific commands that trigger on _git_ events
- _Vite_ : Alternative to _Create-React-App_, packaging less tools for a more fluid experience
- _ESLint_ : "Quality of code" tool, ensures chosen rules will be enforced
- _Prettier_ : "Quality of code" tool as well, focuses on the styleguide
- _ Airbnb Standard_ : One of the most known "standards", even though it's not officially linked to ES/JS

## Deployment with Traefik

> ⚠️ Prerequisites : You must have installed and configured Traefik on your VPS beforehand.
> https://github.com/WildCodeSchool/vps-traefik-starter-kit/

For deployment, you have to go to `secrets` → app `actions` on the github repo to insert via `New repository secret` :

- SSH_HOST : IP address of your VPS
- SSH_USER : SSH login to your VPS
- SSH_PASSWORD : SSH connection password to your VPS

And a public variable from the tab `/settings/variables/actions` :

- PROJECT_NAME : the name of the project used to create the subdomain.

> ⚠️ Warning : underscores are not allowed. They can cause trouble with the let's encrypt certificate

Use this same tab to add the other environment variables required for the project if any.

Only the server will be accessible. The root path `"/"` will redirect to the dist folder of your client. In order to allow that, please uncomment the line as explained in `server/src/app.js` (Line 102).
Because the server will also serve the client, the global variable VITE_SERVER_URL will be set with an empty string.

Your url will be ` https://${PROJECT-NAME}.${subdomain}.wilders.dev/`.

### About the database

The database is automaticaly deployed with the name of your repo. During the build of the projet (`docker-entry.sh`), the `node migrate.js` command is executed in the server. If you want to seed automaticaly your database using the `seed.js` script, replace the `cd ./server && node ./bin/migrate.js && node index.js` by `cd ./server && node ./bin/migrate.js && node ./bin/seed.js && node index.js`

### About public assets (pictures, fonts...)

Don't use any public folder on your client. This folder won't be accessible online. You may move your public assets in the `server/public` folder. Prefer [static assets](https://vitejs.dev/guide/assets) when possible.

### About Specific Environment Variables (e.g., Email)

Students should use the template provided in the `*.env.sample*` file as `<PROJECT_NAME><SPECIFIC_NAME>=<THE_VARIABLE>`.

> ⚠️ **Warning:** The `PROJECT_NAME` should match the one used in the Git public variable.

To add it during deployment, follow these 2 steps:

- Add the following variable to the `docker-compose.prod.yml` file (as shown in the example: `PROJECT_NAME_SPECIFIC_NAME: ${PROJECT_NAME_SPECIFIC_NAME}`).
- Connect to your server via SSH. Open the global `.env` file in Traefik (`nano ./traefik/data/.env`). Add the variable with the correct value and save the file.
- Afterward, you can initiate automatic deployment. Docker will not refresh during this process.

### About Logs

If you want to access the logs of your online projet (to follow the deployement or to watch any bug error), connect to your VPS (`ssh user@host`).
Then, go on your specific project and run  `docker compose logs -t -f`.
=======
