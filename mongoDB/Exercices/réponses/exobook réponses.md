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

b.
```js
db.employees.find()
```

c.
```js
db.employees.find({"age": {$gt: 33}})
```

d.
```js
db.employees.find()
```