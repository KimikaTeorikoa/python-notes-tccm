# Setting yourself up
Welcome to the course. Before we start with programming as such
it is a good idea to have a working environment that will speed up
your learning. This course will be highly interactive, and students
will be doing a lot of typing. For this, it will be very convenient 
to have a set of user-friendly tools ready to write programs and 
run Python code efficiently. Of course, you are free to choose from 
other alternatives if you prefer, particularly if you already have
some prior experience. Hbere we present a minimal set of tools to work 
with.

Additionally, as we have mentioned already, Python is a particular
programming language in a number of ways. At the end of this Chapter
we will focus in a number of different ways that you can use to 
run Python. But we will cross that bridge when we get there. Let's 
not get ahead of ourselves and start speaking about one of the tools
we will need: the **terminal**.

## The terminal
In order to run Python code and receive its output, we will need 
to interact with a program called the **command line interface** 
or **terminal**. Although there are different types of terminals,
here we will always refer to the 
[Unix shell](https://en.wikipedia.org/wiki/Unix_shell).
If you are not familiar with a few basic commands to navigate
your filesystem, list contents from directories, copy and
transfer files, it is probably a good idea to spend some time
on a Unix shell tutorial. For example, the 
[Shell novice](https://swcarpentry.github.io/shell-novice/)
lesson from [**the Carpentries**](https://carpentries.org/) 
may be a good place to start.

Depending of your operative system, access to the command line 
will differ somewhat. Below, we offer different options depending on
the operative system that runs in the machine that you are using
for the course.

````{tab-set}
```{tab-item} Linux
Regardless of the distribution you are using, your OS will
have a native Unix Shell which is usually 
[Bash](https://www.gnu.org/software/bash/). Typically, it
will either be the Gnome Terminal, the KDE Konsole or xterm.
You can find them in the Applications menu.
```

```{tab-item} Mac OS X
The OS running in Apple computers comes with an application
called Terminal that you can find in the Utilities folder. 
You can open it by searching for Terminal in Spotlight. 
Alternatively, you can install a more customizable terminal
called [iTerm2](https://iterm2.com/). 
You may find that the terminal runs a different
Unix shell, [zsh](https://www.zsh.org/). If you want to use
bash instead, you can change your
shell typing `chsh -s /bin/bash`.
```

```{tab-item} Windows
Windows does not come with a native Unix terminal, but there
are a number of alternatives like the bash terminal that
comes with [Git for Windows](https://gitforwindows.org/).
Alternatively, you can install the [Ubuntu terminal for
Windows](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10).
```
````

## The Anaconda Python distribution 
Your computer may have a native Python installed with the operative
system. However, we strongly recommend that you install the 
[**Anaconda Python distribution**](https://www.anaconda.com/products/distribution), 
which comes with all you are likely to need
in your first encounter with Python. Also, make sure that you 
have **Python 3.x**. 

In parts of the course, we will run Python on a
web interface (e.g. using Jupyter notebooks). For this, you will need 
a browser like Chrome, Safari or Firefox.

## Text editor or IDE
In order to write new programs and modify existing ones,
you will need a text editor or an integrated development
environment 
([IDE](https://en.wikipedia.org/wiki/Integrated_development_environment)). 
While many developers enjoy using traditional text editors like 
[Vim](https://www.vim.org/) or 
[Emacs](https://www.gnu.org/software/emacs/), we would
recommend you to work with something closer to a professional IDE like 
[Pycharm](https://www.jetbrains.com/pycharm/) or Microsoft's 
[Visual Studio Code](https://en.wikipedia.org/wiki/Visual_Studio_Code).
Both have community versions that you can install in your computer
free of charge.

## Running Python
As we have mentioned, Python is particular as a programming language.
As illustrated by an [XKCD](https://xkcd.com/) comic strip that is 
famous within the community, emphasis is put in code readability.

![python-flying](https://imgs.xkcd.com/comics/python.png)

Although we will get into more 
details later in the course, an important thing for you to learn before
we start is that Python programs can be run in different ways.

1. You can use a text editor to write a program in a file, e.g. 
`my_program.py` and run it from the terminal typing
```
$ python my_program.py
```

2. You can open a Python intepreter and run an interactive session
where code is interpreted on-the-fly. A typical, feature-rich
interpreter is called [IPython](https://ipython.org/).

3. Finally, you can use a [Jupyter Notebook](https://jupyter-notebook.readthedocs.io)
or [Jupyter-lab](https://jupyterlab.readthedocs.io/) to run an interactive
Python session in your web browser. In your terminal, type for example,
```
$ jupyter-notebook
```
Normally, you will see some information appearing in your terminal and
a web browser window will pop up. It will look something like this
![jupyter](https://jupyter-notebook.readthedocs.io/en/latest/_images/notebook-running-code.png)
Then, you will be able to run code in *cells*, very much like in 
your IPython session. In fact, an IPython kernel is running in the 
terminal you used. You can save sessions using the `.ipynb` extension.

If you know a more traditional programming language like Fortran, C or 
C++, this may feel surprising.


## Python Documentation

