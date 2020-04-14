Floating-point
--------------

In the last chapter we had some problems dealing with numbers that were
not integers. We worked around the problem by measuring percentages
instead of fractions, but a more general solution is to use
floating-point numbers, which can represent fractions as well as
integers. In C++, there are two floating-point types, called float and
double. In this book we will use doubles exclusively.

You can create floating-point variables and assign values to them using
the same syntax we used for the other types. For example:

::

      double pi;
      pi = 3.14159;

It is also legal to declare a variable and assign a value to it at the
same time:

::

      int x = 1;
      string empty = "";
      double pi = 3.14159;

In fact, this syntax is quite common. A combined declaration and
assignment is sometimes called an **initialization**.

Although floating-point numbers are useful, they are often a source of
confusion because there seems to be an overlap between integers and
floating-point numbers. For example, if you have the value 1, is that an
integer, a floating-point number, or both?

Strictly speaking, C++ distinguishes the integer value 1 from the
floating-point value 1.0, even though they seem to be the same number.
They belong to different types, and strictly speaking, you are not
allowed to make assignments between types. For example, the following is
illegal

::

        int x = 1.1;

because the variable on the left is an int and the value on the right is
a double. But it is easy to forget this rule, especially because there
are places where C++ automatically converts from one type to another.
For example,

::

        double y = 1;

should technically not be legal, but C++ allows it by converting the int
to a double automatically. This leniency is convenient, but it can cause
problems; for example:

::

        double y = 1 / 3;

You might expect the variable y to be given the value 0.333333, which is
a legal floating-point value, but in fact it will get the value 0.0. The
reason is that the expression on the right appears to be the ratio of
two integers, so C++ does *integer* division, which yields the integer
value 0. Converted to floating-point, the result is 0.0.

One way to solve this problem (once you figure out what it is) is to
make the right-hand side a floating-point expression:

::

        double y = 1.0 / 3.0;

This sets y to 0.333333, as expected.

All the operations we have seen—addition, subtraction, multiplication,
and division—work on floating-point values, although you might be
interested to know that the underlying mechanism is completely
different. In fact, most processors have special hardware just for
performing floating-point operations.

.. dragndrop:: dragndrop_three_one
    :feedback: Try again!
    :match_1:  double pi = 3.14;|||initialization
    :match_2: pi = 3.14;|||assignment
    :match_3: double pi;|||declaration

    Match the statement to the word that best describes it.

.. mchoice:: test_question_three_one_
   :practice: T
   :answer_a: combination
   :answer_b: initialization
   :answer_c: floating
   :answer_d: assignment
   :correct: b
   :feedback_a: Try again!
   :feedback_b: Correct!
   :feedback_c: Try again!
   :feedback_d: Try again!

   What is it called when a declaration and assignment statement is combined?
