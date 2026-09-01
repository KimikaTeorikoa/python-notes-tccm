# Guide for contributing
This document is aimed to be edited directly by authorized 
contributors only (i.e. those listed as contributors in the
[Github](https://github.com/KimikaTeorikoa/python-notes-tccm/graphs/contributors) page for this book). People not belonging to our 
organization can also contribute, but we kindly ask for those
contributions to be done as 
[pull requests](https://docs.github.com/en/pull-requests).

## General guidelines about jupyterbooks
Before contributing to this book, please read [this
 documentation](https://jupyterbook.org). Specifically,
it is important for you to familiarize yourself with 
the following.

### Configuration
There are two main configuration files in this repository.
The first one is the `_config.yml` file, where you 
will find a number of specifications that the `jupyterbook`
package will be able to process. Find more information
about this configuration file 
[here](https://jupyterbook.org/en/stable/customize/config.html).

### Writing different types of content
When writing a Jupyter Book you can write your content in 
different types of format, mainly markdown files and
jupyter-notebook files. Please go through the specifics of
both of these types of file for generating contents reading
the information [here](https://jupyterbook.org/en/stable/file-types/index.html). 
In general, in the Programming in Python Lecture Notes
Jupyter Book we will use markdown for those files that are
intended to be read-only, while files containing both text
and code will be written as jupyter-notebooks.

### Writing references
In order to introduce references in the text, you should
add the corresponding reference in the text, using
the following format
```
Here is my nifty citation {cite}`perez2011python`.
``` 
 and
the full citation in the `references.bib` file. You 
can find more information about references
 in the Jupyter Book [webpage](Programming in Python Lecture Notes).

### Building the JupyterBook
Once you have made changes locally, it is only natural that you will 
want to take a look at how they look once they are integrated in the
book. First, you may want to take a look locally. You can do this
by running 
```
jupyter-book build python-notes-tccm
```
in the command line.
Deployment online has been taken care of using Github Actions
(specifically, this one 
[here](https://github.com/KimikaTeorikoa/python-notes-tccm/actions/workflows/pages/pages-build-deployment)).
Once you push your changes, they should automatically appear in our
Jupyter Book [webpage](https://kimikateorikoa.github.io/python-notes-tccm) 
shortly.