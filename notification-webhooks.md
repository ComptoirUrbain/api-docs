# Webhooks
Les partenaires à qui l'option WebHook est activée, et pour laquelle une URL a été fournie, recevront en PUSH, les mises à jour de l'état de chaque livraison planifiée:
* Livraisons annulées
* Colis déposés
* Colis retirés

## Appel du WebHook
L'appel se fait par simple requête HTTP en POST, où le body de la requête est un JSON décrivant la commande en question:

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
        "temperture": "FRESH"
    }, {        
        "collectedDate": null,
        "deliveredDate": 1481202477000,
        "deliveryCode": "123456",                
        "collectingCode": "123456",
        "size": "M",
        "temperture": "FRESH"
    }]
}
```

Notons que c'est bien la même structure de données qui est retournée par l'API de récupération de détails d'une livraison de commande
