Composition
-----------

Just as with mathematical functions, C++ functions can be **composed**,
meaning that you use one expression as part of another. For example, you
can use any expression as an argument to a function:

::

        double x = cos (angle + pi/2);

This statement takes the value of pi, divides it by two and adds the
result to the value of angle. The sum is then passed as an argument to
the cos function.

You can also take the result of one function and pass it as an argument
to another:

.. activecode:: threefive
  :language: cpp
  :caption: Composition and math functions

  #include <iostream>
  #include <cmath>
  using namespace std;

    int main ()
    {
      double x = exp (log (10.0));
      cout << x;
    }

This statement finds the log base :math:`e` of 10 and then raises
:math:`e` to that power. The result gets assigned to x.

**Check your understanding!**

.. mchoice:: test_question_three_one
   :answer_a: double val = tan(angle + pi/3);
   :answer_b: double num = exp(cos(1.34))
   :answer_c: double y = exp(cosine(9.8)) + exp(tan(4.5));
   :correct: a
   :feedback_a: Correct!
   :feedback_b: This would be correct if it ended in a semi-colon.
   :feedback_c: Make sure to use the math keywords reserved in C++ when using math functions. Using **cosine** instead of *cos* is incorrect.


   Which of these statements has correct syntax?
