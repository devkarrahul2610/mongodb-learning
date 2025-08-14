db.createCollection('Products')
 
db.Products.insertMany(
    [
        { "_id": 1, "name": "Laptop", "category": "Electronics", "price": 800, "stock": 10, "ratings": [5, 4, 5] },
        { "_id": 2, "name": "Phone", "category": "Electronics", "price": 500, "stock": 30, "ratings": [4, 4, 3, 5] },
        { "_id": 3, "name": "Shoes", "category": "Fashion", "price": 100, "stock": 50, "ratings": [5, 5, 4] },
        { "_id": 4, "name": "Shirt", "category": "Fashion", "price": 40, "stock": 100, "ratings": [4, 3] }
    ]
)
 
aggregate([operation1,operation2,.....])
 
$match :--Filter documents
 
db.Products.find({"category": "Electronics"})
 
//Find all products with category Electronics
db.Products.aggregate(
    [
        {
            $match:{
                "category": "Electronics"
            }
        }
    ]
)
 
//Find all products with stock less than 50--Filter($match)
db.Products.aggregate(
    [
        {
            $match:{
                "stock":{$lt:50}
            }
        }
    ]
)
 
 
//Only project particular fields from document--$project
//Find all products with stock less than 50 and project only name and price--Filter($match)
db.Products.aggregate(
    [
        {
            $match:{
                        stock:{$lt:50}
                    }
        },
        {
            $project:{
                        name:1,
                        price:1,
                        _id:0
                    }
        }
    ]
)
//Find all products with stock less than 50 and project only name and price in desc order of price
filter data ------------------------$match
decide Projection of field----------$project
sort in desc order of price---------$sort(1:asc/-1:desc)
 
db.Products.aggregate(
    [
        {
            $match:{
                'stock':{$lt:50}
            }
        },
        {
            $sort:{
                price:1
            }
        },
        {
            $project:{
                name:1,
                category:1,
                _id:0
            }
        }
    ]
)
 
 
/*
Find Product with lowest price and only project name,price and category
 
1-apply sorting in asc order as we want lowest price products
2-limit result to 1
3-project name,price and category:--- $limit
 
*/
 
db.Products.aggregate(
    [
 
        {
            $sort:{
                price:1
            }
        },
        {
            $limit:1
        },
        {
            $project:{
                _id:0,
                name:1,
                price:1,
                category:1
            }
        }
    ]
)
 
 
/*
Find product with 2 lowest price
n=2
skip (n-1)--$skip
*/
 
db.Products.aggregate(
    [
 
        {
            $sort:{
                price:1
            }
        },
        {
            $skip:2
        },
        {
            $limit:1
        },
        {
            $project:{
                _id:0,
                name:1,
                price:1,
                category:1
            }
        }
    ]
)