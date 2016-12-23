# CSS – make it pretty!

Our blog still looks pretty ugly, right? Time to make it nice! We will use CSS for that.

## What is CSS?

Cascading Style Sheets (CSS) is a language used for describing the look and formatting of a website written in a markup language (like HTML). Treat it as make-up for our web page. ;)

But we don't want to start from scratch again, right? Once more, we'll use something that programmers released on the Internet for free. Reinventing the wheel is no fun, you know.

## Let's use Bootstrap!

Bootstrap is one of the most popular HTML and CSS frameworks for developing beautiful websites: https://getbootstrap.com/

It was written by programmers who worked for Twitter. Now it's developed by volunteers from all over the world!

## Install Bootstrap

To install Bootstrap, you need to add this to your `<head>` in your `.html` file:

{% filename %}views/index.html{% endfilename %}
```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
```

This doesn't add any files to your project. It just points to files that exist on the Internet. Just go ahead, open your website and refresh the page. Here it is!

![Figure 14.1](images/bootstrap1.png)

Looking nicer already!


## Static files in Bottle

Finally we will take a closer look at these things we've been calling __static files__. Static files are all your CSS and images. Their content doesn't depend on the request context and will be the same for every user.


### Where to put static files for Bottle

Basically, we need to set up a special folder to serve static files from.

We do that by creating a folder called `static` inside the blog app:

```
bottleboys
└───/views
└───app.py
└───Procfile
└───db.json
└───/myvenv
└───requirements.txt
└───/static
```

We need to make another route in `app.py` to serve files from the `static` directory.

{% filename %}app.py{% endfilename %}
```python
from sys import argv
from bottle import route, run, template, static_file # This line is new!!!
from tinydb import TinyDB
import os # This line is new!!!

@route('/')
def index():
  db = TinyDB("db.json")
  posts = db.table("posts")
  return template('index.html', posts=list(posts.all()))

@route('/about')
def about():
  return "This is the about me route."

@route('/blog/<post_number>')
def blog(post_number):
  return "This is blog number " + str(post_number)

################################
#  This route is new           #
################################
@route('/static/<filename>')
def server_static(filename):
    cwd = os.getcwd()
    return static_file(filename, root=cwd + '/static')


run(host="0.0.0.0", port=argv[1], debug=True)
```

## Your first CSS file!

Let's create a CSS file now, to add your own style to your web page. Create a new directory called `css` inside your `static` directory. Then create a new file called `blog.css` inside this `css` directory. Ready?

```
bottleboys
└───/views
└───app.py
└───Procfile
└───db.json
└───/myvenv
└───requirements.txt
└───/static
      └─── blog.css

```

Time to write some CSS! Open up the `static/blog.css` file in your code editor.

We won't be going too deep into customizing and learning about CSS here. It's pretty easy and you can learn it on your own after this workshop. There is a recommendation for a free course to learn more at the end of this page.

But let's do at least a little. Maybe we could change the color of our header?
To understand colors, computers use special codes. These codes start with `#` followed by 6 letters (A–F) and numbers (0–9). For example, the code for blue is `#0000FF`. You can find the color codes for many colors here: http://www.colorpicker.com/. You may also use [predefined colors](http://www.w3schools.com/colors/colors_names.asp), such as `red` and `green`.

In your `static/blog.css` file you should add the following code:

{% filename %}static/blog.css{% endfilename %}
```css
h1 a {
    border: solid;
    border-style: groove;
    border-width: 4px;
    padding: 4px
}
```

`h1 a` is a CSS Selector. This means we're applying our styles to any `a` element inside of an `h1` element. So when we have something like `<h1><a href="">link</a></h1>`, the `h1 a` style will apply. In this case, we're telling it to change its color to `#FCA205`, which is orange. Of course, you can put your own color here!

In a CSS file we determine styles for elements in the HTML file. The first way we identify elements is with the element name. You might remember these as tags from the HTML section. Things like `a`, `h1`, and `body` are all examples of element names.
We also identify elements by the attribute `class` or the attribute `id`. Class and id are names you give the element by yourself. Classes define groups of elements, and ids point to specific elements. For example, you could identify the following tag by using the tag name `a`, the class `external_link`, or the id `link_to_wiki_page`:

```html
<a href="https://en.wikipedia.org/wiki/Bottle_(web_framework)" class="external_link" id="link_to_wiki_page">
```

