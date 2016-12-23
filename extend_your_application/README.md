# Extend your application

We've already completed all the different steps necessary for the creation of our website: we know how to write data, routes, views and templates. We also know how to make our website pretty.

Time to practice!

The first thing we need in our blog is, obviously, a page to display one post, right?

## Create a template link to a post's detail

We will start with adding a link inside `views/index.html` file. So far it should look like this:
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

{% raw %}We want to have a link from a post's title in the post list to the post's detail page. Let's change `<h2><a href="">{{post["title"]}}</a></h2>` so that it links to the post's detail page:{% endraw %}

{% filename %}views/index.html{% endfilename %}
```html
<h2><a href="{{"/blog/" + post["postId"]}}">{{post["title"]}}</a></h2>
```

If you fire up your server and check out the page now, you'll have noticed that each of the links now becomes clickable.  And... when you click on the link, you are taken to a very plain and boring page that we created a long time ago, earlier in the tutorial.  Good news, our route still works, now let's go back to `app.py` and dress it up a bit.  Let's just focus on the blog route, everything else can stay the same.  Currently it looks like this:

{% filename %}app.py{% endfilename %}
```python
@route('/blog/<post_number>')
def blog(post_number):
  return "This is blog number " + str(post_number)
```

Let's change it up just a bit.

{% filename %}app.py{% endfilename %}
```python
@route('/blog/<post_number>')
def blog(post_number):
  db = TinyDB('db.json')
  posts = db.table('posts')
  Post = Query()
  blog = posts.get(Post.postId == post_number)
  return template('blog.html', blog=blog)
```

## Create a new template to handle the blog view

Make a new file called `blog.html` in `views`.

{% filename %}views/blog.html{% endfilename %}
```html
% include("header.html")
        <div class="content container">
          <div class="row">
              <div class="col-md-8">
                <h1>{{blog["title"]}}</h1>
                <h2>{{blog["date"]}}</h2>
                <br>
                <p>{{blog["body"]}}</p>
              </div>
          </div>
      </div>
% include('footer.html')
```
Nice!  What a good clean look at each post.  Let's go back to the index route and only give the reader a preview of the blog body, so that they'll be forced to click the link to read on.  *Insert evil laugh.*

{% filename %}views/index.html{% endfilename %}
```html
% include("header.html")
        <div class="content container">
          <div class="row">
              <div class="col-md-8">
                % for post in posts:
                  <div class="post">
                    <p>published: {{post["date"]}}</p>
                    <h2><a href="{{"/blog/" + post["postId"]}}">{{post["title"]}}</a></h2>
                    <h3>{{post["author"]}}</h3>
                    <p>{{post["body"][0:20] + ' ...'}}</p>
                  </div>
                % end
              </div>
          </div>
      </div>
% include('footer.html')
```

Go ahead, check out your site and see if it's still working.  It should be!

## One more thing: deploy time!

It'd be good to see if your website will still be working on Heroku, right? Let's try deploying again.

{% filename %}command-line{% endfilename %}
```
$ git status
$ git add --all .
$ git status
$ git commit -m "Added view and template for detailed blog post as well as CSS for the site."
$ git push
```

Then, in a console:

{% filename %}command-line{% endfilename %}
```
$ git push heroku master
[...]
```

And that should be it! Congrats :)
