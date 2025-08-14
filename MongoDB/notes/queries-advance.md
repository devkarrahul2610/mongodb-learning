use MongoDB_11_8_25;

db.createCollection('Products')

db.Products.insertMany(

    [

        { "_id": 1, "name": "Laptop", "category": "Electronics", "price": 800, "stock": 10, "ratings": [5, 4, 5] },

        { "_id": 2, "name": "Phone", "category": "Electronics", "price": 500, "stock": 30, "ratings": [4, 4, 3, 5] },

        { "_id": 3, "name": "Shoes", "category": "Fashion", "price": 100, "stock": 50, "ratings": [5, 5, 4] },

        { "_id": 4, "name": "Shirt", "category": "Fashion", "price": 40, "stock": 100, "ratings": [4, 3] }

    ]

)

// output of the first one,pass to the input of second one.
aggregate([operation1,operation2,.........])
$match: filter documents.

// find all products with category Electronics.

db.Products.find({"category": "Electronics"})

db.Products.aggregate([
    {
       $match:{
        "category": "Electronics"
       }
    }
])

//find all products with stock less than 50

db.Products.find({
    stock:{
        $lt:50
    }
})

db.Products.aggregate([
    {
        $match:{
            stock:{
                $lt:50
            }
        }
    }
])
// if you want to project then we have : $project operator.
//find all products with stock less than 50 and project only name and price.
db.Products.find({
    stock:{
        $lt:50
    }
},{
    name:1,price:1,_id:0
})

db.Products.aggregate([
    {
        $match:{
            stock:{
                $lt:50
            }
        }
    },
    {
        $project:
        {
           name:1,
           price:1,
           _id:0
        }
    }
])

//find all products with stock less than 50 and project only name and 
  price in decending order of price.

  filter - $match
  projection of field - $project
  sort in decending order of price - $sort(1:ascending and -1:decending)

db.Products.aggregate([
    {
       $match:
       {
          stock:{
            $lt:50
          }
       }
    },
    {
        $project:{
            name:1,price:1,_id:0
        }
    },
    {
        $sort:{
            price:1
        }
    }
])

db.Products.aggregate([
    {
       $match:
       {
          stock:{
            $lt:50
          }
       }
    },
    {
        $project:{
            name:1,category:1,_id:0
        }
    },
    {
        $sort:{
            price:1
        }
    }
])

Here output of first operation to the input of second and so on. If some fields are not the 
part of projection and you perfom something in next operation then didn't get the proper result.
so write projection at the end.

db.Products.aggregate([
    {
       $match:
       {
          stock:{
            $lt:50
          }
       }
    },
    {
        $sort:{
            price:1
        }
    },
    {
        $project:{
            name:1,category:1,_id:0
        }
    }
    
])

//find projects with lowest price and project only name,price and category

1.apply sorting in asc order because we want lowest price.
2. Limit the product to 1.


db.Products.aggregate([
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
            name:1,price:1,category:1,_id:0
        }
    }
])

// find product with second lowest price
db.Products.aggregate([
    {
        $sort:{
            price:1
        }
    },
    {
        $skip:1
    },
    {
        $limit:1
    },
     {
        $project:{
            name:1,price:1,category:1,_id:0
        }
    }
])


