# Documentation

Ce document liste l'ensemble des APIs publiques disponibles sur la plateforme ComptoirUrbain. Toutes ces APIs nécessitent une authentification par **API Key**.  

Chaque partenaire de ComptoirUrbain, qui active l'utilisation des APIs, doit générer, via l'interface du service ComptoirUrbain, une API Key permettant d'authentifier les appels d'APIs.

Obtenir un API Token
====================

Une fois connecté sur l'interface graphique du service ComptoirUrbain, le partenaire peut générer une API Key. Cette API Key doit être fournie dans tout appel d'API REST sous forme d'un header HTTP nommé `Api-Key`

Exemple:
```bash
curl -H 'Api-Key: XXXXXX' http://sandbox.comptoirurbain.com/api/v1/box
```

Où `XXXXXX` est l'API Key générée via l'interface

Liste des APIs disponibles
==========================

* [Lister les comptoirs](api-list-box.md)
* [Récupération des disponibilités de casiers](api-lockers-availabilities.md)
* [Planification de livraisons](api-schedule-delivery.md)
* [Récupération des détails d'une livraison](api-delivery-details.md)
* [Webhooks de notifications](notification-webhooks.md)