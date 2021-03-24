# 911 Calls avec ElasticSearch

## Import du jeu de données

Pour importer le jeu de données, complétez le script `import.js` (ici aussi, cherchez le `TODO` dans le code :wink:).

Exécutez-le ensuite :

```bash
npm install
node import.js
```

Vérifiez que les données ont été importées correctement grâce au shell (le nombre total de documents doit être `153194`) :

```
GET <nom de votre index>/_count
```

## Requêtes

À vous de jouer ! Écrivez les requêtes ElasticSearch permettant de résoudre les problèmes posés.

```
Du à des problèmes techniques indépendants de notre volonté, cette base de donnée (911-calls) est la seule que nous avons pu traiter au cours de la journée. 

Clément a passé toute son après-midi à débugguer neo4j au niveau de l'installation, et nous avons fini par établir avec vous qu'on ne pouvait rien y faire. 

Désolé et merci de votre aide précieuse ! :)

Nombre d'appels par catégorie:
GET /calls/_search 
  {"size": 0, 
  "aggs": 
    {"category": 
      {"terms": 
        {"field": "category.keyword"}}}}

Les trois mois ayant le plus d'appels:
GET /calls/_search
{
  "size": 0,
  "aggs": {
    "month": {
      "terms": {
        "field": "month",
        "size": 3,
        "order": {
          "_count": "desc"
        }
      }
    }
  }
}

Requete des villes de la drogue:
GET /calls/_search
{
  "query": {
    "term": {
      "title.keyword": {
        "value": "EMS: OVERDOSE"
      }
    }
  },
  "size": 0,
  "aggs": {
    "twp": {
      "terms": {
        "field": "twp.keyword",
        "size": 3,
        "order": {
          "_count": "desc"
        }
      }
    }
  }
}

Requete des villes à 500m de Lansdale:
GET /calls/_count
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      },
      "filter": {
        "geo_distance": {
          "distance": "500m",
          "loc": [
            -75.283783,
            40.241493
          ]
        }
      }
    }
  }
}
```

## Kibana

Dans Kibana, créez un dashboard qui permet de visualiser :

* Une carte de l'ensemble des appels
* Un histogramme des appels répartis par catégories
* Un Pie chart réparti par bimestre, par catégories et par canton (township)

Pour nous permettre d'évaluer votre travail, ajoutez une capture d'écran du dashboard dans ce répertoire [images](images).

### Bonus : Timelion
Timelion est un outil de visualisation des timeseries accessible via Kibana à l'aide du bouton : ![](images/timelion.png)

Réalisez le diagramme suivant :
![](images/timelion-chart.png)

Envoyer la réponse sous la forme de la requête Timelion ci-dessous:  

```
TODO : ajouter la requête Timelion ici
```
