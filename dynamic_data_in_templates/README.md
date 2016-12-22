# Dynamic data in templates

We have different pieces in place: the data is in `db.json`, we have `index` in `app.py` and the template added. But how will we actually make our posts appear in our HTML template? Because that is what we want to do – take some content (models saved in the database) and display it nicely in our template, right?

This is exactly what *views* are supposed to do: connect models and templates. In our `index` *view* we will need to take the models we want to display and pass them to the template. In a *view* we decide what (model) will be displayed in a template.

OK, so how will we achieve this?

We need to open our `app.py`. So far `index` *view* looks like this:

{% filename %}app.py{% endfilename %}
```python
@route('/')
def index():
  '''
  db = TinyDB("db.json")
  posts = db.table("posts")
  '''
  return template('index.tpl')
```
But, there was a problem.  None of the data from our database was actually showing up in the webpage.  That was partially due to the fact that we were not sending the data to the template.  Change `app.py` in the following manner to fix this error.

{% filename %}app.py{% endfilename %}
```python
@route('/')
def index():
  db = TinyDB("db.json")
  posts = db.table("posts")
  return template('index.tpl', posts=list(posts.all()))
```


That's it! Time to go back to our template and display this QuerySet!

*Note: Still nothing will have changed on your webpage, we still need to utilize template variables.*
