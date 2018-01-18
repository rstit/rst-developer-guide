Style
======

Rules
----------

- Each project must have a [flake8](https://pypi.python.org/pypi/flake8) linter.
- Each project must follow [PEP8](https://www.python.org/dev/peps/pep-0008/) (inc. 79 chars limit).
- Docstrings must follow PEP257 (https://www.python.org/dev/peps/pep-0257/).
- Functions with more than 1 parameter must [force keyword arguments](https://www.python.org/dev/peps/pep-3102/).
- All class `__init__` methods must [force keyword arguments](https://www.python.org/dev/peps/pep-3102/).
- Follow Python [EAFP principal](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html#eafp-vs-lbyl) where possible.
- Use relative absolute imports within projects, full absolute imports in testing code.
  ```python
  # in testing code
  from project.subpackage import magic_beans
  # in project code
  from .sub_package import magic_beans
  ```
- Don't use single letter variable names, unless within a list comprehension.
- Never put any code in the `__init__.py` of a module (except namespace stitching imports).
- Use Python idioms.
- Avoid redundant labeling.
- Do not use one letter statements.
- Prefer reverse notation.
- Sort and divide import statements.
- Do not comment.

Usefull tools
-----------------
- https://bitbucket.org/pytest-dev/pytest-pep8
- https://github.com/fschulze/pytest-flakes
- https://github.com/cbrueffer/pep8-git-hook