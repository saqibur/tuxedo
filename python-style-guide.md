# Python Style Guide
This entire "style" guide is based on the following:
* [Styling] PEP-8: [Style Guide for Python Code](https://peps.python.org/pep-0008/)
* [Auto-Formatting] Black: [Black Code Style](https://black.readthedocs.io/en/stable/the_black_code_style/current_style.html)
* [Styling] Google Python Style Guide: [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
* [Linting] Ruff: [Ruff Documentation](https://beta.ruff.rs/docs/)
* [Type-Hinting] MyPy: [MyPy GitHub Repository](https://github.com/python/mypy)
* [Automation] Pre-commit: [A Framework for Managing and Maintaining Multi-language Pre-commit Hooks](https://pre-commit.com/)
* [Rambles] My own personal experiences: [My notes](https://notes.saqibur.com)

ALWAYS remember, readability is the most important thing and no "convention" can
supersede that. Borrowing from PEP-8, we stand by "readabilty over everything"-
https://peps.python.org/pep-0008#a-foolish-consistency-is-the-hobgoblin-of-little-minds


## Yet another style guide?
* Ideally, the plan is to use these tools and configure them accordingly. This
guide also helps you set-up those tools to fit the "style", however when in
doubt, consult the style guide.
* It makes my job easier, and makes working with the people around me easier.


## Terse Summary (sorted by "priority")
At the time of writing, I really wanted to ensure people don't have to spend
three reading sessions to go through the entire style guide. But I also wanted
to ensure that it's comprehensive enough to cover all the bases.


1. Indentation: Always 4 spaces, never 2 (tabs are taboo).
1. Function parameters: If there are too many parameters, break them into new
lines. Never hang arguments
1. Imports: Always explicit, never relative. Sort lexicographically.
1. Spacing Between Functions/Methods and Closures: Group code logically and
separate visually.
1. Spacing Between Functions/Methods and Closures: Group code logically and
separate visually.
1. Line length: Stay below 100, 80 is preferred, 120 if unavoidable

---

### Indentation: *"Always 4 spaces, never 2 (tabs are taboo)."*
* 4 spaces are quite standard across the board, and is the default in most IDEs.
It's also the default in Black, which is what we'll using to format our code.
This has the benefit of making code visually pleasing at the cost of allowing
it to hang towards the right as functions get deeper and longer.

```python
if processing:
    do_something()
```

---

### Function Parameters: *"If there are too many parameters, break them into new lines."*
* Hanging arguments are bad because it makes it harder to read the code, and
sometimes it's not clear what the argument is for. The most aggravating thing
about hanging arguments is that it's not clear where the argument ends, and
where the next argument begins.
* In cases of implied line continuation, you should align wrapped elements either vertically, as per the examples in the line length section; or using a hanging indent of 4 spaces, in which case there should be nothing after the open parenthesis or bracket on the first line.

```python
def calculate_age(
    arg1: int,
    arg2: str,
    arg3: bool,
):
    pass
```

---

### Imports: *"Always absolute, never relative. Sort lexicographically. Break imports with newlines."*
* Absolute imports reduce congnitive load, and make it easier to understand where
the import is coming from. Relative imports are confusing, and can lead to
importing the same module twice.
* Sorting lexographically makes it easier to find imports, and makes it easier
to add new imports. It also makes it easier to find imports that are missing.
* Group and format imports to produce the smallest diffs when adding/updating
imports.
* Use import statements for packages and modules only, not for individual classes
or functions. This goes in line with code-sharing within a module. However, if
you ONLY need a single function from a module, it's better to just import that,
instead of the entire module. Another benefit is avoiding circular imports.
Finally, a benefit is that the namespace of the is consistent that is the source
of each identifier is indicated in a consistent way; `x.Obj` says that object `Obj`
is defined in module `x`.

```python
# Python imports
import os
import time

# Framework imports
from django.db import models
from rest_framework.permissions import (
    BasePermission,
    IsAuthenticated,
)

# 3rd Party Library (non-framework) imports
import requests

# Project-specific imports
from my_module import function
```

Here, imports are grouped together, and when importing multiple things from a
module, we're splitting across new lines thereby producing smaller diffs when
changed somewhere down the line.

Further, multiple imports should be broken into newlines.

---

### Spacing Between Functions/Methods and Closures: *"Group code logically and separate visually."*
* Add three newlines before starting a new class. Add two newlines before starting
a new method or function (unless the function is a closure).
* In terms, of readability this allows you to visually separate method
definitions. In the case of a closure, the function should isolate itself with a
preceding and proceeding newline.
* What this also allows us to do is space out lines within functions as much as we
need wherever readability is required without worrying about space between
independent functions themselves.
* In the rare case that you declare multiple classes in a file, be sure to use 3
newlines.

```python
class FirstClass:
    pass



class SecondClass:
    def first_method(self):
      pass


    def second_method(self):
      pass


    def third_method(self):
      print("Do something")
      def closure():
        pass

      closure()
      pass


def first_function():
  pass


def second_function():
  pass
```

---

### Quotes: *"Always double-quotes"*
* Never mix and match quotes in a codebase. Always use double quotes. If you
need to use a double quote within a string, use single quotes.
* This is a matter of consistency. It's easier to read and understand code when it's consistent. It's also easier to write code when it's consistent. It's also easier to search for code when it's consistent.

```python
print("Hello World")
```

---

### Exceptions: *"Lean, tidy, short and handled"*
* Libraries or packages may define their own exceptions. When doing so they must
inherit from an existing exception class. Exception names should end in Error
and should not introduce repetition (foo.FooError).
* Always treat general `Exceptions` as `exn` and not `e`
* Make use of built-in exception classes when it makes sense.
* Do not use `assert` statements for validating argument values of a public API.
`assert` is used to ensure internal correctness, not to enforce correct usage
nor to indicate that some unexpected event occurred. If an exception is desired
in the latter cases, use a raise statement.
* Minimize the amount of code in a try/except block.

---

### Variables: *"Use descriptive names. Avoid abbreviations. Use the most specific type possible."*
* While they are technically variables, module-level constants are permitted and
encouraged. For example: _MAX_HOLY_HANDGRENADE_COUNT = 3. Constants must be named
using all caps with underscores. See Naming below.
* Avoid global variables.
* If needed, globals should be declared at the module level and made internal to
the module by prepending an _ to the name. External access must be done through
public module-level functions. See Naming below.
* Local variables should have the most restrictive scope possible
* Initialization: Every variable and field should be explicitly initialized (set to an initial value). However, it should never be redundantly initialized to a temporary value that will not be read.
* If a variable is initialized after its declaration but before it is used, it should not be initialized to a temporary value that will never be read.
* Initialization for fields
Fields should also be initialized exactly once. If a field is initialized by the constructor, then its declaration should not initialize it to a temporary value that will never be read.
* If a declaration has an initializer, that should be its initial value.
If a declaration has no initializer, that is a signal to the programmer to look elsewhere for the initial value (and that the initial value differs for different instantiations).

The code is clearer if the initializer is explicit. Do so for all datatypes, including objects whose default value (in the absence of an initializer) is null.

Function names, variable names, and filenames should be descriptive; avoid abbreviation. In particular, do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

Always use a .py filename extension. Never use dashes.

“Internal” means internal to a module, or protected or private within a class.

Prepending a single underscore (_) has some support for protecting module variables and functions (linters will flag protected member access).

Prepending a double underscore (__ aka “dunder”) to an instance variable or method effectively makes the variable or method private to its class (using name mangling); we discourage its use as it impacts readability and testability, and isn’t really private. Prefer a single underscore.

Place related classes and top-level functions together in a module. Unlike Java, there is no need to limit yourself to one class per module.

Use CapWords for class names, but lower_with_under.py for module names. Although there are some old modules named CapWords.py, this is now discouraged because it’s confusing when the module happens to be named after a class. (“wait – did I write import StringIO or from StringIO import StringIO?”)

---

### Line length: *"Maximum line length is 100 characters."*
* Maximum line length is 100 characters. Try to keep it under 80 but if the
situation is unavoidable, go up to 120.

Exceptions are:
* Long import statements.
* URLs, pathnames, or long flags in comments.
* Long string module level constants not containing whitespace that would be
inconvenient to split across lines such as URLs or pathnames.
* Pylint disable comments. (e.g.: # pylint: disable=invalid-name)
* Do not use backslash line continuation except for with statements requiring
three or more context managers.

---

### Parentheses: *"Use parentheses sparingly."*
Use parentheses sparingly.

It is fine, though not required, to use parentheses around tuples. Do not use them in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.

So, try to use parentheses only when it's absolutely necessary.

---

### Trailing commas in sequences: *"Always add trailing commas at the end."*
Trailing commas in sequences of items are recommended only when the closing container token ], ), or } does not appear on the same line as the final element.


---

### Truthy-Falsy: *"Use implicit false"*
The following values in Python are false in the context of if and other logical
contexts:

Python evaluates certain values as False when in a boolean context. A quick “rule of thumb” is that all “empty” values are considered false, so 0, None, [], {}, '' all evaluate as false in a boolean context.

Conditions using Python booleans are easier to read and less error-prone. In most cases, they’re also faster.

That is, always try to use implicit false

False
None
numeric values equal to 0, such as 0, 0.0, -0.0
empty strings: '' and u''
empty containers (such as lists, tuples and dictionaries)
anything that implements __bool__ (in Python3) to return False, or __nonzero__ (in Python2) to return False or 0.
anything that doesn't implement __bool__ (in Python3) or __nonzero__ (in Python2), but does implement __len__ to return a value equal to 0
An object is considered "false" if any of those applies, and "true" otherwise, regardless of whether it's actually equal to or identical with False or True


Never compare a boolean variable to False using ==. Use if not x: instead. If you need to distinguish False from None then chain the expressions, such as if not x and x is not None:.

For sequences (strings, lists, tuples), use the fact that empty sequences are false, so if seq: and if not seq: are preferable to if len(seq): and if not len(seq): respectively.


---

### None checking: *"Always use if foo is None: (or is not None) to check for a None value."*
Always use if foo is None: (or is not None) to check for a None value. E.g., when testing whether a variable or argument that defaults to None was set to some other value. The other value might be a value that’s false in a boolean context!


---


### Order of procedures in code: *"Put public methods before private ones in your files."*
In general, put public methods before private ones in your files. Organize your file with helper methods (whether public or private) after the main entry points. This permits readers to read your code top-down, which is more comprehensible: the purpose of each piece of code, and how it fits into the whole, is obvious. A reader can forward-reference to just the specification, not the whole implementation, of a helper method. This doesn't mean you necessarily have to write your in a code top-down order, but do organize it that way for readers.



---

### Type-hinting: *"Use type-hinting for all your functions."*
Look at mypy's guides
However, for return-statements
If a function "returns" None, just type-hint it to return None
Note that there also exists the typing.NoReturn type for functions that actually never return anything, e.g.

from typing import NoReturn
def raise_err() -> NoReturn:
    raise AssertionError("oops an error")

---

### Decorators: *"Use decorators judiciously when there is a clear advantage."*
Use decorators judiciously when there is a clear advantage. Avoid staticmethod and limit use of classmethod.

Avoid external dependencies in the decorator itself (e.g. don’t rely on files, sockets, database connections, etc.), since they might not be available when the decorator runs (at import time, perhaps from pydoc or other tools). A decorator that is called with valid parameters should (as much as possible) be guaranteed to succeed in all cases.

Never use staticmethod unless forced to in order to integrate with an API defined in an existing library. Write a module-level function instead.

Use classmethod only when writing a named constructor, or a class-specific routine that modifies necessary global state such as a process-wide cache.

---

### Docstrings:
Python uses docstrings to document code. A docstring is a string that is the first statement in a package, module, class or function. These strings can be extracted automatically through the __doc__ member of the object and are used by pydoc. (Try running pydoc on your module to see how it looks.) Always use the three-double-quote """ format for docstrings (per PEP 257). A docstring should be organized as a summary line (one physical line not exceeding 80 characters) terminated by a period, question mark, or exclamation point. When writing more (encouraged), this must be followed by a blank line, followed by the rest of the docstring starting at the same cursor position as the first quote of the first line. There are more formatting guidelines for docstrings below.

Example:
```python
  def fetch_smalltable_rows(
      table_handle: smalltable.Table,
      keys: Sequence[bytes | str],
      require_all_keys: bool = False,
  ) -> Mapping[bytes, tuple[str, ...]]:
      """Fetches rows from a Smalltable.

      Retrieves rows pertaining to the given keys from the Table instance
      represented by table_handle.  String keys will be UTF-8 encoded.

      Args:
          table_handle: An open smalltable.Table instance.
          keys: A sequence of strings representing the key of each table
            row to fetch.  String keys will be UTF-8 encoded.
          require_all_keys: If True only rows with values set for all keys will be
            returned.

      Returns:
          A dict mapping keys to the corresponding table row data
          fetched. Each row is represented as a tuple of strings. For
          example:

          {b'Serak': ('Rigel VII', 'Preparer'),
          b'Zim': ('Irk', 'Invader'),
          b'Lrrr': ('Omicron Persei 8', 'Emperor')}

          Returned keys are always bytes.  If a key from the keys argument is
          missing from the dictionary, then that row was not found in the
          table (and require_all_keys must have been False).

      Raises:
          IOError: An error occurred accessing the smalltable.
      """
```

Classes should have a docstring below the class definition describing the class. If your class has public attributes, they should be documented here in an Attributes section and follow the same formatting as a function’s Args section.


All class docstrings should start with a one-line summary that describes what the class instance represents. This implies that subclasses of Exception should also describe what the exception represents, and not the context in which it might occur. The class docstring should not repeat unnecessary information, such as that the class is a class.


```python
class SampleClass:
    """Summary of class here.

    Longer class information...
    Longer class information...

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam: bool = False):
        """Initializes the instance based on spam preference.

        Args:
          likes_spam: Defines if instance exhibits this preference.
        """
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```
---

### Strings: *"Use f-strings or the format method for formatting strings."*
Use an f-string, the % operator, or the format method for formatting strings, even when the parameters are all strings. Use your best judgment to decide between string formatting options. A single join with + is okay but do not format with +.

Avoid using the + and += operators to accumulate a string within a loop. In some conditions, accumulating a string with addition can lead to quadratic rather than linear running time.

Prefer """ for multi-line strings rather than '''. Projects may choose to use ''' for all non-docstring multi-line strings if and only if they also use ' for regular strings. Docstrings must use """ regardless.

---

### Getters and Setters: *"Use getters and setters only when you need to."*
Getter and setter functions (also called accessors and mutators) should be used when they provide a meaningful role or behavior for getting or setting a variable’s value.

In particular, they should be used when getting or setting the variable is complex or the cost is significant, either currently or in a reasonable future.

If, for example, a pair of getters/setters simply read and write an internal attribute, the internal attribute should be made public instead. By comparison, if setting a variable means some state is invalidated or rebuilt, it should be a setter function. The function invocation hints that a potentially non-trivial operation is occurring. Alternatively, properties may be an option when simple logic is needed, or refactoring to no longer need getters and setters.

Getters and setters should follow the Naming guidelines, such as get_foo() and set_foo().

If the past behavior allowed access through a property, do not bind the new getter/setter functions to the property. Any code still attempting to access the variable by the old method should break visibly so they are made aware of the change in complexity.

---

### Unused variables: *"Unused variables should be named with an underscore"*
If you want to assign a value to a variable that will not be used again, name the variable `_` (python convention). This will keep our lint checkers from
complaining.

```python
def my_function():
    """Demonstrate unused variable."""
    _ = 1
    print("I don't use the variable, but I need to assign it to something.")
```

---

### Line Length: *"Shorter lines, avoid lengthy reads"*
Of course having a hard limit for line length is silly. Any reasonable limit
runs into a case where breaking the rule produces better code. However, having
unnecessarily long lines scattered about due to assumptions about a reader's tools
is also silly.

---

### Classes - *"One class per file. Keeps things lean, tidy and contextual"*
* Use classes to encapsulate related data and functionality.  Keep things lean
and tidy. This is discussed more in the `coding-guide.md`.
* In Python, the implementation of a class needs to be in a single file.
* For the same reason, prefer one class per file.  (You can make
exceptions for classes that are very closely related, or a class that
is used primarily as a member of another class.)
