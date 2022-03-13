# Python Style Guide

## Imports

### Proposal
When writing imports, be sure to group related ones, sort lexicographically and
format to produce the smallest diffs when adding/updating new imports.

After imports, there should be at least two new lines (or follow newline rule
for classes and functions).

Always try to use explicit imports unless relative imports are the only options.
When using relative imports.

### Rationale
TODO

### Example
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

TODO: Finally, import functions after importing classes, not before.



## Spacing Between Classes, Functions and Methods
### Proposal
Add three newlines before starting a new class.

Add two newlines before starting a new method or function (unless the function
is a closure).

### Rationale
In terms, of readability this allows you to visually separate method
definitions. In the case of a closure, the function should isolate itself with a
preceding and proceeding newline.

What this also allows us to do is space out lines within functions as much as we
need wherever readability is required without worrying about space between
independent functions themselves.

### Example
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


## Single vs. Double Quotes
### Proposal
If the string is an identifier, use single quotes. If it is a proper string or
f-string, use double quotes.


## Function Arguments
### Proposal
- Keyword arguments should follow the same order as the function definition.
- When writing new function definitions - sort alphabetically, or by importance.

### Rationale
### Example



### Rationale
### Example

## Unused Arguments



### Exceptions
### Proposal
Libraries or packages may define their own exceptions. When doing so they must
inherit from an existing exception class. Exception names should end in Error
and should not introduce repetition (foo.FooError).

Always treat general `Exceptions` as `exn` and not `e`

### Rationale
### Example



## Imports
## Exceptions

## Variables

### Proposal
* While they are technically variables, module-level constants are permitted and
encouraged. For example: _MAX_HOLY_HANDGRENADE_COUNT = 3. Constants must be named
using all caps with underscores. See Naming below.

* Avoid global variables.

* If needed, globals should be declared at the module level and made internal to
the module by prepending an _ to the name. External access must be done through
public module-level functions. See Naming below.


### Rationale

### Example

### Miscellaneous


### Indentation
Indent your code blocks with 4 spaces.

Never use tabs or mix tabs and spaces. In cases of implied line continuation,
you should align wrapped elements either vertically, as per the examples in the
line length section; or using a hanging indent of 4 spaces, in which case there
should be nothing after the open parenthesis or bracket on the first line.



### Rationale
### Example



## Google Python Style Guide Notes
- Check yapf - https://github.com/google/yapf/
- Checkout pylint


### Unused Arguments
def viking_cafe_order(spam: str, beans: str, eggs: Optional[str] = None) -> str:
    del beans, eggs  # Unused by vikings.
    return spam + spam + spam
Other common forms of suppressing this warning include using ‘_ as the identifier for the unused argument or prefixing the argument name with ‘unused_’, or assigning them to ‘_’. These forms are allowed but no longer encouraged. These break callers that pass arguments by name and do not enforce that the arguments are actually unused.





Exceptions must follow certain conditions:

Make use of built-in exception classes when it makes sense. For example, raise a ValueError to indicate a programming mistake like a violated precondition (such as if you were passed a negative number but required a positive one). Do not use assert statements for validating argument values of a public API. assert is used to ensure internal correctness, not to enforce correct usage nor to indicate that some unexpected event occurred. If an exception is desired in the latter cases, use a raise statement. For example:
Never use catch-all except: statements, or catch Exception or StandardError, unless you are

re-raising the exception, or
creating an isolation point in the program where exceptions are not propagated but are recorded and suppressed instead, such as protecting a thread from crashing by guarding its outermost block.
Python is very tolerant in this regard and except: will really catch everything including misspelled names, sys.exit() calls, Ctrl+C interrupts, unittest failures and all kinds of other exceptions that you simply don’t want to catch.

Minimize the amount of code in a try/except block. The larger the body of the try, the more likely that an exception will be raised by a line of code that you didn’t expect to raise an exception. In those cases, the try/except block hides a real error.

Use the finally clause to execute code whether or not an exception is raised in the try block. This is often useful for cleanup, i.e., closing a file.



-- Insert Google Style Guide


Look up pytype


3.2 Line length
Maximum line length is 80 characters.

