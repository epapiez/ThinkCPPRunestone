.. _strings:

Strings and things
==================

Containers for strings
----------------------

We have seen five types of values—booleans, characters, integers,
floating-point numbers and strings—but only four types of
variables—``bool``, ``char``, ``int`` and ``double``. So far we have no
way to store a string in a variable or perform operations on strings.

In fact, there are several kinds of variables in C++ that can store
strings. One is a basic type that is part of the C++ language, sometimes
called “a native C string.” The syntax for C strings is a bit ugly, and
using them requires some concepts we have not covered yet, so for the
most part we are going to avoid them.

The string type we are going to use is called ``string``, which is one
of the classes that belong to the C++ Standard Library. [1]_

Unfortunately, it is not possible to avoid C strings altogether. In a
few places in this chapter I will warn you about some problems you might
run into using ``string``\ s instead of C strings.

``string`` variables
--------------------

You can create a variable with type ``string`` in the usual ways:

::

     string first;
     first = "Hello, ";
     string second = "world.";

The first line creates an ``string`` without giving it a value. The
second line assigns it the string value ``"Hello."`` The third line is a
combined declaration and assignment, also called an initialization.

Normally when string values like ``"Hello, "`` or ``"world."`` appear,
they are treated as C strings. In this case, when we assign them to an
``string`` variable, they are converted automatically to ``string``
values.

We can output strings in the usual way:

::

     cout << first << second << endl;

In order to compile this code, you will have to include the header file
for the ``string`` class, and you will have to add the file ``string``
to the list of files you want to compile. The details of how to do this
depend on your programming environment.

Before proceeding, you should type in the program above and make sure
you can compile and run it.

Extracting characters from a string
-----------------------------------

Strings are called “strings” because they are made up of a sequence, or
string, of characters. The first operation we are going to perform on a
string is to extract one of the characters. C++ uses square brackets
(``[`` and ``]``) for this operation:

::

     string fruit = "banana";
     char letter = fruit[1];
     cout << letter << endl;

The expression ``fruit[1]`` indicates that I want character number 1
from the string named ``fruit``. The result is stored in a ``char``
named ``letter``. When I output the value of ``letter``, I get a
surprise:

::

   a

``a`` is not the first letter of ``"banana"``. Unless you are a computer
scientist. For perverse reasons, computer scientists always start
counting from zero. The 0th letter (“zeroeth”) of ``"banana"`` is ``b``.
The 1th letter (“oneth”) is ``a`` and the 2th (“twoeth”) letter is
``n``.

If you want the the zereoth letter of a string, you have to put zero in
the square brackets:

::

     char letter = fruit[0];

Length
------

To find the length of a string (number of characters), we can use the
``length`` function. The syntax for calling this function is a little
different from what we’ve seen before:

::

     int length;
     length = fruit.length();

To describe this function call, we would say that we are **invoking**
the length function on the string named ``fruit``. This vocabulary may
seem strange, but we will see many more examples where we invoke a
function on an object. The syntax for function invocation is called “dot
notation,” because the dot (period) separates the name of the object,
``fruit``, from the name of the function, ``length``.

``length`` takes no arguments, as indicated by the empty parentheses
``()``. The return value is an integer, in this case 6. Notice that it
is legal to have a variable with the same name as a function.

To find the last letter of a string, you might be tempted to try
something like

::

     int length = fruit.length();
     char last = fruit[length];       // WRONG!!

That won’t work. The reason is that there is no 6th letter in
``"banana"``. Since we started counting at 0, the 6 letters are numbered
from 0 to 5. To get the last character, you have to subtract 1 from
``length``.

::

     int length = fruit.length();
     char last = fruit[length-1];

Traversal
---------

A common thing to do with a string is start at the beginning, select
each character in turn, do something to it, and continue until the end.
This pattern of processing is called a **traversal**. A natural way to
encode a traversal is with a ``while`` statement:

::

     int index = 0;
     while (index < fruit.length()) {
       char letter = fruit[index];
       cout << letter << endl;
       index = index + 1;
     }

This loop traverses the string and outputs each letter on a line by
itself. Notice that the condition is ``index < fruit.length()``, which
means that when ``index`` is equal to the length of the string, the
condition is false and the body of the loop is not executed. The last
character we access is the one with the index ``fruit.length()-1``.

The name of the loop variable is ``index``. An **index** is a variable
or value used to specify one member of an ordered set, in this case the
set of characters in the string. The index indicates (hence the name)
which one you want. The set has to be ordered so that each letter has an
index and each index refers to a single character.

As an exercise, write a function that takes an ``string`` as an argument
and that outputs the letters backwards, all on one line.

A run-time error
----------------

Way back in Section `[run-time] <#run-time>`__ I talked about run-time
errors, which are errors that don’t appear until a program has started
running.

