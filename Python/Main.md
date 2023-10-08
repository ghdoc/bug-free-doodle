**Python**

- Using PYTHON Interpreter

- Env Var & starting Interpreter  
    *UNIX*
- /usr/local/python
- /usr/local/bin/python3.7
- putting /usr/local/bin in your Unix shell’s search path makes it possible to start it by typing the command
- $python3.7

- *WIN*
- c:\python3.7

- Python launcher "py"
- py
- py -2.7
- py -0 => to see which versions are installed

- Exiting the interpreter

- Typing an end-of-file character (Control-D on Unix, Control-Z on Windows) at the primary prompt causes the interpreter to exit with a zero exit status
- >>>quit()

- Interactive Input Editing and History Substitution  
    https://docs.python.org/3/tutorial/interactive.html#tut-interacting
- Typing Control-P to the first Python prompt, If it beeps, you have command line editing. If ^P is echoed, command line editing isn’t available; you’ll only be able to use backspace to remove characters from the current line
- The interpreter operates somewhat like the Unix shell: when called with standard input connected to a tty device, it reads and executes commands interactively; when called with a file name argument or with a file as standard input, it reads and executes a script from that file
- Virtual Environments

- If the launcher is run with no explicit Python version, a virtual env (created with the standard library 'venv' module or the external 'virtualenv' tool) active, the launcher will run the virtual env's interpreter rather than the global one.
- To run the global interpreter, either deactivate the virtual environment, or explicitly specify the global Python version.
- To run v2.7  
    #! python
- import sys
- sys.stdout.write("hello from Python %s\n" % (sys.version,))
- To run v3.0  
    #! python3
- import sys
- sys.stdout.write("hello from Python %s\n" % (sys.version,))
- To allow shebang lines in Python scripts to be portable between Unix and Windows, this launcher supports a number of ‘virtual’ commands to specify which interpreter to use. The supported virtual commands are:
- /usr/bin/env python
- /usr/bin/python
- /usr/local/bin/python
- python
- For example, if the first line of your script starts with
- #! /usr/bin/python
- The default Python will be located and used. As many Python scripts written to work on Unix will already have this line, you should find these scripts can be used by the launcher without modification. If you are writing a new script on Windows which you hope will be useful on Unix, you should use one of the shebang lines starting with /usr.
- Any of the above virtual commands can be suffixed with an explicit version (either just the major version, or the major and minor version). Furthermore the 32-bit version can be requested by adding “-32” after the minor version. I.e. /usr/bin/python2.7-32 will request usage of the 32-bit python 2.7.
- New in version 3.7: Beginning with python launcher 3.7 it is possible to request 64-bit version by the “-64” suffix. Furthermore it is possible to specify a major and architecture without minor (i.e. /usr/bin/python3-64).
- The /usr/bin/env form of shebang line has one further special property. Before looking for installed Python interpreters, this form will search the executable PATH for a Python executable. This corresponds to the behaviour of the Unix env program, which performs a PATH search.

- Argument Passing

- import sys

- When known to the interpreter, the script name and additional arguments thereafter are turned into a list of strings and assigned to the argv variable in the sys module.

- sys.argv[0] is an empty string - when no script and no arguments are given
- sys.argv[0] is set to '-' When the script name is given as '-' (meaning standard input)
- sys.argv[0] is set to '-c' When -c command is used
- sys.argv[0] is set to the full name of the located module - When -m moduleis used

- Introduction to Python

- In addition to int and float, Python supports other types of numbers, such as Decimal and Fraction
- Python also has built-in support for complex numbers, and uses the j or J suffix to indicate the imaginary part (e.g. 3+5j).
- / division always returns float
- // floor division, returns an int  
    >>> 17 / 3  # classic division returns a float
- 5.666666666666667
- >>>
- >>> 17 // 3  # floor division discards the fractional part
- 5
- ** calc power  
    >>> 5 ** 2  # 5 squared
- 25
- >>> 2 ** 7  # 2 to the power of 7
- 128
- full support for floating point; operators with mixed type operands convert the integer operand to floating point  
    >>> 4 * 3.75 - 1
- 14.0
- In interactive mode, the last printed expression is assigned to the variable _  
    >>> tax = 12.5 / 100
- >>> price = 100.50
- >>> price * tax
- 12.5625
- >>> price + _
- 113.0625
- >>> round(_, 2)
- 113.06

- This variable should be treated as read-only by the user. Don’t explicitly assign a value to it — you would create an independent local variable with the same name masking the built-in variable with its magic behavior.

