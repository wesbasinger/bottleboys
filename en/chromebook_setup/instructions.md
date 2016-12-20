You can [skip right over this section](http://tutorial.djangogirls.org/en/installation/#install-python) if you're not using a Chromebook. If you
are, your installation experience will be a little different. You can ignore the
rest of the installation instructions.

### CodeAnywhere 

CodeAnywhere is a tool that gives you a code editor and access to a computer running
on the Internet where you can install, write, and run software. For the duration
of the tutorial, CodeAnywhere will act as your _local machine_. You'll still be
running commands in a terminal interface just like your classmates on OS X,
Ubuntu, or Windows, but your terminal will be connected to a computer running
somewhere else that CodeAnywhere sets up for you.

1. Go to [codeanywhere.com](https://codeanywhere.com)
2. Use your Google account to sign in
3. Create a Python3 container running on Ubuntu 14.04.
4. Name it whatever you like.

Now you should see an interface with a sidebar, a big main window with some
text.

If you right click on your container on the left hand pane, you can open a SSH connection to your instance.  You should be able to see a command prompt like this:

`cabox@box-codeanywhere:~/workspace$`

The large black area is your _terminal_, where you will give the computer CodeAnywhere
has prepared for you instructions.

### Virtual Environment

A virtual environment (also called a virtualenv) is like a private box we can
stuff useful computer code into for a project we're working on. We use them to
keep the various bits of code we want for our various projects separate so
things don't get mixed up between projects.

Run this code.

```
mkdir djangoguy
cd djangoguy
python3.5 -mvenv myvenv
source myvenv/bin/activate
pip install django~=1.10.0
```

(note that on the last line we use a tilde followed by an equal sign: ~=).

### Github

Make a [Github](https://github.com) account.

### PythonAnywhere

This tutorial includes a section on what is called Deployment,
which is the process of taking the code that powers your new web application
and moving it to a publicly accessible computer (called a server) so other
people can see your work.

This part is a little odd when doing the tutorial on a Chromebook since we're
already using a computer that is on the Internet (as opposed to, say, a laptop).
However, it's still useful, as we can think of our CodeAnywhere workspace as a place
or our "in progress" work and Python Anywhere as a place to show off our stuff
as it becomes more complete.

Thus, sign up for a new Python Anywhere account at
[www.pythonanywhere.com](https://www.pythonanywhere.com).
