# Introduction
Creating a blog API using Express.js and Mongoose can be a great way to learn how to build a RESTful API. In this post, we will cover how to set up an Express.js server, define a Mongoose schema for blog posts, and implement CRUD (Create, Read, Update, Delete) operations for the blog post API.

## Setting Up the Server
To get started, we need to create a new Node.js project and install the necessary dependencies. We can do this by running the following commands:

```bash
mkdir blog-api
cd blog-api
npm init -y
npm install express mongoose body-parser
```
> Next, let's create an app.js file in the root of our project and add the following code:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');

// Set up Express app
const app = express();
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// Connect to MongoDB
mongoose.connect('mongodb://localhost/blog-api', { useNewUrlParser: true, useUnifiedTopology: true });
mongoose.Promise = global.Promise;

// Start server
const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```
In this code, we set up our Express app and connect to a local MongoDB database named "blog-api". We also start the server on port 3000.

## Defining the Blog Post Schema
> Next, let's define a Mongoose schema for blog posts. A blog post should contain a title, body, author, date, and tags. We can define this schema as follows:

```javascript
const mongoose = require('mongoose');

const blogPostSchema = new mongoose.Schema({
  title: { type: String, required: true },
  body: { type: String, required: true },
  author: { type: String, required: true },
  date: { type: Date, default: Date.now },
  tags: { type: [String], required: true }
});

module.exports = mongoose.model('BlogPost', blogPostSchema);
```
In this code, we define a new Mongoose schema named "blogPostSchema" that includes five properties: ` title, body, author, date, and tags. The title, body, and author properties are required`, while the date property defaults to the current date and the tags property is an array of strings.

# Implementing CRUD Operations
Now that we have our server set up and our schema defined, let's implement CRUD operations for the blog post API. We will create routes for creating, reading, updating, and deleting blog posts.

## Creating a Blog Post
To create a new blog post, we need to define a `POST` route that takes a JSON payload containing the properties of the blog post. We can implement this as follows:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const BlogPost = require('./models/blogPost');

// Set up Express app
const app = express();
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// Connect to MongoDB
mongoose.connect('mongodb://localhost/blog-api', { useNewUrlParser: true, useUnifiedTopology: true });
mongoose.Promise = global.Promise;

// Define routes
app.post('/blog-posts', (req, res) => {
  const blogPost = new BlogPost(req.body);

  blogPost.save()
    .then(() => {
      res.status(201).send(blogPost);
    })
    .catch((error) => {
      res.status(400).send(error);
    });
});
```

In this code, we define a `POST` route for `/blog-posts` that creates a new `BlogPost `object from the JSON payload in the request body. 
We then save the new blog post to the database using the `save() `method and return a 201 `Created response` with the new blog post in the `response body`. If there is an error, we return a `400 Bad Request response with the error message` in the response body.

## Reading Blog Posts
To read a list of all blog posts, we can define a GET route as follows:

```javascript
app.get('/blog-posts', (req, res) => {
  BlogPost.find()
    .then((blogPosts) => {
      res.send(blogPosts);
    })
    .catch((error) => {
      res.status(500).send(error);
    });
});
```

In this code, we define a GET route for `/blog-posts` that returns all blog posts in the database. We use the `find()` method to query the database and return the results in the response body.
If there is an error, we return a   500 Internal Server Error  `response with the error message in the response body.

To read a single blog post by ID, we can define a   `GET` route as follows:
```javascript
app.get('/blog-posts/:id', (req, res) => {
  BlogPost.findById(req.params.id)
    .then((blogPost) => {
      if (!blogPost) {
        return res.status(404).send();
      }

      res.send(blogPost);
    })
    .catch((error) => {
      res.status(500).send(error);
    });
});

```

In this code, we define a GET route for /blog-posts/:id that returns a single blog post by ID. We use the `findById()` method to query the database and return the result in the response body. 
If the blog post is not found, we return a` 404 Not Found response`. If there is an error, we return a 500 Internal Server Error response with the error message in the response body.

## Updating a Blog Post
To update a blog post by ID, we can define a PUT route as follows:
```javascript
app.put('/blog-posts/:id', (req, res) => {
  BlogPost.findByIdAndUpdate(req.params.id, req.body, { new: true })
    .then((blogPost) => {
      if (!blogPost) {
        return res.status(404).send();
      }

      res.send(blogPost);
    })
    .catch((error) => {
      res.status(500).send(error);
    });
});
```
In this code, we define a `PUT` route for `/blog-posts/:id` that updates a blog post by ID. 
We use the `findByIdAndUpdate()` method to query the database, `update` the blog post with the new values in the request body, and return the updated blog post in the response body. 
We pass the` { new: true } `option to the method to ensure that the updated blog post is returned instead of the old one. If the blog post is not found, we return a `404 Not Found response`. 
If there is an error, we return a `500 Internal Server Error `response with the error message in the response body.

## Deleting a Blog Post
To delete a blog post by ID, we can define a DELETE route as follows:

```javascript

app.delete('/blog-posts/:id', (req, res) => {
  BlogPost.findByIdAndDelete(req.params.id)
    .then((blogPost) => {
      if (!blogPost) {
        return res.status(404).send();
      }

      res.send(blogPost);
    })
    .catch((error) => {
      res.status(500).send(error);
    });
});
```

In this code, we define a `DELETE` route for `/blog-posts/:id `that deletes a blog post by ID. We use the `findByIdAndDelete()` method to query the database, delete the blog post, and return the deleted blog post in the response body. If the blog post is not found,
we return a `404 Not Found response`. If there is an error, we return a `500 Internal Server Error` response with the error message in the response body.

## Conclusion
> In this blog post, we have seen how to create a blog API using Express and Mongoose. We have defined a schema for the blog post model, created routes for CRUD operations, and implemented each operation with the relevant Mongoose method. With this knowledge, you should be able to create your own APIs using Express and MongoDB
