# Documentation (DRAFT)

Ce document liste l'ensemble des APIs publiques disponibles sur la plateform ComptoirUrbain. Toutes ces APIs nécessitent une authentification par **API Key**.  

Chaque partenaire de ComptoirUrbain, qui active l'utilisation des APIs, doit générer, via l'interface du service ComptoirUrbain, une API Key permettant d'authentifier les appels d'APIs.

## Obtenir un API Token

Une fois connecté sur l'interface graphique du service ComptoirUrbain, le partenaire peut générer une API Key. Cette API Key doit être fournie dans n'importe quel appel d'API REST sous forme d'un header HTTP nommé `Api-Key`

Exemple:
```bash
curl -H "Api-Key=XXXXXX" http://api.comptoirurbain.com/api/v1/box"
```

Où `XXXXXX` est l'API Key générée via l'interface



## Lister les comptoirs

Cette API permet de lister les comptoirs disponibles autour d'une position GPS (latitude, longitude).

#### URL
```
POST https://api.comptoirurbain.com/api/v1/box
```

#### Requête
Un objet JSON décrivant la position GPS autour de laquelle la recherche de comptoirs doit s'effectuer

```json
{
    "latitude": 48.8416835,
    "longitude": 2.2761939
}
```

#### Réponse
Cette API retourne la liste des comptoirs ordonnés par distance de la position fournie en entrée. La liste retourne le comptoir le plus proche en premier.  

```json
[
    {
        "reference": "10045",
        "latitude": 48.8470573,
        "longitude": 2.3013761,
        "status": "ACTIVE",
        "address": "2 rue Cambronne",
        "zipcode": "75015",
        "city": "Paris",
        "country": "FR",
        "lockers": [
            {
                "size": "S",
                "count": 12,
                "type": "FRESH"
            },
            {
                "size": "M",
                "count": 7,
                "type": "FRESH"
            }
        ],
        "openinghours": {
            "monday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "tuesday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "wednesday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "thursday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "friday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "saturday": [{
                "from": "00:00",
                "to": "23:59"
            }],
            "sunday": [{
                "from": "00:00",
                "to": "23:59"
            }]
        }
    }
]
```

Le statut HTTP de cette API est:
- **200** en code de succès de l'appel
- **404** si aucun comptoir n'a été trouvé dans un rayons de XXX km

#### Exemple d'appel

```bash
curl -XPOST -H "Api-Key=XXXXXX" \
            -H "Content-Type=application/json" \
            http://api.comptoirurbain.com/api/v1/box \
            -d '{"latitude": 48.8416835, "longitude": 2.2761939}'
```


## Récupération des disponibilités de casiers

Cette API permet de retourner l'état des disponibilités de casiers sur une durée de 7 jours à partir de la date courante, avec 4 créneaux horaires par jours:
- Entre 00:00 et 06:00
- Entre 06:00 et 12:00
- Entre 12:00 et 18:00
- Entre 18:00 et 00:00

#### URL
```
POST https://api.comptoirurbain.com/api/v1/locker
```

#### Requête
Un objet JSON décrivant la demande de disponibilités:
- quel comptoir (identifié par sa référence)
- combien de cases par taille et type

```json
{
    "reference": "<REFERENCE_COMPTOIR>",
    "lockers": [
        {
            "size": "S",
            "type": "FRESH",
            "count": 1
        },
        {
            "size": "M",
            "type": "FRESH",
            "count": 2
        }
    ]
}
```

#### Réponse
Cette API retourne pour chaque jour, quel créneaux peut être utilisé pour livrer.

```json
{
    "01.12.2016": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-12": true,
    },    
    "02.12.2016": {
        "0-6": true,
        "6-12": false,
        "12-18": false,
        "18-12": false,
    },
    "03.12.2016": {
        "0-6": false,
        "6-12": false,
        "12-18": true,
        "18-12": true,
    },
    "04.12.2016": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-12": true,
    }    
}
```

## Planification de livraisons

Cette API permet de confirmer une planification de livraison dans un comptoir donné.

#### URL
```
POST https://api.comptoirurbain.com/api/v1/order
```

#### Requête

```json
{    
    "station": "REFERENCE_COMPTOIR",
    "reference": "ORDER_REFERENCE",
    "firstname": "John",
    "lastname": "Doe",
    "email": "john@doe.com",
    "phone": "+3300000000",
    "notes": "Remarques optionnelles concernant la livraison",
    "timeslot": 12,
    "deliveryDate": "08.12.2016",
    "booking": [{
        "temperature": "FRESH",
        "size": "s",
        "count": 1
    }, {
        "temperature": "FRESH",
        "size": "m",
        "count": 1
    }]
}
```

#### Réponse
Cette API renvoie les détails de la livraison planifiée.

```json
{    
    "orderRefrence": "ORDER_REFERENCE",
    "status": "ASSIGNED",    
    "box": {        
        "reference": "10045",
        "address": "2 rue Cambronne",
        "zipcode": "75015",
        "city": "Paris",
        "country": "FR"        
    },        
    "firstname": "John",
    "lastname": "Doe",
    "email": "john@doe.com",
    "phone": "+33000000000",
    "notes": "Test",
    "deliveryStartDate": 1481194800000,
    "deliveryEndDate": 1481216400000,
    "collectingStartDate": 1481216400000,
    "collectingEndDate": 1481302800000,
    "created": 1481198136602,
    "deliveries": [{        
        "status": "ASSIGNED",
        "collectedDate": null,
        "deliveredDate": null,
        "deliveryCode": "123456",        
        "size": "M",
        "tempertureType": "FRESH"
    }, {        
        "status": "ASSIGNED",
        "collectedDate": null,
        "deliveredDate": null,
        "deliveryCode": "123456",                
        "size": "M",
        "tempertureType": "FRESH"
    }]
}
```

## Récupération des détails d'une commande
Cette API permet de récupérer les détails d'une livraison.

#### URL
```
GET https://api.comptoirurbain.com/api/v1/order/ORDER_REFERENCE
```

#### Requête
*Cette API ne nécessite pas de body*

#### Réponse
```json
{    
    "orderRefrence": "ORDER_REFERENCE",
    "status": "DELIVERED",    
    "box": {        
        "reference": "10045",
        "address": "2 rue Cambronne",
        "zipcode": "75015",
        "city": "Paris",
        "country": "FR"        
    },        
    "firstname": "John",
    "lastname": "Doe",
    "email": "john@doe.com",
    "phone": "+33000000000",
    "notes": "Test",
    "deliveryStartDate": 1481194800000,
    "deliveryEndDate": 1481216400000,
    "collectingStartDate": 1481216400000,
    "collectingEndDate": 1481302800000,
    "created": 1481198136602,
    "deliveries": [{        
        "collectedDate": null,
        "deliveredDate": 1481202477000,
        "deliveryCode": "123456",        
        "collectingCode": "123456",
        "size": "S",
        "tempertureType": "FRESH"
    }, {        
        "collectedDate": null,
        "deliveredDate": 1481202477000,
        "deliveryCode": "123456",                
        "collectingCode": "123456",
        "size": "M",
        "tempertureType": "FRESH"
    }]
}
```

## Webhooks
TODO
