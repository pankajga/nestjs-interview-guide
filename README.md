# nestjs-interview-guide

1. How do you use Redis in Node.js?

Redis is an in-memory data store used for caching and data storage in a Node.js application. Here's an example of using Redis to cache data:

javascriptCopy code
const redis = require('redis');
const client = redis.createClient();

function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = 'Data fetched';
      resolve(data);
    }, 2000);
  });
}

async function getCachedData() {
  const data = await client.get('data');
  if (data) {
    console.log('Data retrieved from cache');
    return data;
  }
  const newData = await fetchData();
  await client.set('data', newData);
  console.log('Data retrieved from server');
  return newData;
}

getCachedData().then((data) => {
  console.log(data);
}).catch((error) => {
  console.error(error);
});
2. How do you use MongoDB in Node.js?

MongoDB is a popular NoSQL database used in Node.js applications. Here's an example of using the official MongoDB Node.js driver to connect to a MongoDB database:

javascriptCopy code
const { MongoClient } = require('mongodb');

async function main() {
  const uri = 'mongodb://localhost:27017';
  const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });
  try {
    await client.connect();
    console.log('Connected to MongoDB');
    const database = client.db('mydb');
    const collection = database.collection('mycollection');
    await collection.insertOne({ name: 'John' });
    const documents = await collection.find().toArray();
    console.log(documents);
  } catch (error) {
    console.error(error);
  } finally {
    await client.close();
    console.log('Disconnected from MongoDB');
  }
}

main();
3. How do you use Mongoose in Node.js?

Mongoose is an Object Document Mapping (ODM) library for MongoDB in Node.js. It provides a way to define models and schemas for MongoDB documents and makes it easier to interact with MongoDB in a Node.js application. Here's an example:

javascriptCopy code
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/mydb', { useNewUrlParser: true, useUnifiedTopology: true });

const personSchema = new mongoose.Schema({
  name: String,
  age: Number
});

const Person = mongoose.model('Person', personSchema);

const person = new Person({
  name: 'John',
  age: 30
});

person.save().then(() => {
  console.log('Person saved');
}).catch((error) => {
  console.error(error);
});
4. How do you use JWT in Node.js?

JSON Web Tokens (JWT) is a way to securely transmit information between parties in a Node.js application. Here's an example of using the jsonwebtoken library to sign and verify JWTs:

javascriptCopy code
const jwt = require('jsonwebtoken');

const secret = 'mysecret';

const payload = {
  name: 'John',
  email: 'john@example.com'
};

const token = jwt.sign(payload, secret, { expiresIn: '1h' });

console.log(token);

jwt.verify(token, secret, (error, decoded) => {
  if (error) {
    console.error(error);
  } else {
    console.log(decoded);
  }
});
5. How do you use Axios in Node.js?

Axios is a popular library used for making HTTP requests in a Node.js application. Here's an example:

javascriptCopy code
const axios = require('axios');

async function fetchData() {
  try {
    const response = await axios.get('<https://jsonplaceholder.typicode.com/posts>');
    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
}

fetchData();
6. How do you use Node.js streams?

javascriptCopy code
const fs = require('fs');

const readableStream = fs.createReadStream('input.txt');

readableStream.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});

readableStream.on('end', () => {
  console.log('Finished reading data.');
});

readableStream.on('error', (error) => {
  console.error(error);
});