You can read more about [CSS Selectors at w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

Between the `<head>` and `</head>` tags, after the links to the Bootstrap CSS files, add this line to `index.html`:

{% filename %}views/index.html{% endfilename %}
```html
<link rel="stylesheet" href="/static/blog.css">
```
The browser reads the files in the order they're given, so we need to make sure this is in the right place. Otherwise the code in our file may override code in Bootstrap files.
We just told our template where our CSS file is located.

Your file should now look like this:

{% filename %}views/index.html{% endfilename %}
```html
<html>
    <head>
        <title>Bottle Boys blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link rel="stylesheet" href="/static/blog.css">
    </head>
    <body>
        <div>
            <h1><a href="/">Bottle Boys blog</a></h1>
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

OK, save the file and refresh the site!

![Border]('images/border.png')


Nice work! Maybe we would also like to give our website a little air and increase the margin on the left side? Let's try this!  Add another selector in your css file.

{% filename %}blog/static/css/blog.css{% endfilename %}
```css
body {
    padding-left: 15px;
}
```

Add that to your CSS, save the file and see how it works!

![Padding](images/padding.png)

Maybe we can customize the font in our header? Paste this into your `<head>` in `views/index.html` file:

{% filename %}views/index.html{% endfilename %}
```html
<link href="https://fonts.googleapis.com/css?family=Exo+2" rel="stylesheet">
```

As before, check the order and place before the link to `static/blog.css`. This line will import a font called *Exo 2* from Google Fonts (https://www.google.com/fonts).

Find the `h1 a` declaration block (the code between braces `{` and `}`) in the CSS file `views/blog.css`.  Now add the line `font-family: 'Exo 2';` between the braces, and refresh the page:

{% filename %}views/blog.css{% endfilename %}
```css
h1 a {
    border: solid;
    border-style: groove;
    border-width: 4px;
    padding: 4px;
    font-family: 'Exo 2';
}
```

![Figure 14.3](images/font.png)

The heading has disappeared for now, but it will be back when we turn the background color to blue.

As mentioned above, CSS has a concept of classes. These allow you to name a part of the HTML code and apply styles only to this part, without affecting other parts. This can be super helpful! Maybe you have two divs that are doing something different (like your header and your post).  A class can help you make them look different.

Go ahead and name some parts of the HTML code. Add a class called `page-header` to your `div` that contains your header, like this:

{% filename %}views/index.html{% endfilename %}
```html
<div class="page-header">
    <h1><a href="/">Bottle Boys Blog</a></h1>
</div>
```

And now add a class `post` to your `div` containing a blog post.

{% filename %}views/index.html{% endfilename %}
```html
<div class="post">
  <p>published: {{post["date"]}}</p>
  <h2><a href="">{{post["title"]}}</a></h2>
  <h3>{{post["author"]}}</h3>
  <p>{{post["body"]}}</p>
</div>
```

We will now add declaration blocks to different selectors. Selectors starting with `.` relate to classes. There are many great tutorials and explanations about CSS on the Web that can help you understand the following code. For now, just copy and paste it into your `static/blog.css` file:

{% filename %}static/blog.css{% endfilename %}
```css
.page-header {
    background-color: #4286f4;
    margin-top: 0;
    padding: 20px 20px 20px 40px;
}

.page-header h1, .page-header h1 a, .page-header h1 a:visited, .page-header h1 a:active {
    color: #ffffff;
    font-size: 36pt;
    text-decoration: none;
}

.content {
    margin-left: 40px;
}

h1, h2, h3, h4 {
    font-family: 'Exo 2', sans-serif;
}

.date {
    color: #828282;
}

.save {
    float: right;
}

.post-form textarea, .post-form input {
    width: 100%;
}

.top-menu, .top-menu:hover, .top-menu:visited {
    color: #ffffff;
    float: right;
    font-size: 26pt;
    margin-right: 20px;
}

.post {
    margin-bottom: 70px;
}

.post h1 a, .post h1 a:visited {
    color: #000000;
}
```

Then surround the HTML code which displays the posts with declarations of classes. Replace this:

{% filename %}views/index.html{% endfilename %}
```html
% for post in posts:
  <div class="post">
    <p>published: {{post["date"]}}</p>
    <h2><a href="">{{post["title"]}}</a></h2>
    <h3>{{post["author"]}}</h3>
    <p>{{post["body"]}}</p>
  </div>
% end
```

in the `view/index.html` with this:

{% filename %}views/index.html{% endfilename %}
```html
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
```

Save those files and refresh your website.

![Figure 14.4](images/final.png)

Woohoo! Looks awesome, right?
Look at the code we just pasted to find the places where we added classes in the HTML and used them in the CSS. Where would you make the change if you wanted the date to be turquoise?

Don't be afraid to tinker with this CSS a little bit and try to change some things. Playing with the CSS can help you understand what the different things are doing. If you break something, don't worry – you can always undo it!

We really recommend taking this free online [Codeacademy HTML & CSS course](https://www.codecademy.com/tracks/web). It can help you learn all about making your websites prettier with CSS.

Ready for the next chapter?! :)
