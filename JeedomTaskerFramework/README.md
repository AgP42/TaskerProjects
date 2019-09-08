# Présentation

Ce projet consiste à creer une base (un framework) pour aider vos projets Tasker en lien avec le solution domotique Jeedom.

Ce Framework se focalise sur la communication Tasker -> Jeedom
Pour la communication Jeedom -> Tasker, vous pouvez utiliser le plugin TaskerAutoRemote [Doc plugin TaskerAutoRemote](https://agp42.github.io/Jeedom-TaskerAutoremote/fr_FR/)

# Liens

[Faire des widget Zooper avec retour d'état](http://www.touteladomotique.com/index.php?option=com_content&view=article&id=1841:tuto-faire-des-widgets-avec-retour-detat-jeedom-zooper&catid=5:domotique&Itemid=89)

[Receive featured notification from AutoRemote](https://forum.joaoapps.com/index.php?resources/tutorial-receive-featured-notifications-from-your-home-automatisation-system.393/)

[Dynamic widgets with Zooper or KWGT using AutoRemote](https://forum.joaoapps.com/index.php?resources/tutorial-display-dynamically-widgets-kwgt-or-zooper-according-to-autoremote-messages.395/)

[Tutoriel Jeedom sur le pilotage à la voix utilisant AutoVoice](https://jeedom.github.io/documentation/howtoadvance/fr_FR/android.autovoice)

[La documentation officielle de l'API HTTP, sur laquelle est basé le framework](https://jeedom.github.io/core/fr_FR/api_http)

# Installation

Télécharger le fichier suivant sur votre appareil ayant Tasker installé : TOOOOODDDOOOOOOOO

# Utilisation 

## General - Initialisation

Avant de pouvoir utiliser le framework il faut l'initialiser en lancant la tache "Config - A lancer !" qui vous demandera l'adresse IP de votre Jeedom ainsi que votre clé API.
Elle se trouve dans le menu “Général” (en haut à droite, le logo engrenage) → “Configuration” → onglet “API” puis prendre la clef API globale de Jeedom.

![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/20190908_170639.jpg?raw=true)
![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/20190908_170658.jpg?raw=true)

Vous pouvez aussi dans cette tâche changer le "PopUpActifs" à 0 si vous ne voulez pas les pop up d'information sur les commandes envoyés et les retours associés.

## Commande d'un scénario

### Extrait de la doc Jeedom 
Scénario

Voici l’URL = http://#IP_JEEDOM#/core/api/jeeApi.php?apikey=#APIKEY#&type=scenario&id=#ID#&action=#ACTION#

- id : correspond à l’id de votre scénario. L’ID se trouve sur la page du scénario concerné, dans “outils” → “Scénarios”, une fois le scénario sélectionné, à côté du nom de l’onglet “Général”. Autre moyen de le retrouver : dans “Outils” → “Scénarios”, cliquez sur “Vue d’ensemble”.

- action : correspond à l’action que vous voulez appliquer. Les commandes disponibles sont : “start”, “stop”, “désactiver” et “activer” pour respectivement démarrer, arrêter, désactiver ou activer le scénario.

- tags [optionnel] : si l’action est “start”, vous pouvez passer des tags au scénario (voir la documentation sur les scénarii) sous la forme tags=toto%3D1%20tata%3D2 (à noter que %20 correspond à un espace et %3D à = )

### Utilisation dans le framework tasker

1. Appel d'un scenario via une tâche : voir la tâche « AppelScenarioTache » d’exemple. Donner en parametre1 l’id du scenario et en parametre2 l’action voulue. Et vous pouvez récuperer le retour de Jeedom dans le champ « Variable de valeur de retour ». Une variable en minuscule sera « locale », en majuscule elle sera globale et disponible partout (convention Tasker).

2. Par un appel via : 
   - une command « AutoAppsHub »
   - un « Direct message » via une appli de widget (Zooper, KWGT, …)
   - un message AutoRemote
   - une notification AutoRemote avec une action associée (à la réception, au clic, liée à un bouton, …)
   - probablement plein d’autres trucs capables d’envoyer une « commande autoapp »

Envoyer « apiscenario=:=#id#=:=#action# »

Par exemple : « apiscenario=:=91=:=start ». Voir l’exemple dans la tâche « AppelScenarioCommand »

Il n’y a pas de retour d’info (il faut demander a Jeedom de vous envoyer une confirmation via AutoRemote si besoin).