So far, you probably haven’t seen many run-time errors, because we
haven’t been doing many things that can cause one. Well, now we are. If
you use the ``[]`` operator and you provide an index that is negative or
greater than ``length-1``, you will get a run-time error and a message
something like this:

::

   index out of range: 6, string: banana

Try it in your development environment and see how it looks.

The ``find`` function
---------------------

The ``string`` class provides several other functions that you can
invoke on strings. The ``find`` function is like the opposite the ``[]``
operator. Instead of taking an index and extracting the character at
that index, ``find`` takes a character and finds the index where that
character appears.

::

     string fruit = "banana";
     int index = fruit.find('a');

This example finds the index of the letter ``’a’`` in the string. In
this case, the letter appears three times, so it is not obvious what
``find`` should do. According to the documentation, it returns the index
of the *first* appearance, so the result is 1. If the given letter does
not appear in the string, ``find`` returns -1.

In addition, there is a version of ``find`` that takes another
``string`` as an argument and that finds the index where the substring
appears in the string. For example,

::

     string fruit = "banana";
     int index = fruit.find("nan");

This example returns the value 2.

You should remember from Section `[overloading] <#overloading>`__ that
there can be more than one function with the same name, as long as they
take a different number of parameters or different types. In this case,
C++ knows which version of ``find`` to invoke by looking at the type of
the argument we provide.

Our own version of ``find``
---------------------------

If we are looking for a letter in an ``string``, we may not want to
start at the beginning of the string. One way to generalize the ``find``
function is to write a version that takes an additional parameter—the
index where we should start looking. Here is an implementation of this
function.

::

   int find (string s, char c, int i)
   {
     while (i<s.length()) {
       if (s[i] == c) return i;
       i = i + 1;
     }
     return -1;
   }

Instead of invoking this function on an ``string``, like the first
version of ``find``, we have to pass the ``string`` as the first
argument. The other arguments are the character we are looking for and
the index where we should start.

.. _loopcount:

Looping and counting
--------------------

The following program counts the number of times the letter ``’a’``
appears in a string:

::

     string fruit = "banana";
     int length = fruit.length();
     int count = 0;

     int index = 0;
     while (index < length) {
       if (fruit[index] == 'a') {
         count = count + 1;
       }
       index = index + 1;
     }
     cout << count << endl;

This program demonstrates a common idiom, called a **counter**. The
variable ``count`` is initialized to zero and then incremented each time
we find an ``’a’``. (To **increment** is to increase by one; it is the
opposite of **decrement**, and unrelated to **excrement**, which is a
noun.) When we exit the loop, ``count`` contains the result: the total
number of a’s.

As an exercise, encapsulate this code in a function named
``countLetters``, and generalize it so that it accepts the string and
the letter as arguments.

As a second exercise, rewrite this function so that instead of
traversing the string, it uses the version of ``find`` we wrote in the
previous section.

Increment and decrement operators
---------------------------------

Incrementing and decrementing are such common operations that C++
provides special operators for them. The ``++`` operator adds one to the
current value of an ``int``, ``char`` or ``double``, and ``–`` subtracts
one. Neither operator works on ``string``\ s, and neither *should* be
used on ``bool``\ s.

Technically, it is legal to increment a variable and use it in an
expression at the same time. For example, you might see something like:

::

     cout << i++ << endl;

Looking at this, it is not clear whether the increment will take effect
before or after the value is displayed. Because expressions like this
tend to be confusing, I would discourage you from using them. In fact,
to discourage you even more, I’m not going to tell you what the result
is. If you really want to know, you can try it.

Using the increment operators, we can rewrite the letter-counter:

::

     int index = 0;
     while (index < length) {
       if (fruit[index] == 'a') {
         count++;
       }
       index++;
     }

It is a common error to write something like

::

     index = index++;             // WRONG!!

Unfortunately, this is syntactically legal, so the compiler will not
warn you. The effect of this statement is to leave the value of
``index`` unchanged. This is often a difficult bug to track down.

Remember, you can write ``index = index +1;``, or you can write
``index++;``, but you shouldn’t mix them.

String concatenation
--------------------

Interestingly, the ``+`` operator can be used on strings; it performs
string **concatenation**. To concatenate means to join the two operands
end to end. For example:

::

     string fruit = "banana";
     string bakedGood = " nut bread";
     string dessert = fruit + bakedGood;
     cout << dessert << endl;

The output of this program is ``banana nut bread``.

Unfortunately, the ``+`` operator does not work on native C strings, so
you cannot write something like

::

     string dessert = "banana" + " nut bread";

because both operands are C strings. As long as one of the operands is
an ``string``, though, C++ will automatically convert the other.

It is also possible to concatenate a character onto the beginning or end
of an ``string``. In the following example, we will use concatenation
and character arithmetic to output an abecedarian series.

“Abecedarian” refers to a series or list in which the elements appear in
alphabetical order. For example, in Robert McCloskey’s book *Make Way
for Ducklings*, the names of the ducklings are Jack, Kack, Lack, Mack,
Nack, Ouack, Pack and Quack. Here is a loop that outputs these names in
order:

