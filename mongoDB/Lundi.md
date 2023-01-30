mongoDB -> système de base de données orienté objet

stocké dans du json -> pas de structure

désavantage : on se retrouve vite aves des infos dupliquées

avantages : pas de shéma; structure simple en objet; pas de jointure complexe; des requêtes imbriquées et dynamiques, très facile de "scale"; stockage sur disque; pas besoin d'ORM

___

voir : notation JSON

mongoDB apporte ses propres types a ceux rencontrés au sein du format JSON standard : 
	- __le type date :__ entier signé de 8 octect représente le nombre de secondes depuis epoch (01/01/1970 00:00:00), le type date ne stocke pas la timezone
	- __le type ObjectID :__ stocke sur 12 octets, utile en interne afin de garantir l'unicité des identifiants auto-générés par la BDD
	- __le type NupberLong et NumberInt :__ par défaut, mongoDB considère que toute valeur numérique est un nombre a virgule code sur 8 octets.
	- __le type NumberDecimal :__ sur 16 octets, le plus précis
	- __le type BinData :__ pour représenter eds caractères qu'on ne peut pas encoder en Utf-8

___

Création de base de données

On peut utiliser `use` pour se connecter a une BDD qui n'existe pas. l'insertion du premier document va entrainer la création de la BDD

```javascript
use tmp
db.uneCollection.insert({"key": "value"})
```

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

