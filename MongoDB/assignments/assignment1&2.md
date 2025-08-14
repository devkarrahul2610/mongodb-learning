Problem Statement: Movie Database Management in MongoDB
You are building a MongoDB database for a streaming platform to store and manage movie details. 
The platform needs functionalities to insert, fetch, update, and delete movie records.
Requirements
1. Database & Collection Setup
Create a database named MovieDB (only if it does not already exist).
Switch to this database.
Create a collection named Movies.
2. Insert Records
a) Insert a single document using insertOne with the following details:
{"_id": 1,"title": "Inception","director": "Christopher Nolan","releaseYear": 2010,"genres": ["Sci-Fi", "Action", "Thriller"],"ratings": { "imdb": 8.8, "rottenTomatoes": 87 },"boxOffice": 829895144 } 
b) Insert multiple documents using insertMany with at least 4 more movies having:
Different sets of genres (array)
Different ratings (object with imdb and rottenTomatoes)
Some missing fields like boxOffice or director to allow later updates.
Example:
[{"_id": 2,"title": "The Dark Knight","director": "Christopher Nolan","releaseYear": 2008,"genres": ["Action", "Crime", "Drama"],"ratings": { "imdb": 9.0, "rottenTomatoes": 94 },"boxOffice": 1004558444},{"_id": 3,"title": "Interstellar","director": "Christopher Nolan","releaseYear": 2014,"genres": ["Sci-Fi", "Adventure", "Drama"],"ratings": { "imdb": 8.6, "rottenTomatoes": 72 }},{"_id": 4,"title": "Parasite","director": "Bong Joon-ho","releaseYear": 2019,"genres": ["Thriller", "Drama"],"ratings": { "imdb": 8.6, "rottenTomatoes": 99 }},{"_id": 5,"title": "Avengers: Endgame","director": "Anthony and Joe Russo","releaseYear": 2019,"genres": ["Action", "Adventure", "Sci-Fi"],"ratings": { "imdb": 8.4, "rottenTomatoes": 94 },"boxOffice": 2797800564} ] 
3. Fetch Records
Retrieve all movies.
Retrieve movies released after 2010 ($gt operator).
Retrieve movies where boxOffice is not in [500000000, 800000000].
Retrieve movies where:
releaseYear is greater than 2015 and
imdb rating is greater than 8.5.
Retrieve movies where:
releaseYear is less than 2015 or
genres contains "Thriller".
Retrieve only title, genres, and ratings fields (exclude _id) using projection.

4. Delete Records
Delete one movie where the title is "Parasite".
Delete all movies with a boxOffice greater than 2000000000.

5. Update Records
Update one movie: change the boxOffice of "Interstellar" to 700000000 and add a missing field "duration": 169 (in minutes).
Update many movies where the director is "Christopher Nolan":
Set "awards": "Multiple Academy Nominations".
If no such document exists, insert one with title "Unknown Nolan Film", releaseYear 2025, genres [], and ratings {} (use upsert: true).

6. Projection Queries
Show only title and imdb rating from ratings for all movies.
Show all fields except boxOffice.
 
Problem Statement: Bookstore Database in MongoDB
You are managing a digital bookstore’s database. You need to create and manipulate book records to help the store track inventory, authors, and customer reviews.
1. Database & Collection Setup
Create a database named BookStoreDB (only if it doesn’t already exist).
Switch to the database.
Create a collection named Books.
2. Insert Records
a) Insert a single book using insertOne:
{"_id": 101,"title": "The Alchemist","authors": ["Paulo Coelho"],"publishedYear": 1988,"genres": ["Fiction", "Adventure"],"reviews": { "goodreads": 4.0, "amazon": 4.7 },"price": 350 } 
b) Insert multiple books using insertMany (at least 4 more), ensuring:
Some have multiple authors.
Some have missing fields like price or reviews.
Different genres for diversity.
Example:
[{"_id": 102,"title": "Atomic Habits","authors": ["James Clear"],"publishedYear": 2018,"genres": ["Self-help", "Productivity"],"reviews": { "goodreads": 4.4, "amazon": 4.8 },"price": 499},{"_id": 103,"title": "Sapiens: A Brief History of Humankind","authors": ["Yuval Noah Harari"],"publishedYear": 2011,"genres": ["History", "Science"],"reviews": { "goodreads": 4.4, "amazon": 4.6 }},{"_id": 104,"title": "Harry Potter and the Sorcerer's Stone","authors": ["J.K. Rowling"],"publishedYear": 1997,"genres": ["Fantasy", "Adventure"],"reviews": { "goodreads": 4.5, "amazon": 4.9 },"price": 599},{"_id": 105,"title": "Ikigai","authors": ["Héctor García", "Francesc Miralles"],"publishedYear": 2016,"genres": ["Self-help", "Philosophy"],"reviews": { "goodreads": 3.9, "amazon": 4.5 },"price": 299} ] 

3. Fetch Records
Retrieve all books.
Retrieve books published after 2010.
Retrieve books where price is not in [299, 350].
Retrieve books where:
publishedYear is greater than 2000 and
goodreads rating is greater than 4.3.
Retrieve books where:
publishedYear is less than 2000 or
genres contains "Self-help".
Retrieve only title, authors, and reviews (exclude _id) using projection.
4. Delete Records
Delete one book where the title is "Ikigai".
Delete all books priced above 500.
5. Update Records
Update one book: set price of "Sapiens: A Brief History of Humankind" to 550 and add "pages": 498.
Update many books where the genre includes "Self-help":
Set "bestseller": true.
If no such document exists, insert one with title "Unknown Self-help Book", publishedYear 2025, empty authors, empty genres, and reviews {} (use upsert: true).
6. Projection Queries
Show only title and goodreads rating from reviews for all books.
Show all fields except price.
 