::

     string suffix = "ack";

     char letter = 'J';
     while (letter <= 'Q') {
       cout << letter + suffix << endl;
       letter++;
     }

The output of this program is:

::

   Jack
   Kack
   Lack
   Mack
   Nack
   Oack
   Pack
   Qack

Of course, that’s not quite right because I’ve misspelled “Ouack” and
“Quack.” As an exercise, modify the program to correct this error.

Again, be careful to use string concatenation only with ``string``\ s
and not with native C strings. Unfortunately, an expression like
``letter + "ack"`` is syntactically legal in C++, although it produces a
very strange result, at least in my development environment.

``string``\ s are mutable
-------------------------

You can change the letters in an ``string`` one at a time using the
``[]`` operator on the left side of an assignment. For example,

::

     string greeting = "Hello, world!";
     greeting[0] = 'J';
     cout << greeting << endl;

produces the output ``Jello, world!``.

.. _incomparable:

``string``\ s are comparable
----------------------------

All the comparison operators that work on ``int``\ s and ``double``\ s
also work on ``strings``. For example, if you want to know if two
strings are equal:

::

     if (word == "banana") {
       cout << "Yes, we have no bananas!" << endl;
     }

The other comparison operations are useful for putting words in
alphabetical order.

::

     if (word < "banana") {
       cout << "Your word, " << word << ", comes before banana." << endl;
     } else if (word > "banana") {
       cout << "Your word, " << word << ", comes after banana." << endl;
     } else {
       cout << "Yes, we have no bananas!" << endl;
     }

You should be aware, though, that the ``string`` class does not handle
upper and lower case letters the same way that people do. All the upper
case letters come before all the lower case letters. As a result,

::

   Your word, Zebra, comes before banana.

A common way to address this problem is to convert strings to a standard
format, like all lower-case, before performing the comparison. The next
sections explains how. I will not address the more difficult problem,
which is making the program realize that zebras are not fruit.

Character classification
------------------------

It is often useful to examine a character and test whether it is upper
or lower case, or whether it is a character or a digit. C++ provides a
library of functions that perform this kind of character classification.
In order to use these functions, you have to include the header file
``ctype.h``.

::

     char letter = 'a';
     if (isalpha(letter)) {
       cout << "The character " << letter << " is a letter." << endl;
     }

You might expect the return value from ``isalpha`` to be a ``bool``, but
for reasons I don’t even want to think about, it is actually an integer
that is 0 if the argument is not a letter, and some non-zero value if it
is.

This oddity is not as inconvenient as it seems, because it is legal to
use this kind of integer in a conditional, as shown in the example. The
value 0 is treated as ``false``, and all non-zero values are treated as
``true``.

Technically, this sort of thing should not be allowed—integers are not
the same thing as boolean values. Nevertheless, the C++ habit of
converting automatically between types can be useful.

Other character classification functions include ``isdigit``, which
identifies the digits 0 through 9, and ``isspace``, which identifies all
kinds of “white” space, including spaces, tabs, newlines, and a few
others. There are also ``isupper`` and ``islower``, which distinguish
upper and lower case letters.

Finally, there are two functions that convert letters from one case to
the other, called ``toupper`` and ``tolower``. Both take a single
character as a parameter and return a (possibly converted) character.

::

     char letter = 'a';
     letter = toupper (letter);
     cout << letter << endl;

The output of this code is ``A``.

As an exercise, use the character classification and conversion library
to write functions named ``stringToUpper`` and ``stringToLower`` that
take a single ``string`` as a parameter, and that modify the string by
converting all the letters to upper or lower case. The return type
should be ``void``.

Other ``string`` functions
--------------------------

This chapter does not cover all the ``string`` functions. Two additional
ones, ``c_str`` and ``substr``, are covered in
Section `[finput] <#finput>`__ and Section `[parsing] <#parsing>`__.

Glossary
--------

object:
   A collection of related data that comes with a set of functions that
   operate on it. The objects we have used so far are the ``cout``
   object provided by the system, and ``string``\ s.

index:
   A variable or value used to select one of the members of an ordered
   set, like a character from a string.

traverse:
   To iterate through all the elements of a set performing a similar
   operation on each.

counter:
   A variable used to count something, usually initialized to zero and
   then incremented.

increment:
   Increase the value of a variable by one. The increment operator in
   C++ is ``++``. In fact, that’s why C++ is called C++, because it is
   meant to be one better than C.

decrement:
   Decrease the value of a variable by one. The decrement operator in
   C++ is ``–``.

concatenate:
   To join two operands end-to-end.

.. [1]
   You might be wondering what I mean by **class**.It will be a few more
   chapters before I can give a complete definition, but for now a class
   is a collection of functions that defines the operations we can
   perform on some type. The ``string`` class contains all the functions
   that apply to ``string``\ \ s.
