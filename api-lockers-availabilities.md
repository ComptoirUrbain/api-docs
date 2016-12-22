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
[{
    "date": "22-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": false
    }
}, {
    "date": "23-12-2016",
    "availabilities": {
        "0-6": false,
        "6-12": false,
        "12-18": false,
        "18-0": false
    }
}, {
    "date": "24-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": true
    }
}, {
    "date": "25-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": true
    }
}, {
    "date": "26-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": true
    }
}, {
    "date": "27-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": true
    }
}, {
    "date": "28-12-2016",
    "availabilities": {
        "0-6": true,
        "6-12": true,
        "12-18": true,
        "18-0": true
    }
}]
```