Explicit exceptions to the 80 character limit:

Long import statements.
URLs, pathnames, or long flags in comments.
Long string module level constants not containing whitespace that would be inconvenient to split across lines such as URLs or pathnames.
Pylint disable comments. (e.g.: # pylint: disable=invalid-name)
Do not use backslash line continuation except for with statements requiring three or more context managers.

Make use of Python’s implicit line joining inside parentheses, brackets and braces. If necessary, you can add an extra pair of parentheses around an expression.

Yes: foo_bar(self, width, height, color='black', design=None, x='foo',
             emphasis=None, highlight=0)

     if (width == 0 and height == 0 and
         color == 'red' and emphasis == 'strong'):
When a literal string won’t fit on a single line, use parentheses for implicit line joining.

x = ('This will build a very long long '
     'long long long long long long string')
Within comments, put long URLs on their own line if necessary.

Yes:  # See details at
      # http://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
No:  # See details at
     # http://www.example.com/us/developer/documentation/api/content/\
     # v2.0/csv_file_name_extension_full_specification.html
It is permissible to use backslash continuation when defining a with statement whose expressions span three or more lines. For two lines of expressions, use a nested with statement:

Yes:  with very_long_first_expression_function() as spam, \
           very_long_second_expression_function() as beans, \
           third_thing() as eggs:
          place_order(eggs, beans, spam, beans)
No:  with VeryLongFirstExpressionFunction() as spam, \
          VeryLongSecondExpressionFunction() as beans:
       PlaceOrder(beans, spam)
Yes:  with very_long_first_expression_function() as spam:
          with very_long_second_expression_function() as beans:
              place_order(beans, spam)
Make note of the indentation of the elements in the line continuation examples above; see the indentation section for explanation.

In all other cases where a line exceeds 80 characters, and the yapf auto-formatter does not help bring the line below the limit, the line is allowed to exceed this maximum. Authors are encouraged to manually break the line up per the notes above when it is sensible.


3.3 Parentheses
Use parentheses sparingly.

It is fine, though not required, to use parentheses around tuples. Do not use them in return statements or conditional statements unless using parentheses for implied line continuation or to indicate a tuple.

Yes: if foo:
         bar()
     while x:
         x = bar()
     if x and y:
         bar()
     if not x:
         bar()
     # For a 1 item tuple the ()s are more visually obvious than the comma.
     onesie = (foo,)
     return foo
     return spam, beans
     return (spam, beans)
     for (x, y) in dict.items(): ...
No:  if (x):
         bar()
     if not(x):
         bar()
     return (foo)





3.4.1 Trailing commas in sequences of items?
Trailing commas in sequences of items are recommended only when the closing container token ], ), or } does not appear on the same line as the final element. The presence of a trailing comma is also used as a hint to our Python code auto-formatter YAPF to direct it to auto-format the container of items to one item per line when the , after the final element is present.



3.6 Whitespace
Follow standard typographic rules for the use of spaces around punctuation.

No whitespace inside parentheses, brackets or braces.

Yes: spam(ham[1], {'eggs': 2}, [])
No:  spam( ham[ 1 ], { 'eggs': 2 }, [ ] )
No whitespace before a comma, semicolon, or colon. Do use whitespace after a comma, semicolon, or colon, except at the end of the line.

Yes: if x == 4:
         print(x, y)
     x, y = y, x
No:  if x == 4 :
         print(x , y)
     x , y = y , x
No whitespace before the open paren/bracket that starts an argument list, indexing or slicing.

Yes: spam(1)
No:  spam (1)
Yes: dict['key'] = list[index]
No:  dict ['key'] = list [index]
No trailing whitespace.

