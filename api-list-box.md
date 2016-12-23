## Lister les comptoirs

Cette API permet de lister les comptoirs disponibles autour d'une position GPS (latitude, longitude).

#### URL
```
POST http://sandbox.comptoirurbain.com/api/v1/box
```

#### Requête
Un objet JSON décrivant la position GPS autour de laquelle la recherche de comptoirs doit s'effectuer

```json
{
    "latitude": 48.8416835,
    "longitude": 2.2761939,
    "distance": 5 // Distance en Kilometres, 0 pour pas limiter la liste à un rayon donné
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
        "distance": 0.5655,        
        "address": "2 rue Cambronne",
        "zipcode": "75015",
        "city": "Paris",
        "country": "FR",
        "lockers": [{
            "size": "M",
            "count": 19,
            "temperture": "FRESH",
            "height": 40,
            "width": 30,
            "depth": 43
        }, {
            "size": "S",
            "count": 30,
            "temperture": "FRESH",
            "height": 22,
            "width": 30,
            "depth": 43
        }],
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
- **404** si aucun comptoir n'a été trouvé dans un rayons de `distance` km

#### Exemple d'appel

```bash
curl -XPOST -H "Api-Key=XXXXXX" \
            -H "Content-Type=application/json" \
            http://sandbox.comptoirurbain.com/api/v1/box \
            -d '{"latitude": 48.8416835, "longitude": 2.2761939}'
```