Exercice 1 :
`db.salles.find({"smac": true})

Exercice 2 :
`db.salles.find({"capacite": { $gt: 1000}})

Exercice 3 :
`db.salles.find({"adresse.numero": null})

Exercice 4 :
db.salles.find({"avis.length": 1}, {"_id": true, "nom": true})

Exercice 5 :
`db.salles.find({"styles": "blues"}, {"styles": true})

Exercice 6 :
`db.salles.find({"styles.0": "blues"})

Exercice 7 :
`db.salles.find({"adresse.codePostal": {$regex: "84.*"}, "capacite": {$lt : 500}})

Exercice 8 :
`db.salles.find({"_id": })