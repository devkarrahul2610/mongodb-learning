create collection:
database_name.createCollection('collection_name')
db.createCollection('Book')

insertMany()
   insert many documents into collection.

   database_name.collection_name.insertMany([
       Array of object as a parameter
   ])

   db.Book.insertMany([
    {
    "_id": 1,
    "bookId": 11,
    "name": "the art of focus",
    "author": "susan lee",
    "price": 300
},
{
    "_id": 2,
    "bookId": 12,
    "name": "mindset mastery",
    "author": "john carter",
    "price": 275
},
{
    "_id": 3,
    "bookId": 13,
    "name": "path to freedom",
    "author": "maria gomez",
    "price": 320
},
{
    "_id": 4,
    "bookId": 14,
    "name": "invest smart",
    "author": "alan smith",
    "price": 450
},
{
    "_id": 5,
    "bookId": 15,
    "name": "power of discipline",
    "author": "kevin brown",
    "price": 280
}
   ])

fetch documents from collection:
current_database_name.collection_name.find()
db.Book.find()