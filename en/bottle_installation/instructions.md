## Virtual environment

*Remember, if you're using a Chromebook, you already did this step.*

Before we install Bottle we will get you to install an extremely useful tool to help keep your coding environment tidy on your computer. It's possible to skip this step, but it's highly recommended. Starting with the best possible setup will save you a lot of trouble in the future!

So, let's create a **virtual environment** (also called a *virtualenv*). Virtualenv will isolate your Python/Django setup on a per-project basis. This means that any changes you make to one website won't affect any others you're also developing. Neat, right?

All you need to do is find a directory in which you want to create the `virtualenv`; your home directory, for example. On Windows it might look like `C:\Users\Name\` (where `Name` is the name of your login).

> __NOTE:__ On Windows, make sure that this directory does not contain accented or special characters; if your username contains accented characters, use a different directory, for example `C:\bottleboys`.

For this tutorial we will be using a new directory `bottleboys` from your home directory:

```
$ mkdir bottleboys 
$ cd bottleboys
```

We will make a virtualenv called `myvenv`. The general command will be in the format:

```
$ python3 -m venv myvenv
```

<!--sec data-title="Windows" data-id="virtualenv_installation_windows"
data-collapse=true ces-->

To create a new `virtualenv`, you need to open the console (we told you about that a few chapters ago – remember?) and run `C:\Python35\python -m venv myvenv`. It will look like this:

```
C:\Users\Name\bottleboys> C:\Python35\python -m venv myvenv
```

where `C:\Python35\python` is the directory in which you previously installed Python and `myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces, accents or special characters. It is also good idea to keep the name short – you'll be referencing it a lot!

<!--endsec-->

<!--sec data-title="Linux and OS X" data-id="virtualenv_installation_linuxosx"
data-collapse=true ces-->

Creating a `virtualenv` on both Linux and OS X is as simple as running `python3 -m venv myvenv`.
It will look like this:

```
$ python3 -m venv myvenv
```

`myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces. It is also good idea to keep the name short as you'll be referencing it a lot!

> __NOTE:__ On some versions of Debian/Ubuntu you may receive the following error:

>```
>The virtual environment was not created successfully because ensurepip is not available.  On Debian/Ubuntu systems, you need to install the python3-venv package using the following command.
>    apt-get install python3-venv
>You may need to use sudo with that command.  After installing the python3-venv package, recreate your virtual environment.
>```
>
> In this case, follow the instructions above and install the `python3-venv` package:
>```
>$ sudo apt-get install python3-venv
>```

> __NOTE:__ On some versions of Debian/Ubuntu initiating the virtual environment like this currently gives the following error:

>```
>Error: Command '['/home/eddie/Slask/tmp/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1
>```

> To get around this, use the `virtualenv` command instead.

>```
>$ sudo apt-get install python-virtualenv
>$ virtualenv --python=python3.5 myvenv
>```

> __NOTE:__ If you get an error like

>```
>E: Unable to locate package python3-venv
>```

> then instead run:
>
>```
>sudo apt install python3.5-venv
>```

<!--endsec-->

## Working with virtualenv

The command above will create a directory called `myvenv` (or whatever name you chose) that contains our virtual environment (basically a bunch of directory and files).

<!--sec data-title="Windows" data-id="virtualenv_windows"
data-collapse=true ces-->

Start your virtual environment by running:

```
C:\Users\Name\bottleboys> myvenv\Scripts\activate
```

> __NOTE:__ on Windows 10 you might get an error in the Windows PowerShell that says `execution of scripts is disabled on this system`. In this case, open another Windows PowerShell with the "Run as Administrator" option.  Then try typing the following command before starting your virtual environment:
>
>```
>C:\WINDOWS\system32> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
>     Execution Policy Change
>     The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose you to the security risks described in the about_Execution_Policies help topic at http://go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy? [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
>```

<!--endsec-->

<!--sec data-title="Linux and OS X" data-id="virtualenv_linuxosx"
data-collapse=true ces-->

Start your virtual environment by running:

```
$ source myvenv/bin/activate
```

Remember to replace `myvenv` with your chosen `virtualenv` name!

> __NOTE:__ sometimes `source` might not be available. In those cases try doing this instead:
>
>```
>$ . myvenv/bin/activate
>```

<!--endsec-->

You will know that you have `virtualenv` started when you see that the prompt in your console is prefixed with `(myvenv)`.

When working within a virtual environment, `python` will automatically refer to the correct version so you can use `python` instead of `python3`.

OK, we have all important dependencies in place. We can finally install Django!

## Installing Bottle 

Now that you have your `virtualenv` started, you can install Bottle.

Before we do that, we should make sure we have the latest version of `pip`, the software that we use to install Bottle:

```
(myvenv) ~$ pip install --upgrade pip
```

Then run `pip install bottle` to install Bottle.

That's it! You're now (finally) ready to create a Bottle application!
