questions : [[exobook]]

__a.__ 
```js
db.employees.insertMany([
{
	"name": "John Doe",
	"age": 35,
	"job": "Manager",
	"salary": 80000
},
{
	"name": "Jane Doe",
	"age": 32,
	"job": "Developper",
	"salary": 75000
},
{
	"name": "Jim Smith",
	"age": 40,
	"job": "Manager",
	"salary": 85000
}])
```

__b.__
```js
db.employees.find()
```

__c.__
```js
db.employees.find({"age": {$gt: 33}})
```

__d.__
```js
db.employees.find().sort({"salary": -1})
```

__e.__
```js
db.employees.find({}, {"_id": false, "name": true, "job": true})
```

__f.__
```js
db.employees.aggregate([
	{
		$group: {_id: "$job", count: {$sum: 1}}
	}
])
```

__g.__
```js
db.employees.update({"job": "Developper"}, {$set:{"salary": 80000}})
```