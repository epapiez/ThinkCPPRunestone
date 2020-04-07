Operators
---------

**Operators** are special symbols that are used to represent simple
computations like addition and multiplication. Most of the operators in
C++ do exactly what you would expect them to do, because they are common
mathematical symbols. For example, the operator for adding two integers
is ``+``.

The following are all legal C++ expressions whose meaning is more or
less obvious:

::

    1+1        hour-1       hour*60 + minute     minute/60

Expressions can contain both variables names and integer values. In each
case the name of the variable is replaced with its value before the
computation is performed.

Addition, subtraction and multiplication all do what you expect, but you
might be surprised by division. For example, compile the following program around
observe the output.

.. activecode:: twonine
  :language: cpp
  :caption: Operators

    #include <iostream>
    using namespace std;

    int main ()
    {
      int hour, minute;
      hour = 11;
      minute = 59;
      cout << "Number of minutes since midnight: ";
      cout << hour*60 + minute << endl;
      cout << "Fraction of the hour that has passed: ";
      cout << minute/60 << endl;
      return 0;
    }

The first line is what we expected, but the second line is odd. The
value of the variable minute is 59, and 59 divided by 60 is 0.98333, not
0. The reason for the discrepancy is that C++ is performing **integer
division**.

When both of the **operands** are integers (operands are the things
operators operate on), the result must also be an integer, and by
definition integer division always rounds *down*, even in cases like
this where the next integer is so close.

A possible alternative in this case is to calculate a percentage rather
than a fraction:

::

      cout << "Percentage of the hour that has passed: ";
      cout << minute*100/60 << endl;

The result is:

::

    Percentage of the hour that has passed: 98

Again the result is rounded down, but at least now the answer is
approximately correct. In order to get an even more accurate answer, we
could use a different type of variable, called floating-point, that is
capable of storing fractional values. We’ll get to that in the next
chapter.

**Fix the code below so that it prints out the total cost of the meal (fries,
a milkshake, and a hamburger) using one of the operators.**

.. activecode:: twoten
  :language: cpp
  :caption: Operators check

    #include <iostream>
    using namespace std;

    int main ()
    {
      int fries, milkshake, hamburger;
      fries = 2;
      milkshake = 3;
      hamburger = 6;
      cout << "The total cost of the meal is ";
      cout << << " dollars." << endl;
      return 0;
    }

.. dragndrop:: dragndrop_two_five
    :feedback: Try again!
    :match_1:  x*10|||100
    :match_2: x-10|||0
    :match_3: 100/x|||10
    :match_4: (x+x+x+x+x)*20|||1000

    Match the statement to the result, given x = 10.
