# Docker-brief-Samantha-Sébastien

## Docker commande de base

* _docker ps_       permet d'afficher les conteneurs en cours d'exécution
* _docker ps -a_    permet d'afficher tous les conteneurs
* _docker images_   permet d'afficher les images existantes  
* _docker pull_     permet de récuperer des images depuis un dépot (de base Docker Hub)   
* _docker start_    permet de démarrer un conteneur
* _docker stop_     permet d'arrêter un conteneur
* _docker inspect_  permet d'inspecter un conteneur et afficher des informations détaillées sur ses propriétés.  

## Docker compose

Docker Compose va nous permettre d'orchestrer nos conteneurs, et ainsi de simplifier nos déploiements sur de multiples environnements. Docker Compose est un outil écrit en Python qui permet de décrire, dans un fichier YAML, plusieurs conteneurs comme un ensemble de services. 

  * _version_  définit la version du fichier yaml en fonction du docker engine utilisé
  * _services_ permet de lister toutes les images utilisées
  
  * Ensuite le détail de chaque image où l'on définit l'image de base utilisée, les volumes, l'environnement, les ports, etc...
  
  Dans l'image wordpress, on a _depends_on_ qui crée le lien avec l'image db.

  ### Exercice

  Une fois le fichier docker-compose.yml écrit, on lance la commande _docker-compose up -d_ qui lance tous les conteneurs définis (mysql et wordpress).
  Afin d'accéder à wordpress, on se place dans un navigateur et on tape l'adresse _localhost:8000_
  8000 étant le port d'entrée pour accéder à wordpress. De plus wordpress est lié à mysql.
  
  
## Dockerfile

le Dockerfile est un fichier qui liste les instructions à exécuter pour build une image. Il est lu de haut en bas au cours du processus de build. On y retrouve cette idée de contexte dont on a parlé avec les images : déplacement dans un dossier, exposition de ports et exécution d'une commande au lancement du conteneur

Pour créer une image Docker, on peut utiliser les instructions suivantes :
  * FROM qui vous permet de définir l'image source ;
  * RUN qui vous permet d’exécuter des commandes dans votre conteneur ;
  * ADD qui vous permet d'ajouter des fichiers dans votre conteneur ;
  * WORKDIR qui vous permet de définir votre répertoire de travail ;
  * EXPOSE qui permet de définir les ports d'écoute par défaut ;
  * VOLUME qui permet de définir les volumes utilisables ;
  * CMD qui permet de définir la commande par défaut lors de l’exécution de vos conteneurs Docker.

  ### Exercice

  On écrit le fichier dockerfile. Dans notre cas :
    on utilise l'image _nginx_ dans sa dernière version comme base
    puis on copy un fichier _index.html_ au bon endroit pour que nginx puisse le retrouver et le lancer.

  On lance la commande  _docker build -t my-nginx ._ afin de créer notre conteneur avec le tag my_nginx

  Puis on lance le conteneur pour voir s'il fonctionne avec
  _docker run -p 8080:80 -v ${PWD}:/usr/share/nginx/html nginx_

  On vérifie sur un navigateur à l'adresse _localhost:8080_


## Dockerhub

Dockerhub permet de stocker des images officielles et personnalisées.

  ### Pousser une image sur dockerhub

    Se connecter sur son terminal avec la commande _docker login_
    Ajouter un tag à l'image qu'on veut pousser sur Docker Hub : _docker tag my-nginx sebastienkusz/my-nginx_
    Pousser l'image dans son repository: _docker push sebastienkusz/mynginx_

  
  ### Récupérer une image sur dockerhub

    Se connecter sur son terminal avec la commande _docker login_
    Récupérer l'image de son repository: _docker pull sebastienkusz/my-nginx_