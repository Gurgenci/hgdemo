# PyPi, GitHub, ReadTheDocs competencies #
After spending one week trying to get ReadTheDocs documentation for `melib` without success, I decided to start from small and start learbibg the ropes the first.  Hence, this project.

In this project, I will start from a simple package with no dependencies.  Once I figure out how to `pypi` and `readthedocs` it, I will gradually make it more and more complex until I reach `melib` complexity.  This file will document the progress.

## One Module, one file : `hgdemo.circle.py` ##
I checked a few 'single module' entries on `GitHub` to find an example to follow.

I picked `requests` as an example because
* It is popular and reputable package
* It has `ReadTheDocs` documentation
* The repository has only one module (like my `melib`)

Structure for the `GitHub` repository `requests`:
* Owner name: psf https://github.com/psf
* Repository name: requests https://github.com/psf/requests 
* Repository structure
  * `.github ` I am not sure what this is for.  My guess is you need it when you have collaboration with multiple coders.
  * `docs` Documentation folder (it looks like the documentation was created using sphinx)
  * `ext` This includes image files presumably all from other sources
  * `requests` This is the folder where you have the module files
    * `__init.py__.py`
    * `__version__.py`
    * `_internal.utils.py`
    * `adapters.py`
    * (and 14 other files with `py` extsnsions)

So let us create a structure for `hgdemo` using the repository `requests` as en example.<br>
$ `mkdir hgdemo`

This folder will be the `hgdemo` module.  All python files will be in this folder.  <br>
$ `cd hgdemo`

Create `circle.py` module with two functions in the module folder (`hgdemo`).  These are `area(r)` and `peri(r)`.  Both functions and the module file itself have docstrings. 

Then create an empty file called `__init__.py` in the same folder as `circle.py` (the inner `hgdemo` folder)

Finally, make a `docs` folder in the root folder.  We can now start following the `sphinx` process to create local dumentation.


### Local Documentation using `sphinx` ###
This is the folder structure at this point:
* `hgdemo`
  * `docs`\ (empty folder)
  * `hgdemo`\
    * `__init__.py`  (empty file)
    * `circle.py` (with two functions: `area` and `peri`)
  * `README.md` (this file)

In VS Code, go to the `docs` folder and enter  
$ `sphinx-quickstart`

Enter the questions as follows:

Separate source and build directories (y/n)[n]: Pick the default ([n])  
Project name: hgdemo  
Author name(s): H Gurgenci  
Project release []: June 2021  
Project language [en]: __  

`sphinx` then ends with the note thatr the following files were created:
```
Creating file H:\My Documents\git\hgdemo\docs\conf.py.
Creating file H:\My Documents\git\hgdemo\docs\index.rst.
Creating file H:\My Documents\git\hgdemo\docs\Makefile.
Creating file H:\My Documents\git\hgdemo\docs\make.bat.
```
This is the folder structure at this point:
* `hgdemo`
  * `docs`\
    * `_build`\
    * `_static`\
    * `_templates`\
    * `conf.py`
    * `index.rst`
    * `make.bat`
    * `Makefile`
  * `hgdemo`\
    * `__init__.py`  (empty file)
    * `circle.py` (with two functions: `area` and `peri`)
  * `README.md` (this file)

#### Edit `conf.py` ####

Path

```
import os
import sys
sys.path.insert(0, os.path.abspath('..'))
```

Extensions (I copied this from the conf file in the requests repository):

```
extensions = [
    "sphinx.ext.autodoc",
    "sphinx.ext.intersphinx",
    "sphinx.ext.todo",
    "sphinx.ext.viewcode",
]
```
#### Edit `index.rst` ####

This is the `index` file after I edit it:
```
.. hgdemo documentation master file, created by sphinx-quickstart on Thu Jun  3 15:18:04 2021.

hgdemo documents python package creation process
================================================

A simple header
===============
The module has two files: circle.py and square.py.
I did go through the process with one file (circle) first and then repeated the process.
A log of my actions can be seen in the file README.md.

   print(hgdemo.circle(2)
   >> 12.56

Guide
^^^^^

.. toctree::
   :maxdepth: 2

   api.rst

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

#### Create `api.rst` ####

I create an `pi.rst` file with the following contents:

```
hgdemo API reference
========================

.. module:: hgdemo

This is a short API file demonstrating the bare essentials.

.. automodule:: hgdemo.circle
    :members:
```
#### Run `./make html` ####
The docs/_build/html/api.html and docs/_build/html/index.html files are generated by sphinx.  All good.

### Remote Documentation ###
* `git init` on `H:\My Documents\git\hgdemo`
* Create `.gitignore` with my standard ignore lines:
  * *.pyc
  * tmp
  * pop
  * .ipynb_checkpoints
* `git add -A`
* `git commit -am `'the first commit'
* log in to github
* Create `hgdemo` as an empty repository
* `git remote add origin` https://github.com/Gurgenci/hgdemo.git
* `git branch -M main`
* `git push origin main`
* Log in to `ReadtheDocs.org`
* Import a repository (hgdemo)

The documentation is created: http://hgdemo.readthedocs.io/ 

### Create a second module, `square`. ###
The second module has two functions: `area`, `side` and it imports `numpy`.
#### Add it to the local `git` ####
* Add the following two lines to the end of `api.rst`:
```  * 
.. automodule:: hgdemo.square
    :members:
```

#### Add it to the github: ####
* `git add -A`
* `git commit -am ` 'the secod module: square'
* `git push origin main`
* Refresh the `Overview` in `ReadtheDocs` project `hgdemo`
* Build Documentation
