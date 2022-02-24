# API WEB : Openrouteservice

## I] API

API signifie "Application Programming Interface". En d'autres termes, c'est un moyen mis en place par une application pour que d'autres applications puissent intéragir simplement avec elle. Tout comme les bibliothèques, il existe de très nombreuses API. Nous allons nous intéresser plus particulièrement l'API Openrouteservice. Il s'agit d'un service de routage basé sur les données ouvertes OpenStreetMap.

Voici l'adresse du site :  https://openrouteservice.org

## II] Utilisation de l'API

Prenons un exemple de la vie courante : "Nous cherchons un appartement situé à chaumont situé à moins de 30 minutes à pieds du centre". Pour cela, nous allons tracer des isochrones sur une plage de 5 min à partir de la mairie.

**Remarque** : une isochrone est une ligne situé à une distance ou à un temps donné d'un point origine  

Dans un premier temps, on peut se familiariser avec les fonctionnalités disponibles sur le site  internet proposant l'API. 

![](2022-02-20%2015.09.39%20openrouteservice.org%2093926522676b.png)

Le menu à gauche permet de saisir et d'exploiter différents options.
Pour poursuivre , il faut créer un compte sur le site afin d'obtenir une clé permettant d'utiliser l'API.
Maintenant, il faut se familiariser directement avec les paramètres de l'API via l'interface suivante : 

https://openrouteservice.org/dev/#/api-docs/v2/isochrones/%7Bprofile%7D/post 

Après avoir analysé tout cela,et notamment la rubrique "Show example code", et sélectionné la catégorie Python, on s'aperçoit qu'on peut utliser cette API. 

Effectivement le programme python envoie un formulaire HTML contenant les paramètres fixés dans un fichier qui ressemble à un dictionnaire qui est en fait un fichier JSON. Une fois ce formulaire envoyé, on obtient en retour  une réponse également sous la forme de données JSON.  

Il faut donc être capable d'envoyer une requête HTML. Pour cela, on va utiliser le module *requests*.

 Si on souhaite avoir un retour visuel avec en fond de carte, les données d'OpenStreetMap. Nous utiliserons pour cela la bibliothèque *folium*. 

Commençons donc par installer ces modules et bibliothèque.

```python
pip install folium
pip install requests
```

Maintenant copier le programme suivant dans votre éditeur:

```python
import json
import folium
import requests


tab_couleurs=["#0e7c0a","#c1ff00","#e1d219","#e1ba19","#e17d19","#ff0000"]

# adresse de la mairie de Chaumont
coord_depart = (48.111006, 5.139613)

temps_max = 1800 #soit 30 min

intervalle_temps = 300 #soit 5 min

#l'API utilise des coordonnées avec la longitude avant la latitude 
coord = [coord_depart[1],coord_depart[0]]

body = {"locations":[coord],
        "range":[temps_max],
        "attributes":["area"],
        "interval":intervalle_temps,
        "location_type":"start",
        "range_type":"time"
        ,"area_units":"m"}

headers = {
    'Accept': 'application/json, application/geo+json, application/gpx+xml, img/png; charset=utf-8',
    'Authorization': 'yourToken',
    'Content-Type': 'application/json; charset=utf-8'
}
call = requests.post('https://api.openrouteservice.org/v2/isochrones/foot-walking',
                     json=body, headers=headers)

print(call.status_code, call.reason)
print(call.text)
geo=call.text


with open('datas.json','w') as f:
    f.write(geo)

with open('datas.json','r') as f:
    datas=json.load(f)

folium_map = folium.Map(location=coord_depart,zoom_start=14)
folium.Marker(coord_depart,popup="Mairie").add_to(folium_map)

i=0

for zone in datas["features"]:
    valeur_tps = zone["properties"]["value"]
    print(valeur_tps)
    path_list=[(y,x) for x,y in zone["geometry"]["coordinates"][0]]
    folium.Polygon(path_list,color=tab_couleurs[i]).add_to(folium_map)
    i=i+1
folium_map.save('map.appart.html')
```

![](Capture%20d’écran%202022-02-20%20à%2015.17.59.png)

## III] Exercices

Réaliser les deux exercices suivants sous Jupyter tout en justifiant les parties de code.

1. Rechercher les isochrones autour du lycée situé à 40 min et par pas de 10 min.

2. Ensuite, utiliser l'API d'une autre manière qu'avec les isochrones.
