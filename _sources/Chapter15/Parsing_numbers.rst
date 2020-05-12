Parsing numbers
---------------

The next task is to convert the numbers in the file from strings to
integers. When people write large numbers, they often use commas to
group the digits, as in 1,750. Most of the time when computers write
large numbers, they don’t include commas, and the built-in functions for
reading numbers usually can’t handle them. That makes the conversion a
little more difficult, but it also provides an opportunity to write a
comma-stripping function, so that’s ok. Once we get rid of the commas,
we can use the library function ``atoi`` to convert to integer. ``atoi``
is defined in the header file ``cstdlib``.

To get rid of the commas, one option is to traverse the string and check
whether each character is a digit. If so, we add it to the result
string. At the end of the loop, the result string contains all the
digits from the original string, in order.


.. activecode:: fifteen_two_three
  :language: cpp

    #include <iostream>
    using namespace std;

   int convertToInt (const apstring& s)
   {
     apstring digitString = "";

     for (int i=0; i<s.length(); i++) {
       if (isdigit (s[i])) {
         digitString += s[i];
       }
     }
     return atoi (digitString.c_str());
   }

The variable ``digitString`` is an example of an **accumulator**. It is
similar to the counter we saw in Section `[loopcount] <#loopcount>`__,
except that instead of getting incremented, it gets accumulates one new
character at a time, using string concatentation.

The expression

::

         digitString += s[i];

is equivalent to

::

         digitString = digitString + s[i];

Both statements add a single character onto the end of the existing
string.

Since ``atoi`` takes a C string as a parameter, we have to convert
``digitString`` to a C string before passing it as an argument.
