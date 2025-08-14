Create a database named MovieDB (only if it does not already exist).
Switch to this database.
solution: use MovieDB

Create a collection named Movies.
solution: db.createCollection('Movies')

2. Insert Records
a) Insert a single document using insertOne with the following details:
{"_id": 1,"title": "Inception","director": "Christopher Nolan","releaseYear": 2010,
"genres": ["Sci-Fi", "Action", "Thriller"],
"ratings": { "imdb": 8.8, "rottenTomatoes": 87 },"boxOffice": 829895144 } 

solution: db.Movies.insertOne(
    {"_id": 1,"title": "Inception","director": "Christopher Nolan","releaseYear": 2010,
"genres": ["Sci-Fi", "Action", "Thriller"],
"ratings": { "imdb": 8.8, "rottenTomatoes": 87 },"boxOffice": 829895144 }
)

b) Insert multiple documents using insertMany with at least 4 more movies having:
Different sets of genres (array)
Different ratings (object with imdb and rottenTomatoes)
Some missing fields like boxOffice or director to allow later updates.
Example:
[{"_id": 2,"title": "The Dark Knight","director": "Christopher Nolan","releaseYear": 2008,
"genres": ["Action", "Crime", "Drama"],"ratings": { "imdb": 9.0, "rottenTomatoes": 94 },
"boxOffice": 1004558444},{"_id": 3,"title": "Interstellar","director": "Christopher Nolan",
"releaseYear": 2014,"genres": ["Sci-Fi", "Adventure", "Drama"],
"ratings": { "imdb": 8.6, "rottenTomatoes": 72 }},
{"_id": 4,"title": "Parasite","director": "Bong Joon-ho","releaseYear": 2019,"genres": 
["Thriller", "Drama"],"ratings": { "imdb": 8.6, "rottenTomatoes": 99 }},
{"_id": 5,"title": "Avengers: Endgame","director": "Anthony and Joe Russo",
"releaseYear": 2019,"genres": ["Action", "Adventure", "Sci-Fi"],"ratings": 
{ "imdb": 8.4, "rottenTomatoes": 94 },"boxOffice": 2797800564} ] 

solution: 
 db.Movies.insertMany(
    [{"_id": 2,"title": "The Dark Knight","director": "Christopher Nolan","releaseYear": 2008,
"genres": ["Action", "Crime", "Drama"],"ratings": { "imdb": 9.0, "rottenTomatoes": 94 },
"boxOffice": 1004558444},{"_id": 3,"title": "Interstellar","director": "Christopher Nolan",
"releaseYear": 2014,"genres": ["Sci-Fi", "Adventure", "Drama"],
"ratings": { "imdb": 8.6, "rottenTomatoes": 72 }},
{"_id": 4,"title": "Parasite","director": "Bong Joon-ho","releaseYear": 2019,"genres": 
["Thriller", "Drama"],"ratings": { "imdb": 8.6, "rottenTomatoes": 99 }},
{"_id": 5,"title": "Avengers: Endgame","director": "Anthony and Joe Russo",
"releaseYear": 2019,"genres": ["Action", "Adventure", "Sci-Fi"],"ratings": 
{ "imdb": 8.4, "rottenTomatoes": 94 },"boxOffice": 2797800564} ] 
 )

3. Fetch Records
a. Retrieve all movies.
b. Retrieve movies released after 2010 ($gt operator).
c. Retrieve movies where boxOffice is not in [500000000, 800000000].
d. Retrieve movies where:
   releaseYear is greater than 2015 and
   imdb rating is greater than 8.5.
e. Retrieve movies where:
   releaseYear is less than 2015 or
   genres contains "Thriller".
f. Retrieve only title, genres, and ratings fields (exclude _id) using projection.

solution:
a. db.Movies.find()
b. db.Movies.find({
    releaseYear:{
        $gt:2010
    }
})
c. db.Movies.find({
    boxOffice:{
        $nin:[500000000, 800000000]
    }
})
d. db.Movies.find({
    $and:[
        {
            releaseYear:{
                $gt:2015
            }
        },
        {
           "ratings.imdb":{
             $gt:8.5
           }
        }
    ]
})
e. db.Movies.find({
    $or:[
        {
            releaseYear:{
                $lt:2015
            }
        },
        {
            genres:{
                $eq:"Thriller"
            }
        }
    ]
})

f. db.Movies.find({},{
    title:1,genres:1,ratings:1,_id:0
})

4. Delete Records
a. Delete one movie where the title is "Parasite".
b .Delete all movies with a boxOffice greater than 2000000000.

solution:
a. db.Movies.deleteOne({
    title:{
        $eq:"Parasite"
    }
})
b. db.Movies.deleteMany({
    boxOffice:{
        $gt:2000000000
    }
})


5. Update Records
a. Update one movie: change the boxOffice of "Interstellar" to 700000000 and add a 
   missing field "duration": 169 (in minutes).

b. Update many movies where the director is "Christopher Nolan":
   Set "awards": "Multiple Academy Nominations".

   If no such document exists, insert one with title "Unknown Nolan Film", 
   releaseYear 2025, genres [], and ratings {} (use upsert: true).

solution:
a. db.Movies.updateOne(
    {
    title:{
        $eq:"Interstellar"
    }
    },
    {
        $set:
        {
            boxOffice:700000000,
            duration:169
        }
         
    }
   
)

b. db.Movies.updateMany(
    {
       director:{
        $eq:"Christopher Nolan"
       }
    },
    {
       $set:
       {
          awards:"Multiple Academy Nominations"
       }

       $setOnInsert: 
         {
            title: "Unknown Nolan Film",
            releaseYear: 2025,
            genres: [],
            ratings: {}
          }
    },
       {upsert:true}
)


6. Projection Queries
a. Show only title and imdb rating from ratings for all movies.
b. Show all fields except boxOffice.

solution:
a. db.Movies.find({},{title:1,"ratings.imdb":1,_id:0})
b. db.Movies.find({},{boxOffice:0})