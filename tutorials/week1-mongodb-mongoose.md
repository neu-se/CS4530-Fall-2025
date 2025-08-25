---
layout: page
title: MongoDB and Mongoose
permalink: /tutorials/week1-mongodb-mongoose
parent: Tutorials
nav_order: 5
---

# A mini-tutorial on MongoDB and Mongoose

This tutorial provides basic introduction to MondoDB and Mongoose:

Contents:

- [MongoDB Concepts](#mongodb-concepts)
- [Mongoose representation of MongoDB Concepts](#mongoose-representation-of-mongodb-concepts)
- [Databases, Collections, and Documents](#databases-collections-and-documents)
- [ObjectIDs and References](#objectids-and-references)
- [Queries](#queries)
- [Populate](#populate)
- [Examples](#examples)
- [Resources](#resources)

## MongoDB Concepts

- An _installation_ consists of a set of named _databases_.
- A _database_ consists of a set of named _collections_.
- A _collection_ consists of a set of _documents_.
- A _document_ is a set of (property,value) pairs.
- A _schema_ is a set of (property,type) pairs. All of the documents in a single collection should satisfy the same _schema_.

## Mongoose representation of MongoDB Concepts

### Databases, Collections, and Documents

Mongoose provides representations of MongoDB concepts in the TypeScript/JavaScript language.

- In any given program `mongoose` refers to a particular database in a particular MongoDB instance. For example, executing

  ```typescript
  await mongoose.connect("mongodb://127.0.0.1:27017/pets");
  ```

  connects Mongoose to the pets database in the local MongoDB instance.

- A MongoDB schema is represented in Mongoose by an object of class `mongoose.Schema`. For example:

  ```typescript
  const kittySchema = new mongoose.Schema({
    name: String,
    color: String,
  });
  ```

  creates `kittySchema` to represent a MongoDB schema with two properties: `name` and `color`, both of type `String`.

  References to other documents are represented by properties with type `Types.ObjectID` (more on this later).

  In this document, we will use the terms 'property' and 'field' interchangeably.

- A MongoDB collection of documents
  is represented in Mongoose by a TypeScript constructor created by `mongoose.model`. For example

  ```typescript
  const Kitten = mongoose.model("Kitten", kittySchema);
  ```

  associates the `Kitten` variable with a collection named `Kitten`. Notice that Kitten is a constructor (like a class name), so
we write it in upper case. All documents in this collection must follow the schema defined by `kittySchema`.

- A document with schema `M` is represented by a TypeScript object created by saying `new C`, where `C` is constructor created by `mongoose.model`. For example

  ```typescript
  const fluffy = new Kitten({ name: "fluffy", color: "black" });
  ```

  creates a document intended for insertion in the collection named `Kitten`.

- In Mongoose, creation of a document is separate from being inserted in a collection. So, to actually insert `fluffy` in the `Kitten` collection, we need to execute

  ```typescript
  await fluffy.save();
  ```

Note that most of the operations that touch the database are asyncs.

### ObjectIDs and References

In MongoDB, every document has a unique identifier stored in its `_id` field. This `_id` field is automatically generated if not explicitly provided when a document is created.

By default, it is an ObjectId, a 12-byte value consisting of a 4-byte timestamp (indicating creation time), a 5-byte random value (unique to the server), and a 3-byte incrementing counter (ensuring uniqueness within the same timestamp). This structure ensures global uniqueness and supports efficient queries and indexing.

As mentioned above, references to documents are represented by properties with type `Types.ObjectID`, which is the type of the `_id` field.

### Queries

In Mongoose, a query is a recipe for retrieving documents from a collection. There are **lots** of ways to do this. Here are some examples:

- Find all documents in a collection:

  ```typescript
  Dog.find();
  ```

- Find one document with specific criteria:

  ```typescript
  Dog.findOne({ name: "Buddy" });
  ```

- Find multiple documents with specific criteria:
  ```typescript
  Dog.find({ breed: "Labrador" });
  ```

Note: These methods are asynchronous, so you need to use await.

#### Query Syntax

Mongoose offers many methods for querying, including JSON-style queries and the query builder syntax. Here’s an example that demonstrates both:

- Using a JSON-object query:

  ```typescript
  Person.find({
    occupation: /host/, // this is a regular expression that matches any words with 'host' within them, e.g. 'ghost', 'hostess'
    "name.last": "Ghost",
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ["vaporizing", "talking"] },
  })
    .limit(10)
    .sort({ occupation: -1 })
    .select({ name: 1, occupation: 1 })
    .exec(callback);
  ```

- Using the query builder:

  ```typescript
  Person.find({ occupation: /host/ })
    .where("name.last")
    .equals("Ghost")
    .where("age")
    .gt(17)
    .lt(66)
    .where("likes")
    .in(["vaporizing", "talking"])
    .limit(10)
    .sort("-occupation")
    .select("name occupation")
    .exec(callback);
  ```

For small projects like the one in the course, it is probably preferable to use the simplest Mongoose queries you can, and then process the list of documents that the query returns.

There are some circumstances where it is helpful to the query do more work. Consider the following example from the codebase:

```typescript
const q = await QuestionModel.findOneAndUpdate(
  { _id: qid },
  { $addToSet: { views: username } },
  { new: true }
);
```

Here’s what happens step by step:

1. Find the document with the matching `_id`.
2. Update the views field to add a username if it doesn’t already exist (using $addToSet).
3. Return the updated document instead of the original with the { new: true } option.

Using findOneAndUpdate offers several advantages over manually retrieving, modifying, and saving documents:

- **Atomicity**: The operation is performed atomically, ensuring data consistency. This avoids race conditions that could occur if multiple processes attempt to update the same document simultaneously.

- **Efficiency**: It combines the find and update steps into a single database operation, reducing the number of queries sent to MongoDB.

- **Clean Code**: It eliminates the need for intermediate checks and manual updates, resulting in more concise and readable code.

If we were to write code to process everything ourselves, it might look like this:

```typescript
const question = await QuestionModel.findOne({ _id: qid });

// Check if the username is already in the views array
if (!question.views.includes(username)) {
  question.views.push(username);
}

// Save the updated question document
const updatedQuestion = await question.save();
```

While this approach works, it requires:

- Two separate database operations: findOne and save.
- Additional checks for modifications (like views.includes).
- Increased risk of conflicts in concurrent environments.

By using findOneAndUpdate, you streamline the operation, make it more robust, and let MongoDB handle the heavy lifting.

### Populate

As mentioned before, documents can reference other documents in MongoDB through the ObjectID fields. In the database, this information is stored as the ID itself, rather than the object. This is super useful for storage purposes, but when we want to access and use the information, we need more than just the ID. That's where the `populate` function comes in, allowing you to replace these simple references with the actual documents, simplifying the retrieval of data. `populate` will query the reference IDs in each document found to be returned, and replace the ID with the actual object value from the database. 

#### How Populate Works

Imagine we have two collections: `User`s and `Post`s. Each `Post` references a `User` in the `author` field by the ObjectID. The schemas and models would be defined as:

```typescript
const postSchema = new mongoose.Schema({
  title: String,
  content: String,
  // author: User is invalid, because "User" is not a legal type for a schema definition
  author: { type: mongoose.Schema.Types.ObjectId, ref: "User" },
});

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
});

const User = mongoose.model("User", userSchema);
const Post = mongoose.model("Post", postSchema);
```



When querying for a post, we would normally just receive the ObjectID in the `author` field, such as:

```typescript
{
    _id: "6754b691a33023f3e1fe9604",
    title: "Intro to MongoDB",
    content: "MongoDB is a database with a lot of features!",
    author: "6754b691a33023f3e1ff9008"
}
```

To retrieve the actual user document, use `populate`:

```typescript
const posts = await Post.find({ _id: "6754b691a33023f3e1fe9604" }).populate("author");
```

which replaces the ObjectID in the author field with the referenced `User` document:

```typescript
{
  _id: "6754b691a33023f3e1fe9604",
  title: "Intro to MongoDB",
  content: "MongoDB is a database with a lot of features!",
  author: {
    _id: "6754b691a33023f3e1ff9008",
    name: "John Doe",
    email: "john@example.com"
  }
}
```

It's important to note that `populate` with **only** populate the reference IDs that you specifically mention in the function call. This is especially important to keep in mind for documents with nested fields containing ObjectID references.

For example, let's extend the `User` schema to contain a `profile` field:

```typescript
const profileSchema = new mongoose.Schema({
  bio: String,
  following: [{ type: String }],
});

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  profile: { type: mongoose.Schema.Types.ObjectId, ref: "Profile" },
});

const Profile = mongoose.model("Profile", profileSchema);
const User = mongoose.model("User", userSchema);
```

Now, if we were to execute the previous `populate` query, the returned object would look like:

```typescript
{
  _id: "6754b691a33023f3e1fe9604",
  title: "Intro to MongoDB",
  content: "MongoDB is a database with a lot of features!",
  author: {
    _id: "6754b691a33023f3e1ff9008",
    name: "John Doe",
    email: "john@example.com",
    profile: "6754b692a33023f4e5be2413"
  }
}
```

To access the object stored with the reference ID, we need to specify populating the field in the query:

```typescript
const posts = await Post.find({ _id: "6754b691a33023f3e1fe9604" }).populate({
  path: "author",
  populate: {
    path: "profile",
    model: Profile,
  },
});
```

which would return the completely populated document:

```typescript
{
  _id: "6754b691a33023f3e1fe9604",
  title: "Intro to MongoDB",
  content: "MongoDB is a database with a lot of features!",
  author: {
    _id: "6754b691a33023f3e1ff9008",
    name: "John Doe",
    email: "john@example.com",
    profile: {
        _id: "6754b692a33023f4e5be2413",
        bio: "My name is John",
        following: ["CS4530"]
    }
  }
}
```

Some additional, advanced examples:

- Select specific fields in the populated document:

  ```typescript
  const posts = await Post.find({ _id: "6754b691a33023f3e1fe9604" }).populate("author", "name");
  ```

  Returns:

  ```typescript
    {
      _id: "6754b691a33023f3e1fe9604",
      title: "Intro to MongoDB",
      content: "MongoDB is a database with a lot of features!",
      author: {
        _id: "6754b691a33023f3e1ff9008",
        name: "John Doe",
      }
    }
  ```

- Filter the populated documents:

  ```typescript
  const posts = await Post.find().populate({
    path: "author",
    match: { email: /example\.edu$/ },
    select: "name email",
  });
  ```

  ```typescript
  [{
    _id: "6754b691a33023f3e1fe9604",
    title: "Intro to MongoDB",
    content: "MongoDB is a database with a lot of features!",
    author: {
        _id: "6754b691a33023f3e1ff9158",
        name: "Jane Doe",
        email: "jane@example.edu"
    }
  },
  {
    _id: "6754b691a33023f4b2da2528",
    title: "Understanding populate",
    content: "You can do a lot with populate!",
    author: {
        _id: "6754b691c63175b2d1fc6490",
        name: "Jack Doe",
        email: "jack@example.edu"
    }
  }]
  ```

#### Why Use Populate

By using populate, you minimize boilerplate code for nested retrieval and ensure data consistency. You only need to ensure the one copy is updated, which is referenced in other places. This approach is especially useful with complex relationships as it reduces errors, simplifies data retrieval, and improves consistency by automating the lookup of references.

However, if you find yourself using deeply nested populates, it's worth revisitng the database design and trying to simplify the schemas. Under the hood, populate executes additional queries for you, which can become very inefficient as database complexity and query size increase. In this toy example, we may want to get rid of the `Profile` collection, and instead define the fields directly within the `User` schema. These design decisions depend on the context and needs of the system.

### Examples

A simple example (i.e, example.ts) can be accessed [here](./assets/week1-mongodb-mongoose/tutorial.zip).

### Resources

- [Official Mongoose/TypeScript docs](https://mongoosejs.com/docs/typescript.html)
- [Mongoose Queries](https://mongoosejs.com/docs/queries.html)
