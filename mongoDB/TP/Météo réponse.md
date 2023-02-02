### Jeu de données: 

[[weather_data.json]]
___
### Préparation des données: 

__a.__ 
```sh
mongoimport --uri 'mongodb+srv://admin:admin@cluster0.0vvbay1.mongodb.net/?retryWrites=true&w=majority' -d tps -c weather --file weather_data.json
```
___
### Indexation avec MongoDB: 

__a.__ 
`db.weather.createIndex({"date": 1}, {"name": "date_croissant"})`

__b.__ 
`db.runCommand ({listIndexes: "january_2023"})`
___
### Requêtes MongoDB: 

__a.__  
```js
db.weather.aggregate([{
	$match: {
		"date": {$gte: ISODate('2022-06-01')}
	}
}, {
	$match: {
		"date": {$lte: ISODate('2022-08-31')}
	}
}])
```

__b.__ `db.weather.find().sort({"pression": -1})`
___
### Framework d'agrégation: 

__a.__ 
```js
db.weather.aggregate([{
	$group: {
		_id: "$city",
		count: {$avg: "$temperature"}
	}
}])
```

__b.__ 
```js
db.weather.aggregate([{
	$group: {_id: "$temperature"}
}, {
	$sort: {"temperature": -1, _id : 1}
}, {
	$limit: 1
}])
```
___
### Export de la base de données: 

__a.__ 