- **Strings Are IMMUTABLE**  
    >>> 'spam eggs'  # single quotes
- 'spam eggs'
- >>> 'doesn\'t'  # use \' to escape the single quote...
- "doesn't"
- >>> "doesn't"  # ...or use double quotes instead
- "doesn't"
- >>> '"Yes," they said.'
- '"Yes," they said.'
- >>> "\"Yes,\" they said."
- '"Yes," they said.'
- >>> '"Isn\'t," they said.'
- '"Isn\'t," they said.'

- In the interactive interpreter, the output string is enclosed in quotes and special characters are escaped with backslashes. While this might sometimes look different from the input (the enclosing quotes could change), the two strings are equivalent. The string is enclosed in double quotes if the string contains a single quote and no double quotes, otherwise it is enclosed in single quotes. The print() function produces a more readable output, by omitting the enclosing quotes and by printing escaped and special characters  
    >>> '"Isn\'t," they said.'
- '"Isn\'t," they said.'
- >>> print('"Isn\'t," they said.')
- "Isn't," they said.
- >>> s = 'First line.\nSecond line.'  # \n means newline
- >>> s  # without print(), \n is included in the output
- 'First line.\nSecond line.'
- >>> print(s)  # with print(), \n produces a new line
- First line.
- Second line.
- If you don’t want characters prefaced by \ to be interpreted as special characters, you can use raw strings by adding an r before the first quote:  
    >>> print('C:\some\name')  # here \n means newline!
- C:\some
- ame
- >>> print(r'C:\some\name')  # note the r before the quote
- C:\some\name
- String literals can **span multiple lines**. One way is using triple-quotes: """...""" or '''...'''. End of lines are automatically included in the string, but it’s possible to prevent this by adding a \ at the end of the line  
    print("""\
- Usage: thingy [OPTIONS]
-     -h                        Display this usage message
-     -H hostname               Hostname to connect to
- """)

- Usage: thingy [OPTIONS]
-     -h                        Display this usage message
-     -H hostname               Hostname to connect to
- Strings can be **concatenated** (glued together) with the + operator, and repeated with *:  
    >>> # 3 times 'un', followed by 'ium'
- >>> 3 * 'un' + 'ium'
- 'unununium'
- Two or more string literals (i.e. the ones enclosed between quotes) next to each other are automatically concatenated. **only works with two literals though, not with variables or expressions**  
    >>> 'Py' 'thon'
- 'Python'

- >>> text = ('Put several strings within parentheses '
- ...         'to have them joined together.')
- >>> text
- 'Put several strings within parentheses to have them joined together.'
- String slicing  
    >>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
- 'Py'
- >>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
- 'tho'

- Note how the start is always included, and the end always excluded. This makes sure that s[:i] + s[i:] is always equal to s:  
    >>> word[:2] + word[2:]
- 'Python'
- >>> word[:4] + word[4:]
- 'Python'
- Slice indices have useful defaults; an omitted first index defaults to zero, an omitted second index defaults to the size of the string being sliced.
- Indices  
    +---+---+---+---+---+---+
- | P   |  y  |   t  |  h  |  o  |  n  |
- +---+---+---+---+---+---+
- 0   1   2   3   4   5   6
- -6  -5  -4  -3  -2  -1
- Slicing out of range is handles gracefully, but indexing out of range throws error

- len(s) gives length
- String literals are written in a variety of ways:

- Single quotes: 'allows embedded "double" quotes'
- Double quotes: "allows embedded 'single' quotes".
- Triple quoted: '''Three single quotes''', """Three double quotes"""

