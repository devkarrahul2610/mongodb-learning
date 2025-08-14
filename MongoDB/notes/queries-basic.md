create database if its not exist
use database

use MongoDB_11_8_25
MongoDB_11_8_25
db: ~current database name

create collection:
database_name.createCollection('collection_name')
db.createCollection('Employees')

Insert Data:
1- insertOne()
   insert single document into collection.

   database_name.collection_name.insertOne(
    {
        JSON object
    }
   )

   db.Employees.insertOne(
    {
        "name":"rahul sanjay devkar",
        "email":"rahulsd@gmail.com",
        "designation":"software engineer",
        "age":27,
        "salary":250000
    }
   )

{
  acknowledged: true,
  insertedId: ObjectId('6899bab0b4399530d589b03d')
}


***********************************************************************************
2. insertMany()
   insert many documents into collection.

   database_name.collection_name.insertMany([
       Array of object as a parameter
   ])

   db.Employees.insertMany([
    {
        "_id":1,
       "name":"rahul devkar",
        "email":"rahul@gmail.com",
        "designation":"software engineer",
        "age":28,
        "salary":290000
    },
    {
        "_id":2,
         "name":"vaibhav kate",
        "email":"vaibhav@gmail.com",
        "age":27,
        "salary":70000
    },
    {
         "_id":3,
       "name":"nikhil patil",
        "email":"nikhil@gmail.com",
        "designation":"software engineer",
        "age":28,
        "salary":270000,
        "address":"Pune"
    }
   ])

   { acknowledged: true, insertedIds: { '0': 1, '1': 2, '2': 3 } }

*************************************************************************************************
fetch documents from collection:
current_database_name.collection_name.find()
db.Employees.find()

// fetch employee whoes age is less than 30:-- 
   operator {$gt/$lt/$eq/$lte/$gte}
   find({condition})  

db.Employees.find({
    age:{$lt:30}
})

operator {$in and $nin}

db.Employees.find({
    salary:{
        $in:[70000,50000,270000,290000]
    }
})

db.Employees.find({
    salary:{
        $nin:[70000,50000,270000,290000]
    }
})

// add more than one condition.
// $and: both the conditions must evaluated to true {age gt 30 and salary gt 150000}

db.Employees.find({
    $and:[
        {
        age:{
            $gt:30
        }
        },
        {
            salary:{
                $gt:150000
            }
        }
    ]
})

// $or:either of the condition evaluated to true.

db.Employees.find(
    {
        $or:[
            {
                age:{
                    $gt:30
                }
            },
            {
                salary:{
                    $gt:150000
                }
            }
        ]
    }
)

// delete documents:
   deleteOne(): delete single document
   deleteMany():delete many document

   delete employees whoes salary is less than 80000.
   deleteOne deletes the only one record which is inserted first and satisfied the condition.
   
   db.Employees.deleteOne({
    salary:{
        $lt:80000
    }
   })

  // deleteMany(): deletes all the documents which satisfied the condition.

  db.Employees.deleteMany({
    salary:{
        $lt:80000
    }
  })

  /* small assignment: 
     find employees whoes age is less than and equal to 30.
     find employees whoes name is not in given list.["Rahul","Pratiksha"]
     Delete Employee whose name is equal to 'Rahul'
     Delete Employee whose salary greater than 150000 */

    solution: 
    1. db.Employees.find({
        age:{
            $lte:30
        }
    })

    2. db.Employees.find({
        name:{
            $nin:["rahul devkar","aish devkar"]
        }
    })

    3. db.Employees.deleteOne({
        name:{
            $eq:"rahul devkar"
        }
    })

    4. db.Employees.find({
        salary:{
            $gt:150000
        }
    })

// update

//Update :- '$set' to specify updated values
//update on the basis of name modify value of salary and age even add designation
1.updateOne():- It will update first Maching document
 
age:26,
salary:190000,
designation:'QA'
 
updateOne({condition},{setter value})

db.Employees.updateOne(
    {
        //name:"rahul devkar"
        name:{
            $eq:"rahul devkar"
        }
    },
    {
        $set:{
                age:27,
                salary:190000,
                designation:'Golang Developer'
        }
    }
)
 
 
 
 
2.UpdateMany():- It will update all matching documents

db.Employees.updateMany(
    {
        //name:"rahul devkar"
        name:{
            $eq:"rahul devkar"
        }
    },
    {
        $set:{
                age:27,
                salary:190000,
                designation:'Golang Developer'
        }
    }
)
 

/*
Update Employees whose email is  "sonalimi@cybahe.com"
Set address,change age,salary and designation
*/

db.Employees.updateOne(
    {
    email:{
        $eq:"vaibhav@gmail.com"
    }
    },
    {
        $set:{
            age:30,
            salary:75000,
            designation:"junior engineer"
        }
    }
)
 
 db.Employees.updateMany(
    {
        name:{
            $eq:"Abhijeet kadam"
        }
    },
    {
        $set:{
                age:45,
                salary:450000,
                designation:'technical architect'
        }
    },
    {
        upsert:true //Insert new document if matching document is not exist
    }
)
 
//Projection:- fetch only specific fields of document
//_id field projection implicitly seted to one 
//1 means project field
//0 means dont project field 
find({condition},{projection})
 
db.Employees.find({},{name:1,email:1,_id:0})
 
 
 


