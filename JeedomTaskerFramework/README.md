# Présentation

Ce projet consiste à créer une base (un framework) pour aider vos projets Tasker en lien avec la solution domotique Jeedom.

Ce Framework se focalise sur la communication Tasker -> Jeedom

Pour la communication Jeedom -> Tasker, vous pouvez utiliser le plugin TaskerAutoRemote [Doc plugin TaskerAutoRemote](https://agp42.github.io/Jeedom-TaskerAutoremote/fr_FR/)

Pré-requis : 

- Tasker

- AutoTools (pour lire du JSON - uniquement pour les lectures multiples des Info/Action)

- AutoRemote pour recevoir des messages et notifications push de votre Jeedom (avec le plugin TaskerAutoRemote)

- [ AutoVoice (pour envoyer des messages via "interaction" à Jeedom) ]

# Liens

[Faire des widget Zooper avec retour d'état](http://www.touteladomotique.com/index.php?option=com_content&view=article&id=1841:tuto-faire-des-widgets-avec-retour-detat-jeedom-zooper&catid=5:domotique&Itemid=89) - Ancien mais détaillé

[Dynamic widgets with Zooper or KWGT using AutoRemote](https://forum.joaoapps.com/index.php?resources/tutorial-display-dynamically-widgets-kwgt-or-zooper-according-to-autoremote-messages.395/) - Une mise à jour du tuto ci-dessus incluant l'appli de widget KWGT (en anglais)

[Receive featured notification from AutoRemote](https://forum.joaoapps.com/index.php?resources/tutorial-receive-featured-notifications-from-your-home-automatisation-system.393/) - Tuto dédié à la reception de notifications par Jeedom (ou tout autre systéme domotique) (en anglais)

[Une interface de thermostat pour Tasker (AutoTools Web Screen)](https://github.com/AgP42/TaskerProjects/tree/master/AutoTools%20Web%20Screen/thermostat)

[La documentation officielle de l'API HTTP, sur laquelle est basé le framework](https://jeedom.github.io/core/fr_FR/api_http)

# Installation

1. Via TasketNet : 

a partir de votre appareil android ayant Tasker installé, cliquez sur ce lien pour charger le projet : [Framework Jeedom Tasker](https://taskernet.com/shares/?user=AS35m8kzmjsXFX0uPzJ%2Fne2qdLmlS2IhQiOVk%2FrAPxMTVSe%2BPHGS7URbKododS1jIWbmQzkGZyG7%2Bw%3D%3D&id=Project%3AFramework)

2. En XML : 

Télécharger le fichier suivant et importez le dans Tasker (clic long dans la barre du bas puis "Importer un projet") : [Framework Jeedom Tasker xml](https://raw.githubusercontent.com/AgP42/TaskerProjects/master/JeedomTaskerFramework/Framework.prj.xml)

# Utilisation 

## General - Initialisation

Avant de pouvoir utiliser le framework il faut l'initialiser en lancant la tache "Config - A lancer !" qui vous demandera l'adresse IP de votre Jeedom ainsi que votre clé API.
La clef API se trouve dans le menu “Général” (en haut à droite, le logo engrenage) → “Configuration” → onglet “API” puis prendre la clef API globale de Jeedom.

![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/20190908_170639.jpg?raw=true)
![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/20190908_170658.jpg?raw=true)

Vous pouvez aussi dans cette tâche changer le "PopUpActifs" à 0 si vous ne voulez pas les pop up d'information sur les commandes envoyés et les retours associés.

![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/A%20lancer.jpg?raw=true)

![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/overview-tasks.jpg?raw=true)

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

## Info/Action commande
### Extrait de la doc Jeedom 
Voici l’URL = http://#IP_JEEDOM#/core/api/jeeApi.php?apikey=#APIKEY#&type=cmd&id=#ID#

•	id : correspond à l’id de ce que vous voulez piloter ou duquel vous souhaitez recevoir des informations
Le plus simple pour avoir cette URL est d’aller sur la page Outils → Résumé domotique, de chercher la commande puis d’ouvrir sa configuration avancée (l’icône “engrenage”) et là, vous allez voir une URL qui contient déjà tout ce qu’il faut en fonction du type et du sous-type de la commande.

Note

Il est possible pour le champs #ID# de passer plusieurs commandes d’un coup. Pour cela, il faut passer un tableau en json (ex %5B12,58,23%5D, à noter que [ et ] doivent être encodés d’où les %5B et %5D). Le retour de Jeedom sera un json

Note

Les paramètres doivent être encodés pour les url, Vous pouvez utiliser un outil, [ici](https://meyerweb.com/eric/tools/dencoder/)

### Utilisation dans le framework tasker

##### Pour une commande unique :

1.	Par une tâche : voir la tâche « AppelInfoActionCmdTache » d’exemple. Donner en parametre1 l’id de la commande voulue. Et vous pouvez récupérer le retour de Jeedom dans le champ « Variable de valeur de retour ». (Pour les « info », correspondra à la valeur de la variable Jeedom.

2.	Par un appel via : une « commande autoapp »

Envoyer « apiinfoactioncmd=:=#id# »

Par exemple : « apiinfoactioncmd =:=506 ». Voir l’exemple dans la tâche « AppelScenarioCommand ». Il n’y a pas de retour d’info, donc a n’utiliser que pour les actions.

##### Pour des commandes multiples :

pas de tache toute faite à utiliser, mais un exemple donné dans « InfoActionMultiple » et qui utilise le module Tasker « AutoTools » pour lire le json renvoyé par Jeedom. 

![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/InfoActionMultiples.jpg?raw=true)

Pour l’utiliser : 

1. A personnaliser : définir les commandes Jeedom que vous voulez lire dans un tableau, séparés par des virgules et aucun espace ! (Vous pouvez aussi les donner directement dans les étapes 2 et 3 sans passer par un tableau intermédiaire.

2. faire la requête à Jeedom avec la liste des commandes

3. lire le JSON, il y a là 2 champs à personnaliser : 
•	« Fields » qui doit être exactement identique à la liste donnée à l’étape précédente
•	« Advanced » / «Variable Name » : c’est le nom à donner aux variables qui vont contenir les infos renvoyées par Jeedom. Par défaut Tasker assigne le nom de « Field », c’est-à-dire ici (dû à Jeedom) des chiffres. Sauf que Tasker n’aime pas avoir des variables dont le nom est un chiffre, donc dans notre cas il faut les définir à la main…
![](https://github.com/AgP42/TaskerProjects/blob/master/JeedomTaskerFramework/img/json.jpg?raw=true)

4. Vous pouvez ensuite garder vos variables individuelles ou les regrouper sous un tableau

## Interactions

Voir ce tuto sur la doc officielle jeedom : [Tutoriel Jeedom sur le pilotage à la voix utilisant AutoVoice](https://jeedom.github.io/documentation/howtoadvance/fr_FR/android.autovoice)
