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

Vous pouvez aussi dans cette tâche changer le "PopUpActifs" à 0 si vous ne voulez pas les pop up d'information sur les commandes envoyés et les retours associés.

## Commande d'un scénario

### Extrait de la doc Jeedom 
