create database if it is not exist
->use database
use MongoDB_8_11_2025
 
db :-current database name
 
create Collection
database_name.createCollection('collection_name')
db.createCollection('Employees')
 
Insert Data 
1-insertOne()
    Insert single document into collection
 
database_name.collection_name.insertOne(
    {
        JSON Object
    }
)
 
db.Employees.insertOne(
    {
        "_id":1,//primary key 
        "name":"Sonali Ashish Maind",
        "email":"sonalimi@cybage.com",
        "designation":"Sr. Tech Lead",
        "age":35,
        "salary":257000
    }
)
**************************************
{
  acknowledged: true,
  insertedId: ObjectId("6899ba9addc4b43ea418aeaa")
}
********************************
{ acknowledged: true, insertedId: 1 }
 
 
2-insertMany()
    Insert many documents into collection
 
database_name.collection_name.insertMany(
   [
        Array of Objects 
   ]
)
 
db.Employees.insertMany(
   [
        {
            "_id":2,//primary key 
            "name":"Ashish Maind",
            "email":"ashishma@cybage.com",
            "designation":"Sr. Manager",
            "age":35,
            "salary":430000
        },
        {
            "_id":3,//primary key 
            "name":"Omkar Mindhe",
            "email":"omkarmi@cybage.com",
            "age":25,
        },
        {
            "_id":4,//primary key 
            "name":"Prasad Korde",
            'address':'Pune'
        }
   ]
)
*********************
{ acknowledged: true, insertedIds: { '0': 2, '1': 3, '2': 4 } }
 
Fetch Documents from Collection
current_database_name.collection_name.find()
db.Employees.find():--Return All documents from Collection
 
//Fetch employee whose age is less than 30--Operator {$gt/$lt/$eq/$lte/$gte}
find({condition})
 
db.Employees.find(
    {
        age:{$gt:30}
    }
)
 
$in and $nin
 
db.Employees.find(
    {
        salary:{
 
            $nin:[60000,180000,40000,28000]
        }
    }
)
 
//Add more than one condition
$and :- Both conditions must evaluated to true -age gt 30 and salary gt 150000
$or :- either of condition must evaluated to true
 
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
 
//delete documents
1.deleteOne({condition}):--delete single document whcich appear first in order
 
//delete employees salary is less that 80000
 
db.Employees.deleteOne(
    {
        salary:{
            $lt:80000
        }
    }
)
2.deleteMany():--delete many document which match given condition
 
db.Employees.deleteMany(
    {
        salary:{
            $lt:80000
        }
    }
)
 
 
/*
Find Employees whose age is less than and equal to 30
Find Employee whose name is not in given list ['Sonali','Prasad']
Delete Employee whose name is equal to 'Sonali'
Delete Employee whose salary greater than 150000
*/
 
 
//Update :- '$set' to specify updated values
//update on the basis of name modify value of salary and age even add designation
1.updateOne():- It will update first Maching document
 
age:26,
salary:190000,
designation:'QA'
 
updateOne({condition},{setter value})
 
db.Employees.updateOne(
    {
        //name:"Omkar Mindhe"
        name:{
            $eq:"Omkar Mindhe"
        }
    },
    {
        $set:{
                age:26,
                salary:190000,
                designation:'QA'
        }
    }
)
 
 
 
 
2.UpdateMany():- It will update all matching documents
 
 
db.Employees.updateMany(
    {
        name:{
            $eq:"Komal Jadhav"
        }
    },
    {
        $set:{
                age:26,
                salary:150000,
                designation:'DBA'
        }
    },
    {
        upsert:true //Insert new document if matching document is not exist
    }
)
/*
Update Employees whose email is  "sonalimi@cybahe.com"
Set address,change age,salary and designation
*/
 
 
//Projection:- fetch only specific fields of document
//_id field projection implicitly seted to one 
//1 means project field
//0 means dont project field 
find({condition},{projection})
 
db.Employees.find({},{name:1,email:1,_id:0})
 
 