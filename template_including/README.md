# Template including

Another nice thing Bottle has for you is __template including__. What does this mean? It means that you can use the same parts of your HTML for different pages of your website.

Templates help when you want to use the same information or layout in more than one place.  You don't have to repeat yourself in every file. And if you want to change something, you don't have to do it in every template, just one!

## Create a header template

A header and footer template will let you include a header and a footer on every page of your website.

Let's create a `header.html` and a `footer.html` file in `views`:

```
views
└───index.html
└───header.html
└───footer.html
```

Then open it up and copy everything from `index.html` to `header.html` file, like this:

{% filename %}header.html{% endfilename %}
```html
<html>
    <head>
        <title>Bottle Boys blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
         <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
         <link href="https://fonts.googleapis.com/css?family=Exo+2" rel="stylesheet">
         <link rel="stylesheet" href="/static/blog.css">
    </head>
    <body>
        <div class="page-header">
            <h1><a href="/">Bottle Boys Blog</a></h1>
        </div>
        <div class="content container">
          <div class="row">
              <div class="col-md-8">
                % for post in posts:
                  <div class="post">
                    <p>published: {{post["date"]}}</p>
                    <h2><a href="">{{post["title"]}}</a></h2>
                    <h3>{{post["author"]}}</h3>
                    <p>{{post["body"]}}</p>
                  </div>
                % end
              </div>
          </div>
      </div>
    </body>
</html>
```

Do the same thing with `footer.html`.  You should now have three identical files.  Wait, what?  What's going on?  You're about to see.

Then in `header.html`, delete everything from `<div class="row">` down.  It should end up looking like this:

{% filename %}views/header.html{% endfilename %}
```html
<html>
    <head>
        <title>Bottle Boys blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
         <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
         <link href="https://fonts.googleapis.com/css?family=Exo+2" rel="stylesheet">
         <link rel="stylesheet" href="/static/blog.css">
    </head>
    <body>
        <div class="page-header">
            <h1><a href="/">Bottle Boys Blog</a></h1>
        </div>
```

Next, we'll doctor up the index page.  Notice how much less code it takes to define the way the body of the page will look.  

{% filename %}views/index.html{% endfilename %}
```html
% include("header.html")
        <div class="content container">
          <div class="row">
              <div class="col-md-8">
                % for post in posts:
                  <div class="post">
                    <p>published: {{post["date"]}}</p>
                    <h2><a href="">{{post["title"]}}</a></h2>
                    <h3>{{post["author"]}}</h3>
                    <p>{{post["body"]}}</p>
                  </div>
                % end
              </div>
          </div>
      </div>
% include('footer.html')
```

Last, the lowly footer.  There's hardly any code in this file.

{% filename %}views/footer.html{% endfilename %}
```html
  </body>
</html>
```

That's it! The include functions will piece all the parts of our website together for us.  Now, when we start making new pages, we only have to change the middle part of the page, the body, or the div with class `content container`.  Check if your website is still working properly. :)
