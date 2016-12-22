# Bottle templates

Time to display some data! Bottle gives us some helpful built-in __template tags__ for that.

## What are template tags?

You see, in HTML, you can't really write Python code, because browsers don't understand it. They know only HTML. We know that HTML is rather static, while Python is much more dynamic.

__Bottle template tags__ allow us to transfer Python-like things into HTML, so you can build dynamic websites faster and easier. Cool!

## Display index template

In the previous chapter we gave our template a list of posts in the `posts` variable. Now we will display it in HTML.

To print a variable in Bottle templates, we use double curly brackets with the variable's name inside, like this:

```
{{ posts }}
```

Bottle understands posts is a list of objects. Remember from __Introduction to Python__ how we can display lists? Yes, with for loops! In a Bottle template you do them like this:

{% filename %}views/index.tpl{% endfilename %}
```html
<html>
    <head>
        <title>Bottle Boys blog</title>
    </head>
    <body>
        <div>
            <h1><a href="">Bottle Boys Blog</a></h1>
        </div>
        % for post in posts:
          <div>
            <p>published: {{post["date"]}}</p>
            <h2>{{post["title"]}}</h2>
            <h3>{{post["author"]}}</h3>
            <p>{{post["body"]}}</p>
          </div>
        % end
    </body>
</html>
```

Try this in your template.

Have you noticed that we used a slightly different notation this time (`{{ post["title"] }}` or `{{ post["body"] }})`? We are accessing data in each of the fields defined in our blog model.

Fire up the webserver and see if it worked.  If it did, it should look something like this:

PICTURE HERE

## One more thing

It'd be good to see if your website will still be working on the public Internet, right? Let's try deploying to Heroku again. Here's a recap of the steps…

* First, push your code to Github

{% filename %}command-line{% endfilename %}
```
$ git status
[...]
$ git add --all .
$ git status
[...]
$ git commit -m "Modified templates to display posts from database."
[...]
$ git push
```

* Then, run:

{% filename %}command-line{% endfilename %}
```
$ git push heroku master
[...]
```

* Finally, hop on over to your web app. Your update should be live! If the blog posts on your heroku site don't match the posts appearing on the blog hosted on your local server, that's OK. The databases on your local computer and Heroku don't sync with the rest of your files.  In fact, there is no data on the Heroku version as of yet.
