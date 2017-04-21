# Récupération des détails d'une livraison
Cette API permet de récupérer les détails d'une livraison.

## URL
```
GET https://cloud.comptoirurbain.com/api/v1/order/ORDER_REFERENCE
```

## Requête
*Cette API ne nécessite pas de body*

## Réponse
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