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
