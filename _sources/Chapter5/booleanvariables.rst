Boolean variables
-----------------

As usual, for every type of value, there is a corresponding type of
variable. In C++ the boolean type is called **bool**. Boolean variables
work just like the other types:

::

      bool fred;
      fred = true;
      bool testResult = false;

The first line is a simple variable declaration; the second line is an
assignment, and the third line is a combination of a declaration and as
assignment, called an initialization.

As I mentioned, the result of a comparison operator is a boolean, so you
can store it in a bool variable

::

      bool evenFlag = (n%2 == 0);     // true if n is even
      bool positiveFlag = (x > 0);    // true if x is positive

and then use it as part of a conditional statement later

::

      if (evenFlag) {
        cout << "n was even when I checked it" << endl;
      }

A variable used in this way is called a **flag**, since it flags the
presence or absence of some condition.

.. dragndrop:: dragndrop_five_one
    :feedback: Try again!
    :match_1: x / 2 > 4|||false
    :match_2: x >= 2|||true

    Match the conditional statement to the correct boolean, given x = 2.
