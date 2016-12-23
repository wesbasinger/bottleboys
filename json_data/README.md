# JSON data

What we want to create now is something that will store all the posts in our blog. But to be able to do that we need to talk a little bit about data.

## Data

There are lots of different ways to store and retrieve information on the web, but one of the most popular and easy to use is JSON.  JSON stands for Java Script Object Notation.  JSON is easy to read and easy to process.  For this tutorial, we will be persisting our data to a file and reading from it with a Python package called TinyDB.  This will allow us to bypass the complexity of databases, for now.  It is not a typical way of handling data and you will need to learn more robust technologies if you ever build a larger application.

JSON is pretty flexible on schema (database design), but we'll keep it simple with some basic key-value pairings.  Look below how I take a table of values and convert it to JSON.  This is a little more nested than a normal JSON structure, but it's going to work well with TinyDB.

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

Time to make our database file.  In your `bottleboys` project directory, create this file.  Feel free to change the values for author, date and body.  Save it when you are finished.

{% filename %}db.json{% endfilename %}
```
{
  "posts" :
    {
      "1" :  
        {
          "postId" : "1",
          "author" : "Wes Basinger",
          "title" : "First Post",
          "date" : "2016-12-21",
          "body" : "This is my first post with of my new blog, I hope you like it!"
        },
      "2" :
        {
          "postId" : "2",
          "author" : "Wes Basinger",
          "title" : "Second Post",
          "date" : "2016-12-24",
          "body" : "It's Christmas Eve, I'm so excited!"
        }
    }
}
```
This is what is called seed data.  Later on, we will write our application in such a way that we can add posts dynamically.

# Accessing our data through the shell

Just to get a feel for how our data is stored and how we can access it, we'll use the Python shell to access it.  TinyDB has some easy methods to work with.  First `pip install tinydb` on the command line.  Should look something like this.

{% filename %}command line{% endfilename %}
```
(myvenv)cabox@box-codeanywhere:~/workspace/bottleboys$ pip install tinydb                                   
Downloading/unpacking tinydb                                                                              
  Downloading tinydb-3.2.1.zip
  Running setup.py (path:/home/cabox/workspace/bottleboys/myvenv/build/tinydb/setup.py) egg_info for package tinydb         
Installing collected packages: tinydb                  
  Running setup.py install for tinydb       
Successfully installed tinydb                                     
Cleaning up...
(myvenv)cabox@box-codeanywhere:~/workspace/bottleboys$  
```
Then you can open up a Python shell and run the following set of commands.

{% filename %}python shell{% endfilename %}
```
>>> from tinydb import TinyDB
>>> db = TinyDB('db.json')
>>> posts = db.table("posts")
>>> posts.all()
[{u'date': u'2016 12 21', u'body': u'This is my first post with of my new blog, I hope you like it!', u'postId': u'1', u'author': u'Wes Basinger', u'title': u'First Post'}, {u'date': u'2016 12 24', u'body': u"It's Christmas Eve, I'm so excited!", u'postId': u'2', u'author': u'Wes Basinger', u'title': u'Second Post'}]
```

And now you can see, all of our posts made it into the database.  TinyDB has lots of methods for modifying our database, all of them are CRUD operations.

CRUD stands for create, read, update, and delete.  These are the basic things we will need to do with our data.  For now, we won't need to think about the database until we get into some topics involving different routes for your web app.
