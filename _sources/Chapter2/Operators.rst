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

    1+1
    hour-1
    hour*60 + minute
    minute/60

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

   int main () {
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
capable of storing fractional values. 

.. note::
   In C++, floating-points are declared as type ``double``. We’ll get 
   to that in the next chapter.

.. dragndrop:: question2_7_1
    :feedback: Try again!
    :match_1:  x*10|||100
    :match_2: x-10|||0
    :match_3: 100/x|||10
    :match_4: (x+x+x+x+x)*20|||1000

    Match the statement to the result, given ``int x = 10``.

.. fillintheblank:: question2_7_2

    Integer division always rounds |blank| to the nearest integer.

    - :[Dd][Oo][Ww][Nn]: Correct!
      :.*: Try again!

.. mchoice:: question2_7_3
   :answer_a: 0
   :answer_b: 1
   :answer_c: .667
   :answer_d: .6666666667
   :correct: a
   :feedback_a: Correct! In integer division, the decimal part is simply discarded, which is why the result would be 0.
   :feedback_b: The decimal part is discarded. This means we do not round up, only down.
   :feedback_c: In integer division, an integer must be the result.
   :feedback_d: In integer division, an integer must be the result.

   What is the output?

   .. code-block:: cpp

    int main ()
    {
      int sum = 2 / 3;
      cout << sum;
    }

.. activecode:: twoten
  :language: cpp
  :caption: Operators check

  Fix the code below so that it prints out the total cost of the meal (fries,
  a milkshake, and a hamburger) using one of the operators.

  ~~~~
  #include <iostream>
  using namespace std;

  int main () {
     int fries, milkshake, hamburger;
     fries = 2;
     milkshake = 3;
     hamburger = 6;
     cout << "The total cost of the meal is ";
     cout << << " dollars." << endl;
     return 0;
  }
