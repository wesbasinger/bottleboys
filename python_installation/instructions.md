> For readers at home: this chapter is covered in the [Installing Python & Code Editor](https://www.youtube.com/watch?v=pVTaqzKZCdA) video.

> This section is based on a tutorial by Geek Girls Carrots (https://github.com/ggcarrots/django-carrots)

Bottle is written in Python. We need Python to do anything with Bottle. Let's start by installing it! We want you to install Python 3.5, so if you have any earlier version, you will need to upgrade it.


<!--sec data-title="Windows" data-id="python_windows" data-collapse=true ces-->

First check whether your computer is running a 32-bit version or a 64-bit version of Windows at https://support.microsoft.com/en-au/kb/827218. You can download Python for Windows from the website https://www.python.org/downloads/windows/. Click on the "Latest Python 3 Release - Python x.x.x" link. If your computer is running a **64-bit** version of Windows, download the **Windows x86-64 executable installer**. Otherwise, download the **Windows x86 executable installer**. After downloading the installer, you should run it (double-click on it) and follow the instructions there.

One thing to watch out for: During the installation you will notice a window marked "Setup". Make sure you tick the "Add Python 3.5 to PATH" checkbox and click on "Install Now", as shown here:

![Don't forget to add Python to the Path](../python_installation/images/python-installation-options.png)

In upcoming steps, you'll be using the Windows Command Line (which we'll also tell you about). For now, if you need to type in some commands, go to Start menu → All Programs → Accessories → Command Prompt. You can also hold in the Windows key and press the "R"-key until the "Run" window pops up. To open the Command Line, type "cmd" and press enter in the "Run" window. (On newer versions of Windows, you might have to search for "Command Prompt" since it's sometimes hidden.)

![Type "cmd" in the "Run" window](../python_installation/images/windows-plus-r.png)

Note: if you are using an older version of Windows (7, Vista, or any older version) and the Python 3.5.x installer fails with an error, you can try either:
1. install all Windows Updates and try to install Python 3.5 again; or
2. install an [older version of Python](https://www.python.org/downloads/windows/), e.g., [3.4.4](https://www.python.org/downloads/release/python-344/).

If you install an older version of Python, the installation screen may look a bit different than shown above. Make sure you scroll down to see "Add python.exe to Path", then click the button on the left and pick "Will be installed on local hard drive":

![Add Python to the Path, older versions](../python_installation/images/add_python_to_windows_path.png)

<!--endsec-->

<!--sec data-title="OS X" data-id="python_OSX"
data-collapse=true ces-->

> **Note** Before you install Python on OS X, you should ensure your Mac settings allow installing packages that aren't from the App Store. Go to System Preferences (it's in the Applications folder), click "Security & Privacy," and then the "General" tab. If your "Allow apps downloaded from:" is set to "Mac App Store," change it to "Mac App Store and identified developers."

You need to go to the website https://www.python.org/downloads/release/python-351/ and download the Python installer:

* Download the *Mac OS X 64-bit/32-bit installer* file,
* Double click *python-3.5.1-macosx10.6.pkg* to run the installer.

<!--endsec-->

Verify the installation was successful by opening the *Terminal* application and running the `python3` command:

```
$ python3 --version
Python 3.5.1
```

**NOTE:** If you're on Windows and you get an error message that `python3` wasn't found, try using `python` (without the `3`) and check if it still might be a version of Python 3.5.

----

If you have any doubts, or if something went wrong and you have no idea what to do next, please ask your coach! Sometimes things don't go smoothly and it's better to ask for help from someone with more experience.
