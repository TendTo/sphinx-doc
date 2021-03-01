
# sphinx-doc
Fast and absolutely NOT exhaustive "guide" on the steps needed to document a python project with sphinx like a :tent:. In fact, this whole "guide" is meant to remember **me** how to document a python project, since it appears like I have the memory of a chicken

This "guide" assumes that your code is already documented through comments. If not, you can still use this "guide", but you will have to do some work editing those _.rts_ files...

Also, it is always assumed that your current working directory is the root directory of the project

### Let's start with pip3
- pip3 install [sphinx](https://www.sphinx-doc.org/en/master/index.html)
- pip3 install [sphinx_rtd_theme](https://sphinx-rtd-theme.readthedocs.io/en/stable/) \[optional, to use the far superior Read the Docs theme\]

### Edit the .gitignore
- Add the following to the _.gitignore_ to avoid committing useless junk (you could also try adding * for a better result)
``` .gitignore
# Sphinx documentation
.sphinx
```

### Whip out the console
- Run `sphinx-quickstart --sep --ext-autodoc ./docs` This will create the _docs_ directory and its structure

### Don't get lost in _conf.py_
- In _docs/source_ you will find a _conf.py_ file. Edit the following
``` python
# -- Path setup --------------------------------------------------------------

# If extensions (or modules to document with autodoc) are in another directory,
# add these directories to sys.path here. If the directory is relative to the
# documentation root, use os.path.abspath to make it absolute, like shown here.
import os
import sys
sys.path.insert(0, os.path.abspath('../..'))  # path to the actual project root folder
```
``` python
# -- General configuration ---------------------------------------------------

# Add any Sphinx extension module names here, as strings. They can be
# extensions coming with Sphinx (named 'sphinx.ext.*') or your custom
# ones.
extensions = [
    'sphinx.ext.autodoc',   # to autodocument your code
    'sphinx.ext.napoleon',  # to use NumPy and Google style docstrings
    ]
```
``` python
# -- Options for HTML output -------------------------------------------------

# The theme to use for HTML and HTML Help pages.  See the documentation for
# a list of builtin themes.
#
html_theme = 'sphinx_rtd_theme' # [optional, to use the far superior Read the Docs theme]
```

### The show must go on
- **Run** `sphinx-apidoc -o docs/source .` This will try to find all the modules in your project and generate the corresponding _.rts_ file
- Make sure the _docs/source/index.rts_ file links to all the other _.rts_ files you want to include in the documentation
- \[Optional\] Edit the _.rts_ files in the _docs/source_ directory in a way you like. Nobody will judge you (**maybe**)
- **Run** `sphinx-build -b html docs/source docs/build`
- **Run** `docs/make html`. This will generate the final result in _docs/build_. You can see it for yourself by opening _docs/build/html/index.html_ in the browser


### Haven't you used your github page yet?
- Make sure the path _docs/build_ is present in the _.gitignore_
- Rename the _html_ folder to _docs_
- Create a _.nojekyll_ empty file and put it in the _docs_ directory too (because otherwise the github-page isn't happy or something like that)
- \[Optional\] Create a README.md file to explain what are you doing in this branch and you think this was a good idea
- **Run** `git worktree add ./docs/build gh-pages` to add the worktree to the current repository. It is in fact a repository inside the repository
- **Run** `cd ./docs/build && git add -A && git commit -m "docs: added documentation"` to commit the documentation
- Push it to github and, in the settings tab of your repository, make sure the github-page is looking for the _index.html_ file in the right folder
- \[optional\] Add the newly created github-page to the description of your repository
- **?**
- Profit

Now you will have a professional looking documentation page that everyone (mosty you from the future) can consult
