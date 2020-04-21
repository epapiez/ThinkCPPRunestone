The modulus operator
--------------------

The modulus operator works on integers (and integer expressions) and
yields the *remainder* when the first operand is divided by the second.
In C++, the modulus operator is a percent sign, ``%``. The syntax is exactly
the same as for other operators:

.. activecode:: fourone
  :language: cpp
  :caption: Modulus operator

    #include <iostream>
    using namespace std;

    int main ()
    {
      int quotient = 7 / 3;
      int remainder = 7 % 3;
      cout << quotient << endl;
      cout << remainder << endl;
      return 0;
    }

The first operator, integer division, yields 2. The second operator
yields 1. Thus, 7 divided by 3 is 2 with 1 left over.

The modulus operator turns out to be surprisingly useful. For example,
you can check whether one number is divisible by another: if ``x % y`` is
zero, then x is divisible by y.

Also, you can use the modulus operator to extract the rightmost digit or
digits from a number. For example, ``x % 10`` yields the rightmost digit of
x (in base 10). Similarly ``x % 100`` yields the last two digits.

.. mchoice:: test_question_four_one
   :practice: T
   :answer_a: Use x % 2, and if the result is 0, it is odd
   :answer_b: Use x % 2, and if the result is  1, it is odd
   :correct: b
   :feedback_a: If you divide a number by two and it has no remainder, that means it is an even number!
   :feedback_b: Yes, if you divide a number by two and it has a remainder of one, that means it is an odd number!


   How do you know whether the variable x is odd?

.. dragndrop:: dragndrop_four_one_one_
    :feedback: Try again!
    :match_1:  cout<<"Hello"; cout<<"Hello";|||one line
    :match_2: cout<<"Hello" << endl; cout<<"Hello";|||two lines

    Match the modulo expression to its result.
