Bool functions
--------------

Functions can return bool values just like any other type, which is
often convenient for hiding complicated tests inside functions. For
example:

::

    bool isSingleDigit (int x)
    {
      if (x >= 0 && x < 10) {
        return true;
      } else {
        return false;
      }
    }

The name of this function is isSingleDigit. It is common to give boolean
functions names that sound like yes/no questions. The return type is
bool, which means that every return statement has to provide a bool
expression.

The code itself is straightforward, although it is a bit longer than it
needs to be. Remember that the expression x >= 0 && x < 10 has type
bool, so there is nothing wrong with returning it directly, and avoiding
the if statement altogether:

::

    bool isSingleDigit (int x)
    {
      return (x >= 0 && x < 10);
    }

In main you can call this function in the usual ways:

::

      cout << isSingleDigit (2) << endl;
      bool bigFlag = !isSingleDigit (17);

.. activecode:: fivethree
  :language: cpp
  :caption: Bool functions

  #include <iostream>
  #include <cmath>
  using namespace std;

   bool isSingleDigit (int x)
   {
     return (x >= 0 && x < 10);
   }

    int main ()
    {
    cout << isSingleDigit (2) << endl;
    bool bigFlag = !isSingleDigit (17);
      return 0;
    }

The first line outputs the value true because 2 is a single-digit
number. Unfortunately, when C++ outputs bools, it does not display the
words true and false, but rather the integers 1 and 0. [1]_

The second line assigns the value true to bigFlag only if 17 is *not* a
single-digit number.

The most common use of bool functions is inside conditional statements

::

      if (isSingleDigit (x)) {
        cout << "x is little" << endl;
      } else {
        cout << "x is big" << endl;
      }

.. dragndrop:: dragndrop_five_three
    :feedback: Try again!
    :match_1:  (x%2 == 1 && x == 7)|||0
    :match_2: (x%2 == 0 || x + 1 == 4)|||1


    Match the conditional statement to its output, assuming it is outputted using cout and x = 3.
