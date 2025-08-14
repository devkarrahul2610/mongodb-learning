Movie Database Analysis using MongoDB Aggregation
Problem Statement:
You are working as a data analyst for an online movie streaming platform. 
Your database contains a collection named movies with the following sample 
structure:
{"_id": ObjectId("..."),"title": "Inception","year": 2010,"genre": 
["Action", "Sci-Fi", "Thriller"],"rating": 8.8,"boxOffice": 
{"budget": 160000000,"collection": 829895144},
"reviews": [{ "user": "John", "score": 9 },{ "user": "Emma", "score": 8 }] }

Your task is to write MongoDB aggregate queries to answer the 
following business requirements:
Tasks:
Find Top 5 Highest Rated Movies in a Given Genre
Filter ($match) movies where genre contains "Action".
Sort ($sort) them in descending order of rating.
Limit ($limit) to top 5 results.
Show only title, year, and rating fields.
Find Top 3 Most Profitable Movies Released After 2015
Use $match to filter movies where year > 2015.
Calculate profit as boxOffice.collection - boxOffice.budget using $addFields.
Sort by profit in descending order.
Limit results to top 3 movies.
Project ($project) only title, year, and calculated profit.

Get Top 5 Movies by Average Review Score

Unwind ($unwind) the reviews array.
Group ($group) by movie title to calculate average review score.
Sort results by average score in descending order.
Limit to top 5 movies.
Show title and average review score.

Get Top 5 Sci-Fi Movies by Box Office Collection

Match movies with "Sci-Fi" in the genre array.
Sort by boxOffice.collection in descending order.
Limit to top 5 results.
Project only title, year, and boxOffice.collection.