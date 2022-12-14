# Mongo DB cheat sheet

## Show All Databases

```BASH
show dbs
```

## Show Current Database

```BASH
db
```

## Create Or Switch Database

```BASH
use acme
```

## Drop

```BASH
db.dropDatabase()
```

## Create Collection

```BASH
db.createCollection('posts')
```

## Show Collections

```BASH
show collections
```

## Insert Row

```BASH
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```BASH
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

## Get All Rows

```BASH
db.posts.find()
```

## Get All Rows Formatted

```BASH
db.find().pretty()
```

## Find Rows

```BASH
db.posts.find({ category: 'News' })
```

## Sort Rows

```BASH
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

## Count Rows

```BASH
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```

## Limit Rows

```BASH
db.posts.find().limit(2).pretty()
```

## Chaining

```BASH
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```

## Foreach

```BASH
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

## Find One Row

```BASH
db.posts.findOne({ category: 'News' })
```

## Find Specific Fields

```BASH
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Update Row

```BASH
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field

```BASH
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

## Increment Field (\$inc)

```BASH
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

## Rename Field

```BASH
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```BASH
db.posts.remove({ title: 'Post Four' })
```

## Sub-Documents

```BASH
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```BASH
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

## Add Index

```BASH
db.posts.createIndex({ title: 'text' })
```

## Text Search

```BASH
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

## Greater & Less Than

```BASH
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```