Employee Performance & Salary Insights using MongoDB Aggregation
Problem Statement:
You are working as a database analyst for a corporate HR system. The database contains a collection named employees with documents in the following structure:
{"_id": ObjectId("..."),"name": "John Doe","department": "IT","designation": "Senior Developer","joiningYear": 2018,"salary": 85000,"projects": [{ "name": "Inventory System", "rating": 9 },{ "name": "CRM Upgrade", "rating": 8 }],"location": "New York" } 
Tasks:
Top 5 Highest Paid Employees in IT Department
Match ($match) employees where department is "IT".
Sort ($sort) by salary in descending order.
Limit ($limit) to 5 employees.
Project ($project) only name, designation, and salary.
Top 3 Employees with Highest Average Project Ratings
Unwind ($unwind) the projects array.
Group ($group) by employee name to calculate average projects.rating.
Sort by average rating in descending order.
Limit to top 3 employees.
Show name and calculated averageRating.
Top 5 Employees Joined After 2020 with Highest Salaries
Match employees with joiningYear > 2020.
Sort salaries in descending order.
Limit to top 5 employees.
Show only name, joiningYear, and salary.
Top 5 Locations by Average Salary
Group employees by location to calculate average salary.
Sort by average salary descending.
Limit to top 5 locations.
Show location and averageSalary.