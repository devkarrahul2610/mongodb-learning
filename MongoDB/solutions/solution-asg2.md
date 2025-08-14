Problem Statement: Bookstore Database in MongoDB
You are managing a digital bookstore’s database. 
You need to create and manipulate book records to help the store track inventory, 
authors, and customer reviews.

1. Database & Collection Setup
Create a database named BookStoreDB (only if it doesn’t already exist).
Switch to the database.

solution: use BookStoreDB

Create a collection named Books.

solution: db.createCollection("Books")

2. Insert Records
a) Insert a single book using insertOne:
{"_id": 101,"title": "The Alchemist","authors": ["Paulo Coelho"],"publishedYear": 1988,
"genres": ["Fiction", "Adventure"],"reviews": { "goodreads": 4.0, "amazon": 4.7 },
"price": 350 } 

solution: db.Books.insertOne(
    {"_id": 101,"title": "The Alchemist","authors": ["Paulo Coelho"],"publishedYear": 1988,
"genres": ["Fiction", "Adventure"],"reviews": { "goodreads": 4.0, "amazon": 4.7 },
"price": 350 } 
)

b) Insert multiple books using insertMany (at least 4 more), ensuring:
Some have multiple authors.
Some have missing fields like price or reviews.
Different genres for diversity.
Example:
[{"_id": 102,"title": "Atomic Habits","authors": ["James Clear"],"publishedYear": 2018,
"genres": ["Self-help", "Productivity"],"reviews": { "goodreads": 4.4, "amazon": 4.8 },
"price": 499},{"_id": 103,"title": "Sapiens: A Brief History of Humankind",
"authors": ["Yuval Noah Harari"],"publishedYear": 2011,"genres": ["History", "Science"],
"reviews": { "goodreads": 4.4, "amazon": 4.6 }},
{"_id": 104,"title": "Harry Potter and the Sorcerer's Stone",
"authors": ["J.K. Rowling"],"publishedYear": 1997,"genres": ["Fantasy", "Adventure"],
"reviews": { "goodreads": 4.5, "amazon": 4.9 },"price": 599},
{"_id": 105,"title": "Ikigai","authors": ["Héctor García", "Francesc Miralles"],
"publishedYear": 2016,"genres": ["Self-help", "Philosophy"],
"reviews": { "goodreads": 3.9, "amazon": 4.5 },"price": 299} ] 

solution: db.Books.insertMany(
    [{"_id": 102,"title": "Atomic Habits","authors": ["James Clear"],"publishedYear": 2018,
"genres": ["Self-help", "Productivity"],"reviews": { "goodreads": 4.4, "amazon": 4.8 },
"price": 499},{"_id": 103,"title": "Sapiens: A Brief History of Humankind",
"authors": ["Yuval Noah Harari"],"publishedYear": 2011,"genres": ["History", "Science"],
"reviews": { "goodreads": 4.4, "amazon": 4.6 }},
{"_id": 104,"title": "Harry Potter and the Sorcerer's Stone",
"authors": ["J.K. Rowling"],"publishedYear": 1997,"genres": ["Fantasy", "Adventure"],
"reviews": { "goodreads": 4.5, "amazon": 4.9 },"price": 599},
{"_id": 105,"title": "Ikigai","authors": ["Héctor García", "Francesc Miralles"],
"publishedYear": 2016,"genres": ["Self-help", "Philosophy"],
"reviews": { "goodreads": 3.9, "amazon": 4.5 },"price": 299} ]
)

3. Fetch Records
a. Retrieve all books.
b. Retrieve books published after 2010.
c. Retrieve books where price is not in [299, 350].
d. Retrieve books where:
   publishedYear is greater than 2000 and
   goodreads rating is greater than 4.3.
e. Retrieve books where:
   publishedYear is less than 2000 or
   genres contains "Self-help".
f. Retrieve only title, authors, and reviews (exclude _id) using projection.

solution:
a. db.Books.find()
b. db.Books.find({
    publishedYear:{
        $gt:2010
    }
})
c. db.Books.find({
    price:{
        $nin:[299,350]
    }
})
d. db.Books.find(
    {
        $and:
        [
        {
          publishedYear:{
            $gt:2000
          }
        },
        {
            "reviews.goodreads":{
                $gt:4.3
            }
        }
        ]
    }
)
e. db.Books.find({
    $or:[
        {
            publishedYear:{
                $lt:2000
            }
        },
        {
            genres:{
                $eq:"self-help"
            }
        }
    ]
})
f. 

