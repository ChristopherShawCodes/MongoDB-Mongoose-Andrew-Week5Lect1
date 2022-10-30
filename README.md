# MongoDB-Mongoose-Andrew-Week5Lect1

Coding Dojo Week 5 Lecture 1

Youtube: https://www.youtube.com/watch?v=CssaK8VDtkU

----------------------------------------
Server.js File

const express = require('express')

const mongoose = require('mongoose')

const app = express()

const PORT = 8000

const DB = 'testdb3'

//middleware to make post requests

app.use(express.json())

app.use(express.urlencoded({extended: true}))

//connect to mongodb

mongoose.connect(`mongodb://localhost/${DB}`, ()=>{

    console.log(`Connected to MongoDB ${DB}`)
    
})


//schema determines the blueprint for the documents

const UserSchema = mongoose.Schema({

    name: String,
    
    age: Number,
    
    developer: Boolean
    
})

//turns schema into a model which creates a collection in the database

const User = mongoose.model('User', UserSchema)

app.post('/api/addUser', (req,res)=>{

    User.create(req.body)
    
    .then((result) =>{
    
        res.json(result)
        
    }).catch(err => console.log(err))
    
})

app.get('/api/allUsers', (req,res)=>{

    User.find()
    
    .then((result) =>{
    
        res.json(result)
        
        
    }).catch(err => console.log(err))
    
})

app.listen(PORT, () =>{

    console.log(`Server is up and running on port ${PORT}`)
    
})

//From here we can use Postman to POST  a user

//Confirm entry with Compass
