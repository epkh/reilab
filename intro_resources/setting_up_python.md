# Setting Up Python

Here we will walk through some of the basics of setting up your Python environment, including installing Python, setting up Hydrogen in Atom, and installing Anaconda and setting up a virtual environment.

###### Note
This is very closely drawn (and sometimes directly taken) from the MIT Big Data, Visualization, and Society class' Python Setup [linked here](https://github.com/ericmhuntley/big-data-spring2018/blob/master/week-01/WS01d_Python-Setup.md) and [here](https://github.com/civic-data-design-lab/big-data-spring2017/blob/master/week1/Part2_Anaconda_Setup.ipynb).

## What is Python?

Python was created in 1989 by Guido van Rossum. For more info, see [here](https://docs.python.org/3/faq/general.html#why-was-python-created-in-the-first-place).
The [Python documentation](https://docs.python.org/3/faq/general.html#what-is-python) describe Python as:
>...An interpreted, interactive, object-oriented programming language. It incorporates modules, exceptions, dynamic typing, very high level dynamic data types, and classes. Python combines remarkable power with very clear syntax. It has interfaces to many system calls and libraries, as well as to various window systems, and is extensible in C or C++. It is also usable as an extension language for applications that need a programmable interface. Finally, Python is portable: it runs on many Unix variants, on the Mac, and on Windows 2000 and later.

Where does the name come from? According to [A Byte of Python](https://python.swaroopch.com/about_python.html) (a useful resource on getting started with Python):
>Guido van Rossum, the creator of the Python language, named the language after the BBC show "Monty Python's Flying Circus". He doesn't particularly like snakes that kill animals for food by winding their long bodies around them and crushing them.

Basically, Python is a **really** valuable scripting language for data cleaning, analysis, and...almost anything. [Python](https://www.python.org/) is a very, very popular high-level programming language. It emphasizes legibility over highly complex structure. Python provides simple data structures that allow for easy data manipulation. Python's simplicity and legibility has led to a large and devoted user community who have created numerous libraries that vastly extend the basic capacities of the language. See [here](https://pypi.org/) for a searchable index of Python's libraries in the Python Package Index.

Python is an "interpreted" language. This means that every Python command that is executed is actually translated to lower-level programming languages. Lower-level, compiled programming languages (for example, C++) are very fast and powerful, but writing programs in these languages can be difficult.

There are two main versions of Python (Python 2 and Python 3). Python 3 is newer, and removed bugs and idiosyncrasies of Python 2; however Python 2 is still heavily used. While the fundamentals of the two versions are the same, there are some differences (mostly syntactical) between the two. These differences are substantial enough that, unfortunately, Python 3 is NOT backwards compatible, so always double check which version of Python a given script is written in. It should be documented, but if it isn't, you can consult a [Python 2 vs. Python 3 cheatsheet](http://python-future.org/compatible_idioms.html) to scan the script for some tell-tale signs of either (print commands tend to be an easy way of doing this).

There are a number of great Python tutorials available on the web, some can be found here:

+ [Python Docs Tutorials](https://docs.python.org/3/tutorial/)
+ [Python Docs Guide to Tutorials](http://docs.python-guide.org/en/latest/intro/learning/)
+ [Learn Python the Hard Way](https://learncodethehardway.org/python/)
+ [Learn More Python the Hard Way](https://learncodethehardway.org/more-python/)

There are also some excellent Python textbooks and cookbooks, including the following:

+ Guttag, John. *Introduction to Computation and Programming Using Python*. Cambridge: MIT Press, 2017.
+ McKinney, Wes. 2017. *Python for Data Analysis*. 2nd ed. Boston: O’Reilly Media.


## Installing Python

### Checking for Installed Versions
First, check whether you have Python installed. Open the Terminal or Windows Command Prompt and type the following command:

```sh
python --version
```
You should see something like `Python 3.6.3`. If a Python 2.x.x version shows up, type `python3 -V`. If the console prints a Python `3.6.x` version, you're set. Otherwise, you'll need to install Python 3.

### Installing Python 3.6.x

Navigate to the [3.6.3 release page](https://www.python.org/downloads/release/python-363/) and select the appropriate installer for your operating system.

+ On OS X, this is [Mac OS X 64-bit/32-bit installer](https://www.python.org/downloads/release/python-360/).
+ On Windows, this is [Windows x86-64 executable installer](https://www.python.org/downloads/release/python-360/).

Install Python. **On Windows, you should ensure that "Add Python 3.6 to PATH" is checked.** Close any open Terminal or Command Prompt windows and reopen the application. Now type `python -V`. This may still cause a Python 2.x.x version to appear; if this is the case, type `python3 -V`. We now have Python 3 and can execute it from the command line!

**Note**: If you ran Python 3 using the `python3` command, you'll use this in every instance below where you're instructed to type `python`.

### A Note on Python Versions

You may wonder why you'd want to maintain two versions of the same language on my operating system. Ordinarily, this would be only a source of confusion. But the development team made unusually significant changes to the way the language thinks and operates between Python 2.7 and Python 3.x---. These were so significant, in fact, that Python 3 sacrificed **backwards-compatibility**. In other words, scripts written in Python 2.x will often not run correctly in Python 3.x.

Imagine you've built up a substantial collection of scripts in Python 2 that you'd still like to be able to execute. You'll need to have Python 2.7.x on hand if you want to run older scripts! Nowadays, most scripts you find on GitHub and elsewhere are going to be updated for Python 3 or written in Python 3, but in case they aren't, having Python 2 will allow for more compatibility.

### Test that Python works by Running a Script from the Command Line

In the subfolder, scripts, you should see a file called `first-script.py`. `.py` is the standard file extension. Now that we've installed Python, test it by running the script from the command line.

```sh
$ cd /path/to/repo/reilab/intro_resources/scripts/
$ python first-script.py
Python is printing me!
```
Open the script to see what's included in the .py file itself.


## Installing Hydrogen

While some coders like to run all of their scripts from the command line, it is much easier (and often very useful) to run chunks of our Python scripts rather than the scripts in their entirety. This is why many (maybe most?) use Jupyter Notebooks to code in Python. However, we will do this using an Atom package called Hydrogen that will let us execute and display the output of our Python and JavaScript code [(and other code, like R, Julia, and more)](https://blog.nteract.io/hydrogen-interactive-computing-in-atom-89d291bcc4dd) from within Atom.

To install Hydrogen, open Atom, and open your preferences. Select 'Install' search for Hydrogen. Click the 'Install' button. After a brief interlude, Hydrogen should be installed! Check that 'Hydrogen' appears under the Packages drop-down menu. If not, try restarting Atom and checking again.


## Setting up a Virtual Environment
Before we start using Python, we're going to install a platform that will allow us to create virtual environments where we can manage our libraries for different projects.

Python is a valuable scripting language for data analysis and management (and more!); however managing a Python project environment can be nuanced and tricky. Anaconda is a platform built to complement Python by creating customizable and easily accessible environments in which you can run Python scripts. For more info on Anaconda, check out the [Anaconda homepage](https://www.continuum.io/why-anaconda).

***Note: you may prefer to use `virtualenv` instead of Anaconda. If you prefer to use that, there are brief instructions on how to do that below the Anaconda instructions.***

### Why Use a Virtual Environment?

Projects have what are called dependencies. These are packages that given scripts require to run successfully. By using a virtual environment, we can carefully tailor Python and package versions for each project or use without worrying about or scuttling other projects' dependencies.  

Anaconda is basically creating specific environments on your machine in which you can specify the packages that are installed and used, and easily lets you toggle between environments. Within the individual environments, you can perform analysis, run scripts, and develop code.

Environments are the bread and butter of Anaconda, because not all Python scripts you run will use the same packages, so you can customize exactly what you need, and create a sandbox that lets you try new things. Your environments will save the packages you have installed, allowing you to easily load an environment and run your scripts. For example, you might want a virtual environment for projects that involve geospatial data cleaning and analysis, and others for projects that involve regressions and data science. Or you might want a virtual environment for projects related to the Lab and another one for personal projects. Either way, keeping your libraries organized will help keep your workflow (and brain!) organized.

#### [Python Environment](https://xkcd.com/1987/)
![](https://imgs.xkcd.com/comics/python_environment.png "Python Environment")


### Installing Anaconda
The first step is to open Terminal and check to see if you already have Anaconda installed.

The syntax to access Anaconda on the command line is simply ‘conda’. To check the version you have installed, use the following:
```sh
conda info
```

If you have it installed, you will see platform information, version details, and environment paths after you hit enter, if not, the terminal will not recognize the command.

To install ‘Conda’, navigate to the Anaconda downloads page [here](https://www.anaconda.com/download/#macos).

Here, pick your system (Mac/Windows) and the Python version. In our case, we are going to select Python version 3.6. Use the ***graphical installer***, it will provide us a wizard that will step us through the installation process. Download the installer, double click the package file and follow the instructions. Heads up: the installation process takes 5-10 minutes since Conda is a big program.

If you run into problems installing, or you get an error that states that Anaconda cannot be installed in the default location, visit [this page](https://docs.anaconda.com/anaconda/install/) for short instructions on how to troubleshoot installation.

Anaconda is contained in one directory, so if you ever need to uninstall Anaconda, use your command line to remove the entire Anaconda directory using:
```sh
rm -rf ~/anaconda.
```

***Another note on why we chose Python 3 instead of Python 2:*** The guidelines on the site describe that we should use whichever version we intend to use most often, but ultimately it will not matter that much. Anaconda supports both Python 2 and 3, and if you ever want to use Python 2, you can create an environment that uses Python 2 and activate it.

Once we are finished with the installation, check to make sure it installed correctly by performing a version check.
```sh
conda info
```

If you see a 5.X.X version number popup, and with platform and environment information, the installation worked!

### Taking Conda for a Test Drive

To take advantage of Conda and the organizational benefits of a virtual environment, make sure that each time you start using Python, you activate your virtual environment. How to do this (and more!) is easily laid out in a tutorial created by the Anaconda team. This test drive is designed to take about 30 minutes to introduce you to concepts around Anaconda, including setting up an environment, toggling between environments, managing the Python version you are using, managing the Python packages you are using in your environments, and finally, removing or uninstall packages and environments if you no longer need them.

These tutorials are [here](https://conda.io/docs/user-guide/getting-started.html) and [here](https://docs.anaconda.com/anaconda/navigator/getting-started) depending on whether you want to use Conda in the command line or in the navigator app, or both!

Working with Anaconda can make working with Python a much more pleasant experience. For additional resources, including cheatsheets and useful links, check out the Anaconda website or see these cheat sheets.

[Anaconda Starter Guide](https://docs.anaconda.com/_downloads/Anaconda-Starter-Guide-Cheat-Sheet.pdf)

[Anaconda Cheat Sheet](https://conda.io/docs/_downloads/conda-cheatsheet.pdf)


## Install the `ipython` kernel

We installed Hydrogen above, which will allow you to run Python scripts from within Atom. However, if you try to do this now, you may get an error that you need to install a **kernel**. Basically, a kernel is a program that runs your code. One very common kernel is `ipython`, which should already be installed in your Anaconda virtual environments, but if it isn't, let's make sure we install or update it.

Before doing so, make sure you're in your virtual environment by typing `source activate ENVIRONMENT NAME` (if you're on a Mac) or `activate ENVIRONMENT NAME` (if you're on Windows). Then, try `conda install ipython` or `conda update ipython`. Now that we're working within a virtual environment, any packages you install will be installed in the virtual environment, rather than in your global Python packages.


### Running Atom from within a virtual environment

Once you've activated your virtual environment (make sure you see your environment name before the prompt in your command line), you can run Atom, and therefore Hydrogen, from within this environment. To do so, you must start Atom from the command line using the following command:

```sh
atom ./
```

## Run a script from within Atom

Open the the `first-script.py` script in Atom. Select the first line and type shift-enter. You'll see a checkmark appear next to the line and your cursor will have progressed to the next line. The checkmark tells you that the line executed successfully. In this case, that means a variable called `msg` is now stored in memory. Type shift-enter again. You should see "Python is printing me!" appear next to the print function. This is how Hydrogen displays console output. We can now run not only full scripts, but 'chunks' of code. This will allow us significantly more flexibility as we develop our own scripts.












[UPDATE TO REFLECT NON BDVS AND JUST BE A BASIC TUTORIAL ON VIRTUALENV]

### An Alternative to Anaconda

An alternative way to manage your virtual environments uses the `virtualenv` package for Python (which you can install using the `pip` package manager).

#### Installing `virtualenv` using `pip`

Install the virtual environment library using `pip`. `pip` is a package management system that allows you to easily install and maintain python libraries using a simple command line interface. If you're on a Mac with a Python distribution, you'll probably be able to run `pip` or `pip3` from your command line with no problems. On Windows, it's a bit trickier (as usual) and so Anaconda might be the choice for you.

#### Installing `pip` on Windows

Go to [the pip webpage](https://pip.pypa.io/en/stable/installing/#installing-with-get-pip-py) and download `get-pip.py`. Change your directory to the location to which you downloaded the `get-pip` script, and execute the following command:

```sh
python get-pip.py
```

This will install `pip` on your system. Close your command line windows and reopen them. You should then be able to execute pip; type `pip -V` to see which version you have installed. Much like with Python, if you have installations of both Python 2 and Python 3 on the same machine, you'll have to use the `pip3` command to install Python 3 packages.

### Install

We installed Hydrogen above, which will allow you to run Python scripts from within Atom. However, if you try to do this now, you're likely to be in trouble; we have yet to install a **kernel**. Basically, a kernel is a program that runs your code. One very common kernel is `ipython`, which we can install using `pip` in the same way that we installed `virtualenv` above. The only difference is that we're now working within a virtual environment, meaning that any packages you install will be installed in the virtual environment, rather than in your global Python packages.

```sh
# Remember that you may need to use pip3
pip install ipython
```

### Install `virtualenv`

Now we're going to install `virtualenv` using `pip`.

```sh
# if you have only Python 3.x installed
pip install virtualenv
# If you have both Python 2.x and Python 3.x installed
pip3 install virtualenv
```

Wow! That was easy. And that, my friends, is why we use package managers.

### Creating a New Virtual Environment

Once we've installed `virtualenv`, we can create a new virtual environment using only a few commands.

```sh
mkdir ~/.venvs
virtualenv --system-site-packages ~/.venvs/bdvs

# On Mac or Linux...
. ~/.venvs/bdvs/bin/activate
# On Windows...
. ~/.venvs/bdvs/Scripts/activate
```

First we create a new folder to hold our virtual environments. Next, we create a new virtual environment in the `bdvs` subfolder of our new `.venvs` subdirectory. We're also telling `virtualenv` that we want this environment to inherit its packages from the Python system installation (this is the role of the `--system-site packages` option). Finally, we activate the virtual environment using the `.` operator, which tells the shell to source from a provided path.

Cool! You're now running Python in a virtual environment! You should see (bdvs) before the prompt in Terminal or Git Bash.
