db.createCollection("films")

db.films.insertMany([
  {
    title: "Inception",
    year: 2010,
    genre: ["Action", "Sci-Fi", "Thriller"],
    rating: 8.8,
    boxOffice: { budget: 160000000, collection: 829895144 },
    reviews: [
      { user: "John", score: 9 },
      { user: "Emma", score: 8 }
    ]
  },
  {
    title: "Interstellar",
    year: 2014,
    genre: ["Adventure", "Drama", "Sci-Fi"],
    rating: 8.6,
    boxOffice: { budget: 165000000, collection: 701729206 },
    reviews: [
      { user: "Alice", score: 9 },
      { user: "Bob", score: 8 }
    ]
  },
  {
    title: "The Dark Knight",
    year: 2008,
    genre: ["Action", "Crime", "Drama"],
    rating: 9.0,
    boxOffice: { budget: 185000000, collection: 1004558444 },
    reviews: [
      { user: "Charlie", score: 10 },
      { user: "Dave", score: 9 }
    ]
  },
  {
    title: "Avengers: Endgame",
    year: 2019,
    genre: ["Action", "Adventure", "Sci-Fi"],
    rating: 8.4,
    boxOffice: { budget: 356000000, collection: 2797800564 },
    reviews: [
      { user: "Sophia", score: 9 },
      { user: "Liam", score: 10 }
    ]
  },
  {
    title: "Parasite",
    year: 2019,
    genre: ["Drama", "Thriller"],
    rating: 8.6,
    boxOffice: { budget: 11400000, collection: 263100000 },
    reviews: [
      { user: "Olivia", score: 10 },
      { user: "Ethan", score: 9 }
    ]
  }
])

1. Find Top 5 Highest Rated Movies in a Given Genre
solution:
db.films.aggregate([
    {
        $sort:
        {
            rating:-1
        }
    },
    {
        $limit:5
    }
])

2. Filter ($match) movies where genre contains "Action"
solution: 
db.films.aggregate([
    {
        $match:
        {
          genre:'Action'
        }
    }
])

3. Sort ($sort) them in descending order of rating.
solution:
db.films.aggregate([
    {
        $sort:
        {
          rating:-1
        }
    }
])

4.Limit ($limit) to top 5 results.
solution:
db.films.aggregate(
    [
        {
            $limit:5
        }
    ]
)

5. Show only title, year, and rating fields.
solution:
db.films.aggregate([{
    $project:{
        title:1,year:1,rating:1,_id:0
    }
}])

6.Find Top 3 Most Profitable Movies Released After 2015.
solution:
db.films.aggregate([
    {
        $match:
        {
          year:
          {
            $gt:2015
          }
        }
    },
    {
        $addFields: 
        {
                profit: { $subtract: ["$boxOffice.collection", "$boxOffice.budget"] }
        }
    },
    {
        $limit:3
    },
    {
        $sort:{
            profit:-1
        }
    }
])

7. Use $match to filter movies where year > 2015.
solution: 
db.films.aggregate([
    {
        $match:
        {
           year:{
            $gt:2015
           }
        }
    }
])

8. Calculate profit as boxOffice.collection - boxOffice.budget using $addFields.
solution:
db.films.aggregate([
    {
        $addFields:{
            profit : { $subtract: ["$boxOffice.collection", "$boxOffice.budget"] }
        }
    }
])

9. Sort by profit in descending order.
solution:
db.films.aggregate([
    {
        $addFields:{
            profit : { $subtract: ["$boxOffice.collection", "$boxOffice.budget"] }
        }
    },
    {
        $sort:{
            profit:-1
        }
    }
])

10. Limit results to top 3 movies.
solution:
