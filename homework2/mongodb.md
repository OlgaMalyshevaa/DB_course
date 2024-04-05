# MongoDB

## **Используемый датасет:** [Mall_Customers](https://www.kaggle.com/datasets/shwetabh123/mall-customers?resource=download)
Данные посетителей магазина: id, пол, возраст, доход, рейтинг трат\
Работа выполнена в MongoDB Compass
## **Запросы на выборку и обновление данных**
### **1. Create**
**1.1 Добавление одного элемента (метод insertOne()):**
```js
db.customers.insertOne({ "CustomerID": 201,
"Genre": "Female",
"Age": 37,
"Annual Income (k$)":  137,
"Spending Score (1-100)": 69})
```

```js
{
    acknowledged: true,
    insertedId: ObjectId('660fdd8272aec7d7ee53a43b')
}
```
**1.2 Множественное добавление (метод insertMany()):**
```js
db.customers.insertMany([ 
{ "CustomerID": 202, "Genre": "Female", "Age": 32, "Annual Income (k$)":  137, "Spending Score (1-100)": 33},
{ "CustomerID": 203, "Genre": "Male", "Age": 28, "Annual Income (k$)":  137, "Spending Score (1-100)": 29} 
])
```

```js
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('660fe24872aec7d7ee53a43e'),
    '1': ObjectId('660fe24872aec7d7ee53a43f')
  }
}
```
### **2. Read**
**2.1 Метод findOne():**
```js
db.customers.findOne({ _id: ObjectId('660fda26e6f10aab4d9d0351')}, {CustomerID: 1})
```

```js
{
  _id: ObjectId('660fda26e6f10aab4d9d0351'),
  CustomerID: 181
}
```
**2.2 Метод find():**
```js
db.customers.find({ $and: [{Age: {$lte: 24}}, {Genre: "Female"}] }, {CustomerID: 1, Age: 1}).sort({Age: 1}).limit(4)
```

```js
{
  _id: ObjectId('660fda26e6f10aab4d9d030f'),
  CustomerID: 115,
  Age: 18
}
{
  _id: ObjectId('660fda26e6f10aab4d9d0310'),
  CustomerID: 116,
  Age: 19
}
{
  _id: ObjectId('660fda26e6f10aab4d9d030c'),
  CustomerID: 112,
  Age: 19
}
{
  _id: ObjectId('660fda26e6f10aab4d9d02c4'),
  CustomerID: 40,
  Age: 20
}
```
### **3. Update**
**3.1 Метод updateOne():**

До вызова метода: 
```js
db.customers.findOne({ _id: ObjectId('660fda26e6f10aab4d9d0351') }, {'Spending Score (1-100)': 1})
```
```js
{
  _id: ObjectId('660fda26e6f10aab4d9d0351'),
  'Spending Score (1-100)': 38
}
```
Вызов метода:

```js
db.customers.update({CustomerID: 181}, {$inc: {"Spending Score (1-100)": 3}})
```

```js
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
После вызова метода: 
```js
db.customers.findOne({ _id: ObjectId('660fda26e6f10aab4d9d0351') }, {'Spending Score (1-100)': 1})
```

```js
{
  _id: ObjectId('660fda26e6f10aab4d9d0351'),
  'Spending Score (1-100)': 48
}
```

**3.2 Метод updateMany():**

До вызова метода:
```js
db.customers.find({CustomerID: {$lte: 4}}, {'Spending Score (1-100)': 1})
```
```js
{
  _id: ObjectId('660fda26e6f10aab4d9d029d'),
  'Spending Score (1-100)': 39
}
{
  _id: ObjectId('660fda26e6f10aab4d9d029e'),
  'Spending Score (1-100)': 81
}
{
  _id: ObjectId('660fda26e6f10aab4d9d029f'),
  'Spending Score (1-100)': 6
}
{
  _id: ObjectId('660fda26e6f10aab4d9d029f'),
  'Spending Score (1-100)': 6
}
```
Вызов метода:
```js
db.customers.updateMany({CustomerID: {$lte: 4}}, {$set: {'Spending Score (1-100)': 50}})
```
```js
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}
```
После вызова метода:
```js
db.customers.find({CustomerID: {$lte: 4}}, {'Spending Score (1-100)': 1})
```
```js
{
  _id: ObjectId('660fda26e6f10aab4d9d029d'),
  'Spending Score (1-100)': 50
}
{
  _id: ObjectId('660fda26e6f10aab4d9d029e'),
  'Spending Score (1-100)': 50
}
{
  _id: ObjectId('660fda26e6f10aab4d9d029f'),
  'Spending Score (1-100)': 50
}
{
  _id: ObjectId('660fda26e6f10aab4d9d02a0'),
  'Spending Score (1-100)': 50
}
```

**3.3 Метод updateMany():**
```

```

### **4. Delete**






