Style
======

Little Zen for Code Style
----------

Barry Warsaw, one of the core Python developers, once said that it frustrated him that "The Zen of Python" ([PEP 20][pep20]) is used as a style guide for Python code, since it was originally written as a poem about Python's **internal** design. That is, the design of the language and language implementation itself. One can acknowledge that, but a few of the lines from PEP 20 serve as pretty good guidelines for idiomatic Python code, so we'll just go with it.

Beautiful is better than ugly
~~~~~~~~~~~
This one is subjective, but what it usually amounts to is this: will the person who inherits this code from you be impressed or disappointed? What if that person is you, three years later?

Explicit is better than implicit
~~~~~~~~~~~
Sometimes in the name of refactoring out repetition in our code, we also get a little bit abstract with it. It should be possible to translate the code into plain English and basically understand what's going on. There shouldn't be an excessive amount of "magic".

Flat is better than nested
~~~~~~~~~~~

This one is really easy to understand. The best functions have no nesting, neither by loops nor `if` statements. Second best is one level of nesting. Two or more levels of nesting, and you should probably start refactoring to smaller functions.

Also, don't be afraid to refactor a nested if statement into a multi-part boolean conditional.

Readability counts
~~~~~~~~~~~
Don't be afraid to add line-comments with `#`. Don't go overboard on these or over-document, but a little explanation, line-by-line, often helps a whole lot. Don't be afraid to pick a slightly longer name because it's more descriptive. No one wins any points for shortening "`response`" to "`rsp`". Use doctest-style examples to illustrate edge cases in docstrings. Keep it simple!

Errors should never pass silently
~~~~~~~~~~~
The biggest offender here is the bare `except: pass` clause. Never use these. Suppressing **all** exceptions is simply dangerous. Scope your exception handling to single lines of code, and always scope your `except` handler to a specific type. Also, get comfortable with the `logging` module and `log.exception(...)`.

If the implementation is hard to explain, it's a bad idea
~~~~~~~~~~~
This is a general software engineering principle -- but applies very well to Python code. Most Python functions and objects can have an easy-to-explain implementation. If it's hard to explain, it's probably a bad idea. Usually you can make a hard-to-explain function easier-to-explain via "divide and conquer" -- split it into several functions.

Testing is one honking great idea
~~~~~~~~~~~
OK, we took liberty on this one -- in "The Zen of Python", it's actually "namespaces" that's the honking great idea.

But seriously: beautiful code without tests is simply worse than even the ugliest tested code. At least the ugly code can be refactored to be beautiful, but the beautiful code can't be refactored to be verifiably correct, at least not without writing the tests! So, write tests! Please!


Strict Rules
----------
- Each project must have a flake8 linter.
- Each project must follow PEP8 (with 99 chars limit).
- Docstrings must follow PEP257.
- Do not use wildcard imports.
- Don't use single letter variable names, unless within a list comprehension.
- Use Python idioms.
- Avoid redundant labeling.
- Prefer reverse notation.
- Sort and divide import statements.


Usefull tools
-----------------
- https://bitbucket.org/pytest-dev/pytest-pep8
- https://github.com/fschulze/pytest-flakes
- https://github.com/cbrueffer/pep8-git-hook