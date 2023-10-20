

Ce projet implémente un pipeline Jenkins pour la construction et le déploiement d'une application Docker. Le pipeline prend en charge la création d'une image Docker, le déploiement de conteneurs, les tests d'image, le déploiement sur des environnements de staging et de production, et envoie des notifications Slack en cas de succès ou d'échec.

### Inntroduction

Dans le contexte de ce projet, une architecture Docker a été conceptualisée pour faciliter le déploiement et la gestion de l'application. L'application se compose de deux modules principaux : une API REST et un frontend en PHP/HTML. Deux réseaux Docker distincts ont été créés pour isoler les composants de l'application.

### Plan d'action
Le pipeline Jenkins suit les étapes suivantes :

## Étape 1: Build de l'image Docker

Cette étape génère une image Docker pour l'application en utilisant le Dockerfile spécifié.
La commande docker build est utilisée pour créer l'image avec un tag correspondant.

## Étape 2: Exécution du conteneur basé sur l'image construite
Un conteneur Docker est lancé en utilisant l'image construite précédemment.
Avant cela, tout conteneur existant portant le même nom est nettoyé.
Le conteneur est démarré en associant le port exposé de l'application à un port interne.
Étape 3: Test de l'image Docker
Un test est effectué en interrogeant l'application à l'aide de la commande curl.
Le test vérifie si l'application répond comme prévu.
Étape 4: Nettoyage du conteneur
À la fin du test, le conteneur est stoppé et supprimé pour maintenir un environnement propre.
Étape 5: Login et Push de l'image sur Docker Hub
Cette étape consiste à s'authentifier sur Docker Hub en utilisant les informations d'identification sécurisées stockées dans Jenkins.
Ensuite, l'image Docker est poussée sur Docker Hub pour le stockage.
Étape 6: Déploiement sur STAGING
L'application est déployée sur un environnement de staging en utilisant une requête HTTP vers un endpoint spécifique.
Les détails de déploiement sont stockés dans un fichier JSON.
Étape 7: Déploiement sur PRODUCTION
L'application est déployée sur un environnement de production uniquement si la branche Git est 'origin/master'.
Les détails de déploiement sont également stockés dans un fichier JSON.
Notifications Slack
En cas de succès, une notification Slack verte est envoyée, indiquant le succès de la construction et du déploiement.
En cas d'échec, une notification Slack rouge est envoyée pour informer de l'échec du pipeline.
Vous pouvez personnaliser ce README en fonction de vos besoins spécifiques et ajouter des détails supplémentaires sur l'application et le pipeline Jenkins.