- the r (“raw”) prefix disables most escape sequence processing
- There is also no mutable string type, but str.join() or io.StringIO can be used to efficiently construct strings from multiple fragments.
- String Methods  
    [https://docs.python.org/3.7/library/stdtypes.html#textseq](https://docs.python.org/3.7/library/stdtypes.html#textseq)

- str.**capitalize**() - Return a copy of the string with its first character capitalized and the rest lowercased.  
     
- str.**center**(width[, fillchar]) - Return centered in a string of length width. Padding is done using the specified fillchar (default is an ASCII space). The original string is returned if width is less than or equal to len(s)  
     
- str.**count**(sub[, start[, end]]) - Return the number of non-overlapping occurrences of substring sub in the range [start, end]. Optional arguments start and end are interpreted as in slice notation  
     
- str.**endswith**(suffix[, start[, end]]) - Return True if the string ends with the specified suffix, otherwise return False.  suffix can also be a tuple of suffixes to look for. With optional start, test beginning at that position. With optional end, stop comparing at that position.  
     see startswith https://docs.python.org/3.7/library/stdtypes.html#str.startswith
- str.**expandtabs**(tabsize=8) - Return a copy of the string where all tab characters are replaced by one or more spaces  
    >>> '01\t012\t0123\t01234'.expandtabs()
- '01      012     0123    01234'
- >>> '01\t012\t0123\t01234'.expandtabs(4)
- '01  012 0123    01234'
- str.**find**(sub[, start[, end]]) - Return the lowest index in the string where substring sub is found within the slice s[start:end]. Optional arguments start and end are interpreted as in slice notation. Return -1 if sub is not found.  
    see rfind https://docs.python.org/3.7/library/stdtypes.html#str.rfind
- The **find**() method should be used only if you need to know the position of sub. To check if sub is a substring or not, use the in operator:  
    >>> 'Py' in 'Python'
- True
- str.**format**(*args, **kwargs) - string on which which this format method is called, can contain literal text or replacement fields delimited by braces {} Each replacement field contains either the numeric index of a positional argument, or the name of a keyword argument. Returns a copy of the string where each replacement field is replaced with the string value of the corresponding argument.  
    >>> "The sum of 1 + 2 is {0}".format(1+2)
- 'The sum of 1 + 2 is 3'
- See Format String Syntax for a description of the various formatting options that can be specified in format strings.

- Note When formatting a number (int, float, complex, decimal.Decimal and subclasses) with the n type (ex: '{:n}'.format(1234)), the function temporarily sets the LC_CTYPE locale to the LC_NUMERIC locale to decode decimal_point and thousands_sep fields of localeconv() if they are non-ASCII or longer than 1 byte, and the LC_NUMERIC locale is different than the LC_CTYPElocale. This temporary change affects other threads.

- Changed in version 3.7: When formatting a number with the n type, the function sets temporarily the LC_CTYPE locale to the LC_NUMERIC locale in some cases.
- str.**format_map**(mapping_dict) - reads in mapping from a dictionary  
    >>> s = {'name':'sandeep','age':37}
- >>> 'My name is {name} and my age is {age}'.format_map(s)
- 'My name is sandeep and my age is 37'
- str.**index**(sub[, start[, end]]) - like find, but raise ValueError when the substring is not found  
    see rindex https://docs.python.org/3.7/library/stdtypes.html#str.rindex
- str.**isalnum**() - Return true if all characters in the string are alphanumeric and there is at least one character, false otherwise. A character c is alphanumeric if one of the following returns True: c.**isalpha**(), c.**isdecimal**(), c.**isdigit**(), or c.**isnumeric**()  
     
- str.**isalpha**() - Return true if all characters in the string are alphabetic and there is at least one character, false otherwise. Alphabetic characters are those characters defined in the Unicode character database as “Letter”, i.e., those with general category property being one of “Lm”, “Lt”, “Lu”, “Ll”, or “Lo”. Note that this is different from the “Alphabetic” property defined in the Unicode Standard.  
    https://docs.python.org/3.7/reference/lexical_analysis.html#identifiers
- The Unicode category codes mentioned above stand for:

- Lu - uppercase letters

- Ll - lowercase letters

- Lt - titlecase letters

- Lm - modifier letters

- Lo - other letters

- Nl - letter numbers

- Mn - nonspacing marks

- Mc - spacing combining marks

- Nd - decimal numbers

- Pc - connector punctuations

- Other_ID_Start - explicit list of characters in PropList.txt to support backwards compatibility

- Other_ID_Continue - likewise
- str.**isascii**() - Return true if the string is empty or all characters in the string are ASCII, false otherwise. ASCII characters have code points in the range U+0000-U+007F. New in version 3.7.  
     
- str.**isdecimal**() - Return true if all characters in the string are decimal characters and there is at least one character, false otherwise. Decimal characters are those that can be used to form numbers in base 10, e.g. U+0660, ARABIC-INDIC DIGIT ZERO. Formally a decimal character is a character in the Unicode General Category “Nd”.
- str.**isdigit**() - Return true if all characters in the string are digits and there is at least one character, false otherwise. Digits include decimal characters and digits that need special handling, such as the compatibility superscript digits. This covers digits which cannot be used to form numbers in base 10, like the Kharosthi numbers. Formally, a digit is a character that has the property value Numeric_Type=Digit or Numeric_Type=Decimal.
- str.**islower**() / **isupper**()- Return true if all cased characters 4 in the string are upper/lowercase and there is at least one cased character, false otherwise
- str.**isnumeric**() - Return true if all characters in the string are numeric characters, and there is at least one character, false otherwise. 
- str.**isspace**() - Return true if there are only whitespace characters in the string and there is at least one character, false otherwise.
- str.**join**(iterable) - Return a string which is the concatenation of the strings in iterable. A TypeError will be raised if there are any non-string values in iterable, including bytes objects. The separator between elements is the string providing this method
- str.**ljust**(width[, fillchar]) / str.**rjust**(width[, fillchar]) - Return the string left/right justified in a string of length width. Padding is done using the specified fillchar (default is an ASCII space). The original string is returned if width is less than or equal to len(s).  
    see rjust https://docs.python.org/3.7/library/stdtypes.html#str.rjust
- str.**lower**() - Return a copy of the string with all the cased characters 4 converted to lowercase.  
     
- str.**lstrip**([chars]) - Return a copy of the string with leading characters removed. The chars argument is a string specifying the set of characters to be removed. If omitted or None, the chars argument defaults to removing whitespace. The chars argument is not a prefix; rather, all combinations of its values are stripped  
    see rstrip https://docs.python.org/3.7/library/stdtypes.html#str.rstrip

- >>> '   spacious   '.lstrip()
- 'spacious   '
- >>> 'www.example.com'.lstrip('cmowz.')
- 'example.com'
- str.**partition**(sep) - Split the string at the first occurrence of sep, and return a 3-tuple containing the part before the separator, the separator itself, and the part after the separator. If the separator is not found, return a 3-tuple containing the string itself, followed by two empty strings.  
     see rpartition https://docs.python.org/3.7/library/stdtypes.html#str.rpartition
- str.**replace**(old, new[, count]) - Return a copy of the string with all occurrences of substring old replaced by new. If the optional argument count is given, only the first count occurrences are replaced.  
     
- str.**split**(sep=None, maxsplit=-1) - Return a list of the words in the string, using sep as the delimiter string. If maxsplit is given, at most maxsplit splits are done (thus, the list will have at most maxsplit+1 elements). If maxsplit is not specified or -1, then there is no limit on the number of splits (all possible splits are made).  
    >>> '1,2,3'.split(',')
- ['1', '2', '3']
- >>> '1,2,3'.split(',', maxsplit=1)
- ['1', '2,3']
- >>> '1,2,,3,'.split(',')
- ['1', '2', '', '3', '']

- If sep is given, consecutive delimiters are not grouped together and are deemed to delimit empty strings (for example, '1,,2'.split(',') returns ['1', '', '2']). The sep argument may consist of multiple characters (for example, '1<>2<>3'.split('<>') returns ['1', '2', '3']). Splitting an empty string with a specified separator returns [''].

- str.**splitlines**([keepends]) - Return a list of the lines in the string, breaking at line boundaries. Line breaks are not included in the resulting list unless keepends is given and true.

- This method splits on the following line boundaries. In particular, the boundaries are a superset of universal newlines.  
    Representation

- Description

- \n

- Line Feed

- \r

- Carriage Return

- \r\n

- Carriage Return + Line Feed

- \v or \x0b

- Line Tabulation

- \f or \x0c

- Form Feed

- \x1c

- File Separator

- \x1d

- Group Separator

- \x1e

- Record Separator

- \x85

- Next Line (C1 Control Code)

- \u2028

- Line Separator

- \u2029

- Paragraph Separator

- Changed in version 3.2: \v and \f added to list of line boundaries.

- str.**strip**([chars]) - Return a copy of the string with the leading and trailing characters removed. The chars argument is a string specifying the set of characters to be removed. If omitted or None, the chars argument defaults to removing whitespace. The chars argument is not a prefix or suffix; rather, all combinations of its values are stripped:  
    see lstrip and rstrip https://workflowy.com/#/07c0227cf13d
- >>> '   spacious   '.strip()
- 'spacious'
- >>> 'www.example.com'.strip('cmowz.')
- 'example'

- The outermost leading and trailing chars argument values are stripped from the string. Characters are removed from the leading end until reaching a string character that is not contained in the set of characters in chars. A similar action takes place on the trailing end.  
    >>> comment_string = '#....... Section 3.2.1 Issue #32 .......'
- >>> comment_string.strip('.#! ')
- 'Section 3.2.1 Issue #32'

- **formatting**

- 'hello {} it is a {} day'.format(name, 'great')
- f'hello {name} it is a {type_of_day} day'

- Collections

- Are comma separated  
    >>> squares = [1, 4, 9, 16, 25]
- >>> squares
- [1, 4, 9, 16, 25]
- items of different types
- indexed and sliced  
    >>> squares[0]  # indexing returns the item
- 1
- >>> squares[-1]
- 25
- >>> squares[-3:]  # slicing returns a new list
- [9, 16, 25]
- slice operations return a new list, returns a new (shallow) copy of the list  
    >>> squares[:]
- [1, 4, 9, 16, 25]
- >>> a = [-1, 5, 10, -4, 23, 28]
- >>> a[1:3] (start, end but not inclusive)
- [5, 10]
- >>> a[:3]
- [-1, 5, 10]
- concatenation  
    >>> squares + [36, 49, 64, 81, 100]
- [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
- mutable  
    >>> cubes = [1, 8, 27, 65, 125]  # something's wrong here
- >>> 4 ** 3  # the cube of 4 is 64, not 65!
- 64
- >>> cubes[3] = 64  # replace the wrong value
- >>> cubes
- [1, 8, 27, 64, 125]
- add to end of list using append(...)  
    >>> cubes.append(216)  # add the cube of 6
- >>> cubes.append(7 ** 3)  # and the cube of 7
- >>> cubes
- [1, 8, 27, 64, 125, 216, 343]
- Update list in slices  
    >>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
- >>> letters
- ['a', 'b', 'c', 'd', 'e', 'f', 'g']
- >>> # replace some values
- >>> letters[2:5] = ['C', 'D', 'E']
- >>> letters
- ['a', 'b', 'C', 'D', 'E', 'f', 'g']
- >>> # now remove them
- >>> letters[2:5] = []
- >>> letters
- ['a', 'b', 'f', 'g']
- >>> # clear the list by replacing all the elements with an empty list
- >>> letters[:] = []
- >>> letters
- []
- len() for length of list
- nested lists  
    >>> a = ['a', 'b', 'c']
- >>> n = [1, 2, 3]
- >>> x = [a, n]
- >>> x
- [['a', 'b', 'c'], [1, 2, 3]]
- >>> x[0]
- ['a', 'b', 'c']
- >>> x[0][1]
- 'b'
- Arrays

- from array import array
- create

- scores = array('d')
- scores.append(97)
- print(scores)

- Arrays vs List vs Dictionary

- Array

- only of one data type(numeric)
- has to be created by calling constructor: array('d')

- List

- each item could be different data type
- l = []

- l.append('apple')

- create empty list of size = [None] * size

- Dictionary

- each k,v can be different type
- person = {'andrew':34, 'john':45}
- person['john']=54
- person['aby'] = 12
- adding DOESNOT guarantee order of insertion

- Set

- set() to create empty set
- s = {1,2,3}
- s.update([1,2,3,5])
- s will be {1,2,3,5}
- s.remove(key present in set)
- s.add(1)

- Numbers

- power **
- str(num) to convert to string
- print(int(fnum) + int(fmul))
- print(float(fnum) + float(fmul))

- Dates

- from datetime import datetime
- current_date = datetime.now()
- datetime.strptime(birthdaystr, '%d/%m/%Y')

- Control Flow

- **while**

- while index < len(names):

- index = index + 1

- **if**,**elif**,**else**

- if province in ('mumbai', 'delhi):

- do something

- elif province == 'bangalore':

- do something else

- **for**

- If you need to modify the sequence you are iterating over while inside the loop (for example to duplicate selected items), it is recommended that you first make a copy. Iterating over a sequence does not implicitly make a copy.  
    >>> for w in words[:]:  # Loop over a slice copy of the entire list.
- ...     if len(w) > 6:
- ...         words.insert(0, w)
- ...
- >>> words
- ['defenestrate', 'cat', 'window', 'defenestrate']
- range allows to start range at another number  
    range(4) => 0,1,2,3
- range(5,5+5) => 5,6,7,8,9
- range allows to specify a step for increment (negative allowed)  
    range(4,10,2) => 4,6,8
- >>> list(range(-4,-11,-3))
- [-4, -7, -10]
- to iterate over sequence or dictionary  
    >>> a = ['Mary', 'had', 'a', 'little', 'lamb']
- >>> for i in range(len(a)):
- ...     print(i, a[i])
- ...
- 0 Mary
- 1 had
- 2 a
- 3 little
- 4 lamb

- >>> people = ['a','b']
- >>> for l in people:
- ...     print(l)
- ...
- a
- b

- >>> people_map = {'a':12,'b':13}
- >>> for m in people_map:
- ...     print(m)
- ...
- a
- b

- **break** and **continue** AND '**else clause on loop**'

- break - breaks innermost loop
- else in a loop - Loop statements may have an else clause; it is executed when the loop terminates through exhaustion of the list (with for) or when the condition becomes false (with while), but not when the loop is terminated by a break statement.  
    >>> for n in range(2, 10):
- ...     for x in range(2, n):
- ...         if n % x == 0:
- ...             print(n, 'equals', x, '*', n//x)
- ...             break
- ...     else:
- ...         # loop fell through without finding a factor
- ...         print(n, 'is a prime number')
- ...
- 2 is a prime number
- 3 is a prime number
- 4 equals 2 * 2
- 5 is a prime number
- 6 equals 2 * 3
- 7 is a prime number
- 8 equals 2 * 4
- 9 equals 3 * 3

- **pass**

- The pass statement does nothing. It can be used when a statement is required syntactically but the program requires no action  
    >>> while True:
- ...     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
- ...
- creating minimal classes  
    >>> class MyEmptyClass:
- ...     pass
- ...
- Another place pass can be used is as a place-holder for a function or conditional body when you are working on new code, allowing you to keep thinking at a more abstract level. The pass is silently ignored  
    >>> def initlog(*args):
- ...     pass   # Remember to implement this!
- ...

- **functions**  
    >>> def fib(n):    # write Fibonacci series up to n
- ...     """Print a Fibonacci series up to n."""
- ...     a, b = 0, 1
- ...     while a < n:
- ...         print(a, end=' ')
- ...         a, b = b, a+b
- ...     print()
- ...
- >>> # Now call the function we just defined:
- ... fib(2000)
- 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

- **def** - keyword starts a function, must be followed by function name and the parameterized list of formal parameters
- **first statement** can be string literal to produce docstring 
- **execution**

- The execution of a function introduces a new symbol table used for the local variables of the function. 
- All variable assignments in a function store the value in the local symbol table; 
- Variable references first look in the local symbol table, 

- then in the local symbol tables of enclosing functions, 
- then in the global symbol table, and finally in the table of built-in names. 

- Global variables and variables of enclosing functions cannot be directly assigned a value within a function (unless, for global variables, named in a global statement, or, for variables of enclosing functions, named in a nonlocal statement), although they may be referenced.
- The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called; thus, arguments are passed using call by value (**where the value is always an object reference, not the value of the object**). 
- When a function calls another function, a new local symbol table is created for that call.
- A function definition introduces the function name in the current symbol table. 

- The value of the function name has a type that is recognized by the interpreter as a user-defined function. 
- This value can be assigned to another name which can then also be used as a function. This serves as a general renaming mechanism  
    >>> fib(0)
- >>> print(fib(0))
- None

- **return** - returns a value, or return without an expression argument returns None. Falling off the end of a function also returns None.
- Defaulting Argument Values  
    >>> def get_initial(name, force_uppercase=True):
- ...     if force_uppercase:
- ...             return name[0:1].upper()
- ...     else:
- ...             return name[0:1]
- ...

- >>> print(get_initial('alex'))
- A
- >>> print(get_initial('alex',False))
- a
- Positional notation of parameters  
    >>> print(get_initial(force_uppercase=False,name='friend'))
- f
- >>> print(get_initial(force_uppercase=True,name='friend'))
- F
- >>>

- Modules & Packages

- Module

- A python file with functions, classes and other components
- Creating a module  
    //helpers.py
- def display(message, is_warning=False):
- if is_warning:
- print('Warning!!' + ' ' + message)
- else:
- print(messsage)
- Importing a module to use it

- import module as a namespace  
    import helpers
- helpers.display('Not a warning!')
- import all into current namespace (to not use helpers.xxx)  
    from helpers import *
- display('Not a warning.')
- import specific items into current namespace  
    from helpers import display
- display('Not a warning')

- Package

- it is a collection of modules
- installing a package

- pip install colorama
- pip install -r requirements.txt (to install from a list of packages, listed in a txt)
- packages are installed globally by default (version management might become a problem)
- Virtual environments can be used to contain and manage package collections (really just a folder behind the scenes with all your packages)

- creating a virtual environment

- pip install virtualenv
- Windows - python -m venv <folder_name>
- OSX/Linux - virtualenv <folder_name>
- Using virtual environments  
    //Windows systems
- //cmd.exe
- <folder_name>\Scripts\Activate.bat
- //PowerShell
- <folder_name>Scripts\Activate.ps1

- //bash shell
- ../<folder_name>/Scripts/activate

- OSC/Linux (bash)
- <folder_name>/bin/activate
- To install into a virtual env  
    python -m venv venv
- the second venv is the name of the folder being created for virtual env

- Calling an API

- Function on a webserver is exposed via an API
- HTTP is a standard protocol for sending messages across the web

- GET

- pass values in query string only
- special chars must be escaped
- limited amount of data

- POST

- Pass values in query string and body
- no need to escape special characters if passed in body
- can pass large amounts of data, including images in body

- python 'request' lib is useful for POST methods

- request.post(address,http_headers,function_params,message_body)

- Other

- zip

- python 3 return a zip object, which is an iterable.
- list(zipped_obj) extracts it into a list

- Unit Testing  
    Code Structure
- root_folder
- __init__.py
- Library
- __init__.py
- class.py
- test
- __init__.py
- test_class.py

- cd into root_folder
- python -m unittest Library\test\[test_class.py](http://test_class.py/)

- Functions

- Defining Functions  
    >>> def fib(n):    # write Fibonacci series up to n
- ...     """Print a Fibonacci series up to n."""
- ...     a, b = 0, 1
- ...     while a < n:
- ...         print(a, end=' ')
- ...         a, b = b, a+b
- ...     print()
- ...
- >>> # Now call the function we just defined:
- ... fib(2000)
- 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597

- def - definition of a function
- fib - name of a function
- n - one argument to a function
- """Print a Fibonacci series up to n.""" - docstring of a function
- The execution of a function introduces a new symbol table

- used for the local variables of the function
- all variable assignments store the value in the local symbol table
- variable references first look in the local symbol table, 

- then in the local symbol tables of enclosing functions

- then in the global symbol table

- and finally in the table of built-in names.

- Thus, global variables and variables of enclosing functions can't be directly assigned a value within a function **unless**

- Global variables are named in a 'global' statement
- Variables of enclosing functions are named in 'nonlocal' statement

- The actual parameters to a function call are introduced in the local symbol table of the called function when it is called;
- Arguments are pass using _call by value_ where _value_ is the object reference
- When a function calls another function, a new symbol table is created for that call
- A function definition introduces the function name in the current symbol table. 

- The value of the function name has a type that is recognized by the interpreter as a user-defined function.
- This value can be assigned to another name which can be used as a function  
    >>> fib
- <function fib at 10042ed0>
- >>> f = fib
- >>> f(100)
- 0 1 1 2 3 5 8 13 21 34 55 89

- **Functions not returning a value return None**

- More on Defining Functions

- Default Argument Values  
    def ask_ok(prompt, retries=4, reminder='Please try again!'):
-     while True:
-         ok = input(prompt)
-         if ok in ('y', 'ye', 'yes'):
-             return True
-         if ok in ('n', 'no', 'nop', 'nope'):
-             return False
-         retries = retries - 1
-         if retries < 0:
-             raise ValueError('invalid user response')
-         print(reminder)

- Default values are evaluated at the point of function definition, in the defining scope  
    i = 5

- def f(arg=i):
-     print(arg)

- i = 6
- f()
- prints 5
- Default values are evaluated only once  
    def f(a, L=[]):
-     L.append(a)
-     return L

- print(f(1))
- print(f(2))
- print(f(3))
- ------
- [1]
- [1, 2]
- [1, 2, 3]
- -------------------------------
- if you don't want the default to be shared between subsequent calls, you can write:
- def f(a, L=None):
-     if L is None:
-         L = []
-     L.append(a)
-     return L

- Keyword Arguments

- Functions can also be called using keyword arguments of the form kwarg=value. For instance, the following function  
    def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
-     print("-- This parrot wouldn't", action, end=' ')
-     print("if you put", voltage, "volts through it.")
-     print("-- Lovely plumage, the", type)
-     print("-- It's", state, "!")

- accepts one required argument (voltage) and three optional arguments (state, action, and type). This function can be called in any of the following ways:  
    parrot(1000)                                          # 1 positional argument
- parrot(voltage=1000)                                  # 1 keyword argument
- parrot(voltage=1000000, action='VOOOOOM')          # 2 keyword arguments
- parrot(action='VOOOOOM', voltage=1000000)          # 2 keyword arguments
- parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
- parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword

- When a final formal parameter of the form **name is present, it receives a dictionary (see Mapping Types — dict) containing all keyword arguments except for those corresponding to a formal parameter
- This may be combined with a formal parameter of the form *name (described in the next subsection) which receives a tuple containing the positional arguments beyond the formal parameter list. (*name must occur before **name.)  
    def cheeseshop(kind, *arguments, **keywords):
-     print("-- Do you have any", kind, "?")
-     print("-- I'm sorry, we're all out of", kind)
-     for arg in arguments:
-         print(arg)
-     print("-" * 40)
-     for kw in keywords:
-         print(kw, ":", keywords[kw])
- --------------------------
- could be called like:
- cheeseshop("Limburger", "It's very runny, sir.",
-           "It's really very, VERY runny, sir.",
-           shopkeeper="Michael Palin",
-           client="John Cleese",
-           sketch="Cheese Shop Sketch")
- ----------------------------
- -- Do you have any Limburger ?
- -- I'm sorry, we're all out of Limburger
- It's very runny, sir.
- It's really very, VERY runny, sir.
- ----------------------------------------
- shopkeeper : Michael Palin
- client : John Cleese
- sketch : Cheese Shop Sketch

- Special parameters

- Position-Only parameters

- Positional-only parameters are placed before a / (forward-slash). The / is used to logically separate the positional-only parameters from the rest of the parameters

- Keyword-Only parameters

- To mark parameters as keyword-only, indicating the parameters must be passed by keyword argument, place an * in the arguments list just before the first keyword-only parameter.

- Example  
    >>> def standard_arg(arg):
- ...     print(arg)
- ...
- >>> def pos_only_arg(arg, /):
- ...     print(arg)
- ...
- >>> def kwd_only_arg(*, arg):
- ...     print(arg)
- ...
- >>> def combined_example(pos_only, /, standard, *, kwd_only):
- ...     print(pos_only, standard, kwd_only)

- >>> combined_example(1, 2, kwd_only=3)
- 1 2 3

- >>> combined_example(1, standard=2, kwd_only=3)
- 1 2 3
- But using / (positional only arguments), it is possible since it allows name as a positional argument and 'name' as a key in the keyword arguments:  
    def foo(name, /, **kwds):
-     return 'name' in kwds
- >>> foo(1, **{'name': 2})
- True

- Arbitary Argument List

- a function can be called with an arbitrary number of arguments. These arguments will be wrapped up in a tuple (see Tuples and Sequences). Before the variable number of arguments, zero or more normal arguments may occur.  
    def write_multiple_items(file, separator, *args):
-     file.write(separator.join(args))
- Normally, these variadic arguments will be last in the list of formal parameters, because they scoop up all remaining input arguments that are passed to the function. Any formal parameters which occur after the *args parameter are ‘keyword-only’ arguments, meaning that they can only be used as keywords rather than positional arguments.  
    >>> def concat(*args, sep="/"):
- ...     return sep.join(args)
- ...
- >>> concat("earth", "mars", "venus")
- 'earth/mars/venus'
- >>> concat("earth", "mars", "venus", sep=".")
- 'earth.mars.venus'

- Unpacking argument lists

- If the arguments are in a list or tuple, but need to be unpacked for a function call requiring separate positional arguments  
    >>> list(range(3, 6))            # normal call with separate arguments
- [3, 4, 5]
- >>> args = [3, 6]
- >>> list(range(*args))            # call with arguments unpacked from a list
- [3, 4, 5]
- /-------------
-  dictionaries can deliver keyword arguments with the **-operator:

- >>> def parrot(voltage, state='a stiff', action='voom'):
- ...     print("-- This parrot wouldn't", action, end=' ')
- ...     print("if you put", voltage, "volts through it.", end=' ')
- ...     print("E's", state, "!")
- ...
- >>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
- >>> parrot(**d)
- -- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !

- Lambda expressions

- can reference variables from the containing scope  
    >>> def make_incrementor(n):
- ...     return lambda x: x + n
- ...
- >>> f = make_incrementor(42)
- >>> f(0)
- 42
- >>> f(1)
- 43
- Another use is to pass a small function as a argument  
    >>> pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
- >>> pairs.sort(key=lambda pair: pair[1])
- >>> pairs
- [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]

- Doc strings  
    >>> def my_function():
- ...     """Do nothing, but document it.
- ...
- ...     No, really, it doesn't do anything.
- ...     """
- ...     pass
- ...
- >>> print(my_function.__doc__)
- Do nothing, but document it.

-     No, really, it doesn't do anything.
- Function annotations  
    >>> def f(ham: str, eggs: str = 'eggs') -> str:
- ...     print("Annotations:", f.__annotations__)
- ...     print("Arguments:", ham, eggs)
- ...     return ham + ' and ' + eggs
- ...
- >>> f('spam')
- Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
- Arguments: spam eggs
- 'spam and eggs'

- Tutorial  
    https://docs.python.org/3/tutorial/index.html