Surround binary operators with a single space on either side for assignment (=), comparisons (==, <, >, !=, <>, <=, >=, in, not in, is, is not), and Booleans (and, or, not). Use your better judgment for the insertion of spaces around arithmetic operators (+, -, *, /, //, %, **, @).

Yes: x == 1
No:  x<1
Never use spaces around = when passing keyword arguments or defining a default parameter value, with one exception: when a type annotation is present, do use spaces around the = for the default parameter value.

Yes: def complex(real, imag=0.0): return Magic(r=real, i=imag)
Yes: def complex(real, imag: float = 0.0): return Magic(r=real, i=imag)
No:  def complex(real, imag = 0.0): return Magic(r = real, i = imag)
No:  def complex(real, imag: float=0.0): return Magic(r = real, i = imag)
Don’t use spaces to vertically align tokens on consecutive lines, since it becomes a maintenance burden (applies to :, #, =, etc.):

Yes:
  foo = 1000  # comment
  long_name = 2  # comment that should not be aligned

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
No:
  foo       = 1000  # comment
  long_name = 2     # comment that should not be aligned

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }


3.7 Shebang Line
Most .py files do not need to start with a #! line. Start the main file of a program with #!/usr/bin/env python3 (to support virtualenvs) or #!/usr/bin/python3 per PEP-394.

This line is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules. It is only necessary on a file intended to be executed directly.


Continue on from here: https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings


Refernece: https://google.github.io/styleguide/pyguide.html

The following values in Python are false in the context of if and other logical contexts:

False
None
numeric values equal to 0, such as 0, 0.0, -0.0
empty strings: '' and u''
empty containers (such as lists, tuples and dictionaries)
anything that implements __bool__ (in Python3) to return False, or __nonzero__ (in Python2) to return False or 0.
anything that doesn't implement __bool__ (in Python3) or __nonzero__ (in Python2), but does implement __len__ to return a value equal to 0
An object is considered "false" if any of those applies, and "true" otherwise, regardless of whether it's actually equal to or identical with False or True

Now, if you've arranged that x is necessarily one of the objects True or False, then you can safely write if x. If you've arranged that the "trueness" of x indicates whether or not to perform the operation, regardless of type, then you can safely write if x. Where you can write that you should prefer to do so, since it's cleaner to read.

Normally, if it is allowed for x to take the value True then you're in one of those two cases, and so you would not write if x is True. The important thing is to correctly document the meaning of x, so that it reflects the test used in the code.

Python programmers are expected to know what's considered true, so if you just document, "runs the function if x is true", then that expresses what your original code does. Documenting it, "runs the function if x is True" would have a different meaning, and is less commonly used precisely because of the style rule in PEP8 that says to test for trueness rather than the specific value True.

However, if you wanted the code to behave differently in the case where x is an empty container from the case where it is None, then you would write something like if x is not None.


Order of procedures
When you add a new procedure to a file, don't just type it wherever your cursor happens to be. Instead, place related procedures together. It is often helpful to put a block comment (e.g., starting with a row of 75 asterisks, or whatever style you use, so long as you are consistent) at the beginning of each group of related procedures. 

In general, put public methods before private ones in your files. Organize your file with helper methods (whether public or private) after the main entry points. This permits readers to read your code top-down, which is more comprehensible: the purpose of each piece of code, and how it fits into the whole, is obvious. A reader can forward-reference to just the specification, not the whole implementation, of a helper method. This doesn't mean you necessarily have to write your in a code top-down order, but do organize it that way for readers.

Comments
Every code file that you write (Java classes, Perl scripts, etc.) needs to have a comment at the top explaining exactly what it does and, if applicable, how to run it. Otherwise it will be a mystery to others — and perhaps to you when you return to it. In some cases one or two sentences will do; in many other cases, the description needs to be more complete. Every non-trivial procedure should also contain a brief comment saying what it does. 

Code copying
In general, you should not copy code. It is easy to make a mistake when copying, even easier to forget to update some of the copies when editing other copies, and difficult for readers to understand the distinction (or lack thereof) among the versions. Rather than copying, it is often better to use hooks or to generalize the original version.

If you are forced to copy code, then it is essential that you indicate where you got the original version from; this is important for understanding the code and for giving credit where credit is due, and to not do so is intellectually dishonest. Furthermore, you should indicate the reason for the copying and how this version differs from the original, and clearly indicate every change that you have made, perhaps with a distinctive comment that is indicated in the prefatory comment, or perhaps by giving a command that can be run to get a diff of your version of code against the original. If the original code is still being maintained, you should periodically update your code with respect to the upstream version, and should document how to do this.



Local variables
Local variables should have the most restrictive scope possible. For instance, don't do this:

  int x;
  ...
  for () {
    ...
    x = ...;
    ...
  }
Instead, do this:

  for () {
    ...
    int x = ...;
    ...
  }
A loop-carried dependence is when a variable is (sometimes) set on one loop iteration and used on the next iteration. A loop-carried dependence is the only reason to declare, external to a loop, a variable that is set in the loop. Reducing scopes makes it clear that there are no loop-carried dependences. Likewise, if two loops both use a temporary variable, you should declare two separate variables rather than reusing the same one, to indicate that there are no inter-loop dependences.

Initialization
Every variable and field should be explicitly initialized (set to an initial value). However, it should never be redundantly initialized to a temporary value that will not be read.


Initialization for variables
If a variable is initialized after its declaration but before it is used, it should not be initialized to a temporary value that will never be read. An example is

  int x;    // it would be bad style to initialize x to a dummy value
  if (p) {
    x = someValue;
  } else {
    x = otherValue;
  }
It is clearer, when possible, not to reassign values immediately. Prefer the above construct with an else clause over

  int x = otherValue; // this is confusing; put it in an else clause instead
  if (p) {
    x = someValue;
  }
Initialization for fields
Fields should also be initialized exactly once. If a field is initialized by the constructor, then its declaration should not initialize it to a temporary value that will never be read.

If a declaration has an initializer, that should be its initial value.
If a declaration has no initializer, that is a signal to the programmer to look elsewhere for the initial value (and that the initial value differs for different instantiations).
In some languages (for example, Java), it is possible to omit the initializer for a field: boolean myField; is equivalent to boolean myField = false;. The short version is no more efficient, but it is more confusing. A reader must waste time searching the code (including in subclasses) to determine the initial value. The code is clearer if the initializer is explicit. Do so for all datatypes, including objects whose default value (in the absence of an initializer) is null.

Code formatting and whitespace
When code has a consistent style, particularly within a single file but also over an entire project, the code is much easier to read and understand. I don't wish to spend an excessive amount of time or energy promulgating coding guidelines, but here are a few things you should pay attention to.

Use a consistent indentation style. When editing an existing file, adopt its indentation style rather than writing your additions in an incompatible style. This means that you must set your editor to respect the current indentation style. You can do this by hand, but that's error-prone and programmers hate to perform tasks manually. You should be able to find a customization package that does this for you. For example, Emacs users can use dtrt-indent, which causes Emacs to set its indentation parameters to whatever the file already happens to use (for C and Java code).

In general, do not re-format existing files to suit your own personal indentation style. That does you very little good (you should be comfortable using any consistent indentation style), it destroys the version control history information by modifying every line of code, and it annoys others who wrote or maintain the code.

Ensure that whitespace makes keywords easy to read: do not jam punctuation against other entities, which makes the program hard to read. Here are some examples of this rule:

Place whitespace around the outside of grouping punctuation: use "if (foo) bar;" rather than "if(foo)bar;".
Use "} else {" rather than "}else{".
Place a space after // that starts a comment.
Additionally, make keywords and procedure calls visually distinct. Do not place whitespace between a procedure name and its arguments. Thus, you would write "while (x != 0)" but "myProcedure(x != 0)".




Diffs before checkin
Before you commit a change, you should always run the status and diff command, such as svn status or hg status and svn diff or hg diff, to see exactly what changes you have made. It is far too easy to inadvertently check in changes that you didn't intend to, and it is far to easy to fail to check in part of a larger change. (This advice is equally applicable to papers as it is to code.)


https://stackoverflow.com/questions/64063732/type-hint-for-return-return-none-and-no-return-at-all


https://www.python.org/dev/peps/pep-0484/#using-none

https://stackoverflow.com/questions/36797282/python-void-return-type-annotation

https://stackoverflow.com/questions/19202633/python-3-type-hinting-for-none

https://mypy.readthedocs.io/en/stable/kinds_of_types.html#:~:text=None%20is%20a%20type%20with,functions%20that%20implicitly%20return%20None%20.&text=The%20Python%20interpreter%20internally%20uses,always%20used%20in%20type%20annotations.