# Database Interacation in Web Applications

This demonstrates the cconnection of MySQL database and Node.js to create a simple API

## Requirements
- [Node.js](https://nodejs.org/) installed
-  MySQL installed and running
-  A code editor, like [Visual Studio Code](https://code.visualstudio.com/download)

## Setup
1. Clone the repository
2. Initialize the node.js environment
   ```
   npm init -y
   ```
3. Install the necessary dependancies
   ```
   npm install express mysql2 dotenv nodemon
   ```
4. Create a ``` server.js ``` and ```.env``` files
5. Basic ```server.js``` setup
   <br>
   
   ```js
   const express = require('express')
   const app = express()

   
   // Question 1 goes here


   // Question 2 goes here


   // Question 3 goes here


   // Question 4 goes here

   

   // listen to the server
   const PORT = 3000
   app.listen(PORT, () => {
     console.log(`server is runnig on http://localhost:${PORT}`)
   })
   ```
<br><br>

## Run the server
   ```
   nodemon server.js
   ```
<br><br>

## Setup the ```.env``` file
```.env
DB_USERNAME=root
DB_HOST=localhost
DB_PASSWORD=your_password
DB_NAME=hospital_db
```

<br><br>

## Configure the database connection and test the connection
Configure the ```server.js``` file to access the credentials in the ```.env``` to use them in the database connection

<br>

## 1. Retrieve all patients
Create a ```GET``` endpoint that retrieves all patients and displays their:
- ```patient_id```
- ```first_name```
- ```last_name```
- ```date_of_birth```

<br>

## 2. Retrieve all providers
Create a ```GET``` endpoint that displays all providers with their:
- ```first_name```
- ```last_name```
- ```provider_specialty```

<br>

## 3. Filter patients by First Name
Create a ```GET``` endpoint that retrieves all patients by their first name

<br>

## 4. Retrieve all providers by their specialty
Create a ```GET``` endpoint that retrieves all providers by their specialty

<br>

// // Declare dependences
// const express = require('express');
// const app = express();
// const mysql = require("mysql2");
// const dotenv = require('dotenv');
// const cors=require('cors');

// app.use(express.json());
// app.use(cors());
// dotenv.config();

// //Connect to the database ***
// const db = mysql.createConnection({
//     host: process.env.DB_HOST,
//     user: process.env.DB_USER,
//     password: process.env.DB_PASSWORD,
//     database: process.env.DB_NAME
// }); 

// Declare dependencies / variables
const express = require("express");
const app = express();
const mysql = require("mysql2");
const dotenv = require("dotenv");
const cors = require("cors");

app.use(express.json());
app.use(cors());
dotenv.config();

// Connect to the database
const db = mysql.createConnection({
  host: process.env.DB_HOST,
  user: process.env.DB_USERNAME,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
});


// Set view engine to EJS
app.set("view engine", "ejs");
app.set("views", __dirname + "/views");

// GET method to retrieve data from the database
app.get("/data", (req, res) => {
  db.query("SELECT * FROM patients", (err, results) => {
    if (err) {
      console.error(err);
      res.status(500).send("Error retrieving data");
    } else {
      // Render the data in the template
      res.render("data", { results });
    }
  });
});

// Question 1 goes here
// Assume 'db' is your MySQL connection
console.log("Connected to MySQL successfully as id:", db.threadId);


app.get('/', (req, res) => {
   
    const patient_id = 949; 
    const first_name = 'Oluwatosin'; 
    const last_name = 'Ayoola'; 
    const date_of_birth = '1990-04-28'; 

    // Sending a single response with all data
    res.json({
        patient_id: patient_id,
        first_name: first_name,
        last_name: last_name,
        date_of_birth: date_of_birth
    });
});
// Question 2 goes here

app.get('/', (req, res) => {
   
   
    const first_name = 'Oluwatosin'; 
    const last_name = 'Ayoola'; 
    const provider_specialty = 'neurologist'; 

    // Sending a single response with all data
    res.json({
        first_name: first_name,
        last_name: last_name,
        provider_specialty: neurologist,
    });
});

// Question 3 goes here

// Connect to MySQL
db.connect((err) => {
    if (err) {
        console.error("Couldn't connect to the database:", err);
        return;
    }
    console.log("Connected to MySQL successfully as id:", db.threadId);
});

// Define a route to retrieve all patients
app.get('/patients', (req, res) => {
    const sqlQuery = 'SELECT patient_id, FROM patients';
    
    db.query(sqlQuery, (err, results) => {
        if (err) {
            return res.status(500).json({ error: err.message });
        }
        
        // To send the results as a JSON response
        res.json(results);
    });
});

// Question 4 goes here

app.get('/patients/specialty/:specialty', (req, res) => {
    const { specialty } = req.params;  

    const sqlQuery = 'SELECT patient_id, first_name, last_name, date_of_birth, specialty FROM patients WHERE specialty = ?';
    
    db.query(sqlQuery, [specialty], (err, results) => {
        if (err) {
            return res.status(500).json({ error: err.message });
        }

        if (results.length === 0) {
            return res.status(404).json({ message: 'No patients found for this specialty' });
        }
        // To send the results as a JSON response
        res.json(results);
    });
});
// listen to the server
const PORT = 3000
app.listen(PORT, () => {
  console.log(`server is runnig on http://localhost:${PORT}`)
})

## NOTE: Do not fork this repository
