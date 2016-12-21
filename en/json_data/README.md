# JSON data

What we want to create now is something that will store all the posts in our blog. But to be able to do that we need to talk a little bit about data.

## Data

There are lots of different ways to store and retrieve information on the web, but one of the most popular and easy to use is JSON.  JSON stands for Java Script Object Notation.  JSON is easy to read and easy to process.  For this tutorial, we will be persisting our data to a file and reading from it with a Python package called TinyDB.  This will allow us to bypass the complexity of databases, for now.  It is not a typical way of handling data and you will need to learn more robust technologies if you ever build a larger application.

JSON is pretty flexible on schema (database design), but we'll keep it simple with some basic key-value pairings.  Look below how I take a table of values and convert it to JSON.

```
NAME      AGE      GENDER
---------------------------
Wes       33       male
Rick      22       male

{
  "people" :
    {
      "1" :  
        {
          "name": "Wes",
          "age": 33,
          "gender" : "male"
        },
      "2" :
        {
          "name" : "Rick",
          "age" : 22,
          "gender" : "male"
        }
    }
}
```

Notice the similarities between JSON and a Python dictionary, that will certainly help as we learn to access and modify the data inside the database file.

Time to make our database file.  In your `bottleboys` project directory, create this file.  Feel free to change the values for author, date and body.

{% filename %}db.json{% endfilename %}
```
{
  "posts" :
    {
      "1" :  
        {
          "postId" : "1",
          "author" : "Wes Basinger",
          "date" : "2016 12 21",
          "body" : "This is my first post with of my new blog, I hope you like it!",
          "comments" : []
        },
      "2" :
        {
          "postId" : "2",
          "author" : "Wes Basinger",
          "date" : "2016 12 24",
          "body" : "It's Christmas Eve, I'm so excited!",
          "comments" : []
        }
    }
}
```
This is what is called seed data.  Later on, we will write our application in such a way that we can add posts dynamically.

# Accessing our data through the shell

Just to get a feel for how our data is stored and how we can access it, we'll use the Python shell to access it.  TinyDB has some easy methods to work with.

{% filename %}python shell{% endfilename %}
```
>>> from tinydb import TinyDB
>>> db = TinyDB('db.json')
>>> posts = db.table("posts")
>>> posts.all()
[{u'date': u'2016 12 21', u'body': u'This is my first post with of my new blog, I hope you like it!', u'postId': u'1', u'comments': [], u'author': u'Wes Basinger'}, {u'date': u'2016 12 24', u'body': u"It's Christmas Eve, I'm so excited!", u'postId': u'2', u'comments': [], u'author': u'Wes Basinger'}]
```

And now you can see, all of our posts made it into the database.  TinyDB has lots of methods for modifying our database, all of them are CRUD operations.

CRUD stands for create, read, update, and delete.  These are the basic things we will need to do with our data.  For now, we won't need to think about the database until we get into some topics involving different routes for your web app.
