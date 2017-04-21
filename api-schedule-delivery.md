# Planification de livraisons

Cette API permet de confirmer une planification de livraison dans un comptoir donné.

## URL
```
POST https://cloud.comptoirurbain.com/api/v1/order
```

## Requête

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

## Réponse
Cette API renvoie les détails de la livraison planifiée.

```json
{    
    "reference": "ORDER_REFERENCE",
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
        "collectedDate": null,
        "deliveredDate": null,
        "deliveryCode": "123456",        
        "collectingCode": "123456",
        "size": "S",
        "temperture": "FRESH"
    }, {        
        "collectedDate": null,
        "deliveredDate": null,
        "deliveryCode": "123456",        
        "collectingCode": "123456",
        "size": "M",
        "temperture": "FRESH"
    }]
}
```