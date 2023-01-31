(j'utililse le markdown javascript pour la coloration des requêtes mongo, y compris dans les exercices)

voir [[Lexique MongoDB]]

mongoDB -> système de base de données orienté objet

stocké dans du json -> pas de structure

désavantage : on se retrouve vite aves des infos dupliquées

avantages : pas de shéma; structure simple en objet; pas de jointure complexe; des requêtes imbriquées et dynamiques, très facile de "scale"; stockage sur disque; pas besoin d'ORM

___

voir : [[JSON]]

mongoDB apporte ses propres types a ceux rencontrés au sein du format JSON standard : 
>- __le type date :__ entier signé de 8 octect représente le nombre de secondes depuis epoch (01/01/1970 00:00:00), le type date ne stocke pas la timezone
>- __le type ObjectID :__ stocke sur 12 octets, utile en interne afin de garantir l'unicité des identifiants auto-générés par la BDD
>- __le type NupberLong et NumberInt :__ par défaut, mongoDB considère que toute valeur numérique est un nombre a virgule code sur 8 octets.
> - __le type NumberDecimal :__ sur 16 octets, le plus précis
>- __le type BinData :__ pour représenter eds caractères qu'on ne peut pas encoder en Utf-8

___

Création de base de données

On peut utiliser `use` pour se connecter a une BDD qui n'existe pas. l'insertion du premier document va entrainer la création de la BDD

```javascript
use tmp
db.uneCollection.insert({"key": "value"})
```
/!\ attention, lors d'un insertMany, il est IMPÉRATIF de mettre toutes les valeurs dans des \[crochets\]!! /!\

on peut effectuer la requête :

```js
db.uneCollection.find()

db.uneCollection.find().pretty()
```

on obtient un résultat du type : 

```json
{
	"_id":ObjectId("5d12edfd09ffef"),
	"key": "value"
}
```

on remarque l'utilisation du mot clé `db` il s'agit d'un mot clé qui renvoie vers la base de données en cours d'utilisation 
La combinaison `db.uneCollection` constitue ce qu'on appelle `namespace` en mongoDB

___

Suppression d'une base de données : 

```js
use maDb
db.dropDatabase()
```

pour vérifier, utilisez la commande :

Affichez l’identifiant pour les salles dont l’identifiant est pair ou le cha
```sh
show dbs
```

afin de lister les bases de données.

___

mongoDB met a disposition des commandes de type 'helper'

`runCommand()
`adminCommand()

pour créer une collection, il suffit l'entrer : 

```js
db.createCollection("maCollection")
```


pour update une collection, il suffit l'entrer : 

```js
db.collection.updateOne(<filtre>, <modification>)

db.personnes.updateOne(
	{
		"nom": "PEYRACHON"
	},
	{
		$set : { "nom": "BARRAY" }
	}
)
```

___

les méthodes find et findOne ont la même signature et permettent d'effectuer des requêtes mongoDB

```js
db.collection.find(<requete>, <projection>)
```

chacun de ces deux paramètres sont tous deux des documents

```js
DBQuerry.shellBatchSize = 40
```

mongorc.js est un fichier de config qui se trouve a la racine du répertoire utilisateur
/home/userName


par exemple, pour limiter le nombre de résultat a 5, on fait :

```js
db.maCollection.find.limit(12)
```

___

__Indexation : __

L'indexation simple : 

```js
db.collection.createIndex(<champ_et_type>, <options>)
```



db : `db.personnes.insert({"nom": "Durand", "prenom": "René", "interets": ["jardinage", "bricolage"], "age": 77},  {"nom": "Durand", "prenom": "Gisèle", "interets": ["bridge", "cuisine"], "age": 75},  {"nom": "Dupont", "prenom": "Gaston", "interets": ["jardinage",   "pétanque"], "age": 79},  {"nom": "Dupont", "prenom": "Catherine", "interets": ["cuisine"], "age": 66},  {"nom": "Duport", "prenom": "Eric", "interets": ["cuisine", "pétanque"], "age": 57},  {"nom": "Duport", "prenom": "Arlette","interets": ["jardinage"], "age": 80},  {"nom": "Lejeune", "prenom": "Jean","interets": ["jardinage"], "age": 75},  {"nom": "Lejeune", "prenom": "Mariette","interets": ["jardinage", "bridge"], "age": 66})
`

on peut donc créer un index de la collection trié par ordre décroissant

```js
db.personnes.createIndex({"age": -1})
```

il existe un moyen de consulter la liste de index d'une collection :

```js
db.personnes.getIndexes()
```

et va retourner : 

```js
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { age: -1 }, name: 'age_-1' }
]
```

pour supprimet un index, il suffit d'effectuer la commande suivante :

```js
db.personnes.dropIndex("age_-1")
```

on peut aussi nommer un index (age_-1 c'est moche):

```js
db.personnes.createIndex({"age": -1}, {"name": "unJoliNom"})
```

exercices : [[index]] et [[index réponses]]

___

__Tableaux : 

db: `db.hobbies.insertMany([   {"_id": 1, "nom": "Yves"},   {"_id": 2, "nom": "Sandra", "passions": []},   {"_id": 3, "nom": "Line", "passions": ["Théâtre"]}  ])`


les opérateurs de tableaux : 


`push` permet d'ajouter une ou plusieurs valeurs au sein d'un tableau

```js
{ $push: {<champ>: <valeur>, ...} }
```

exemple : 
```js
db.hobbies.updateOne({"_id": 1}, {$push: {"passions": "Le roller!"}})
```


pour accéder aux données, on ajoute un . avec la position de la valeur attendue : 

```js
db.hobbies.find("passions.1": "Le roller!")
```


`pop` permet de retirer une ou plusieurs valeurs au sein d'un tableau

```js
{ $pop: {<champ>: <valeur>, ...} }
```

exemple :
```js
db.hobbies.updateOne({"_id": 1}, {$push: {"passions": 1}})
```
