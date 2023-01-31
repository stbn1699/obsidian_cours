questions : [[index]]

```js
db.salles.createIndex({
	"capacite": {$gt: 500}, 
	"adresse.codePostal": /^30/
}, 
{
	"name": "capGT500_endPostal30"
})


db.salles.createIndex({
	"adresse.codePostal": /^30/, 
	"capacite": {$lte: 400}
}, 
{
	"name" : "endPostal30_capLTE400"
})



db.personnes.dropIndex("capGT500_endPostal30", "endPostal30_capLTE400")
```