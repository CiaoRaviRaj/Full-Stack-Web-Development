* # MongoDB
    * Introduction
        * 
    * SetUP
        * install MongoDB community Edition on system
            * it is 
        * install mongosh
            * it is used run mongoDB queries
        * install mongoDB server
    * to Show databases
        * Show databases
        * Show dbs
    * to create database
        * use database_name 
        * // if it is exist then i use otherwise it create

    * to show collection
        * show collections
    * to drop database
        * use database
        * db.dropDatabase()
    * cls - clear screen on terminal
    * BEST feature 
        * you never create any things
        * you just access it 
            * if it has , it fetch the data
            * otherwise it create data
        * 
    * to exit from terminal
        * run exit

    * create database
        * use appdb
        * it is not create utill it has data.
    * to create collections
        * // insertOne : - create one record
        * db.users.insertOne({name: "john"})
    * to fetch collection data
        * db.users.find()
        * it return all records of users
    * Flow of MongoDB
        * it is not need any schema
        * it follow documents
        * database -> collection -> documents(objects)
        * so you can save anything you want,it just create a object as a record, it is similar like  you make object in javascript
        * nested object can easily possible in mongoDB
        * EG: 
            * db.users.insertOne({name: "sally", age: 19 , address: {street: "987 north st"}, hobbies: ["Running"]})
            * it has nested object/ array anything you want.
            * it is impossible to do in SQL
        
    * Insert Many records
        * db.users.insertMany([{name: "record1"},{name: "record2"},{name: "record3"}]);
    * Limit and sort
        * db.users.find().sort({name: 1/-1}).limit(2)
        * sort({name: 1}) // ACE , -1 => DESC
        * we can also sort using multy fields
            * sort({name: 1, age: -1})
                * it sort first with name then , if record have same name , then it sort them with age
    * skip
        * skip some record from first
        * db.users.find().skip(2).limit(2)
        * it skip first 2 record , then it show next 2 records
    * find with condition
        * db.users.find({name: "record_name"})
            * it fetch record with name = "record_name"
            * it is type sensitive
                * db.users.find({age: 26})
                * it show records
                * db.users.find({age: "26"})
                * it do not show any records because it is a number on collection
    * find with condition with select 
        * db.users.find({name: "Kyle"}, {name: 1, age: 1, _id: 0})
        * it show name , age and it do not show _id field in fetched data with condition
        * or if you want to only not show age then you can use except field
            * db.users.find({name: "Kaly"}, {age: 0})
            * it show all record except age.
    * nested(complex) condition in find
        * db.users.find({name: {$eq: "Sally"}})
            * it show record where name = "Sally"
        * db.users.find({name: {$ne: "Sally"}})
            * it show record where name != "Sally"
        * $eq => equal
        * $ne => Not equal
        * $gt => Greater Then
        * $gte => Greater Then And Equal
        * $lt
        * $lte
        * $in => In that data set array
            * db.users.find({name: { $in: ["Kyle","Silly"]}})
            * it return records where name = "Kyle" Or "Silly"
        * $nin => Not In that data set array
        * $exists => is that exists
            * db.users.find({age: {$exists : true}})
            * it return where age field exists
            * it also return null value field 
            * because it check object_id field that age field or not . not check data type/ value
            * for not Exists
                * db.users.find({age: {$exists : false}})
        

        * $and with complex query  
            * db.user.find({age: {$gte: 20, $lte: 40}, name: "Kyle"})
            * every , is treat as AND statement
            * like it above
                * age is greater then 20 AND less then 40 AND name = "Kyle"
            * it is similar like 
                * db.user.find({ $and: [{age: 26},{name: "Kyle"}]})
            * 
        * $or 
            * db.users.find({ $or : [{age: {$lte: 20}}, {name: "Kyle"}]})
            * it return records where age < 20 OR name = "Kyle"
        * $not
            * db.users.find({age: {$not : {$lte: 20}}})
            * it not return records where age < 20
        * $expr
            * it is used to run a query using different field
            * db.users.find($expr: { $gt: ["$dept", "$balance"]})
            * return where column value $dept > column value $balance
        * if you want to find in nested object filed
            * db.users.find({ "address.street: : "123 Main st"})
            * it return address.street = "123 Main st"
            * now you can applied any condition on it
    * findOne
        * findOne
            * it return the first record of match condition
    * countDocuments
        * it return count of documents with match condition

    * UPDATE data Record
        * db.users.update({age: 22} , {$set: {age: 27}});
        * it find all records where age 22 and and set age = 27
        * all prefer update document with _id value

        * updateOne()
            * it update first record that match
            * db.users.updateOne({age: 27}, { $inc: {age: 3}})
            * it find the first record of matched conditions and INCREMENT age with 3
        * $inc
        * $rename
            * $rename : {name: "first"}
        * $unset
            * it delete that column
            * $unset : {age: ""}
            * it remove age record
        * $push
            * it is use to push value in fetch record array field
            * $push : { hobbies: "Bowling"}
        * $pull
            * it is use to pull value / remove particular value from fetch record array field
            * $pull: { hobbies: "Bowling"}
            * it remove Bowling value from hobbies array
        * updateMany
            * it make change every record that match with the conditions
    * replace
        * it is used to reset object with a condition
        * it change entire object with new object 
        * db.users.replaceOne({age: 30}, {name: "John"})
        * it return change object field only
            * i.e
                name : "John" // field only
    * Delete
        * to delete record
        * db.users.deleteOne({name: "John:})
        * db.users.deleteMany({name: "John"})
* # mongoose
    * set up 
        * npm i mongoose
    * connection to database
        * const mongoose = require('mongoose')
        * mongoose.connect("mongoDBServer_url", () => {
            console.log("dddd")
        }, e => console.error)
    * schema 
        * User.js
        * const userSchema = new mongoose.Schema({
            name: {
                type: string
            },
            age: {
                type: number,
                require: true,
                min: 0,
                max: 100, // min and max value to assign
                lowercase: true //it make uppercase
            },
            createdAt: {
                type: Date,
                immutable: true, // restrict to  change
                default: () => new Date.now(), // it run every time we made 
            },
            updatedAt: Date,
            another user 
            hobbies: [String],
            address: {
                street: String,
                city: String
            }

            //nested another type
            bestFriend: {
                type : mongoose.SchemaType.ObjectId,
                ref: "User" //it refer to which collection
            }, // it refer to a id type of 
        })
        * module.exports = mongoose.model("User", userSchema)
            //to user in different files
        * const User = require("./User")
    * Create new User
        * const User = require("/User")
        *   const user = new User({name: "Kyle", age: 26});
        * user.save().then(() => console.log())
        * Best Way
            * const user  = await User.create({name: "Kyle", age: 26})
            * 
    * Update
        * user.name = "jjjj"
        * user.save()
    * nested Schema
        * const addressSchema = new mongoose>Schema({
            street: String,
            city: String,
        });
        * const userSchema = new mongoose.Schema({
            name: String,
            ...
            address: addressSchema,
        })
    * custom validator to schema
        * 
        * age: {
            type: number,
            validate: {
                validator: v => v%2 === 0,
                message: props => `${props.value} is not an even number`,
            }
        }
        * Some of the method are not applied validate method , some are just pass
    * findById
    * Own Query
        * const user = await User.where("name").equals("Kyle")
        * it work as same as find 
        * const user = await User
            .where("age")
            .gt(12)
            .lt(33)
            .where("name")
            .equals("Kyle")
            .populate("bestFriend") // refer User to a user SO now it show the date of User that has contain Id 

            .limit(2)
            .select("age") //return age only
    * Method for every instance of schema
        //it use function name function Not Arrow function Because it uses This for refer schema value.
        * userSchema.methods.sayHi = function() {
            console.log('Hi ... is ${this.name})
        }
        * // all of the User has this method

        * user.sayHi() // can call this method


    * Method for all over schema that work as static
        * it work as User.find  method
        * userSchema.statics.findByName(function (name) {
            return this.where({name: new RegExp(name, 'i')})
        })
        // it return name = given name
        //Call
        * const user = await User.findByName("Kyle")
    * Query Method
        * it is used as Query over another method
        * it is not able to call it directly
        * it is a extra query
        * userSchema.query.byName = function(name) {
            return this.where({name: RegExp(name. "i")})
        }
        * call
        * const user = User.find().byName("Kyle")
        * const user = User.byName(kyle") // error 

    * virtual
        * it is virtual properties that based on properties which is already there
        * it is going to return as a properties on that schema

        * UserSchema.virtual('virtualFunctionName').get(function () {

            return `${this.name} << ${this.email}`
        })
        * // when we call find on records
        * then it also return this virtual properties
        * it is not save on database
    * Middleware on mongoose
        * userSchema.pre("save", function(next) {
            this.updatedAt = Date.now()
            next()
        })
        * userSchema.post("save", function(doc, next) {
            //this is not work here , Because it pass the save method . this not refer record
            * //instead , we get on first props
            doc.syHi()
            next()
        })


















    
    
        

             