Math functions
--------------

In mathematics, you have probably seen functions like :math:`\sin` and
:math:`\log`, and you have learned to evaluate expressions like
:math:`\sin(\pi/2)` and :math:`\log(1/x)`. First, you evaluate the
expression in parentheses, which is called the **argument** of the
function. For example, :math:`\pi/2` is approximately 1.571, and
:math:`1/x` is 0.1 (if :math:`x` happens to be 10).

Then you can evaluate the function itself, either by looking it up in a
table or by performing various computations. The :math:`\sin` of 1.571
is 1, and the :math:`\log` of 0.1 is -1 (assuming that :math:`\log`
indicates the logarithm base 10).

This process can be applied repeatedly to evaluate more complicated
expressions like :math:`\log(1/\sin(\pi/2))`. First we evaluate the
argument of the innermost function, then evaluate the function, and so
on.

C++ provides a set of built-in functions that includes most of the
mathematical operations you can think of. The math functions are invoked
using a syntax that is similar to mathematical notation:

.. activecode:: threetwo
  :language: cpp
  :caption: Using math functions

  #include <iostream>
  #include <cmath>
  using namespace std;

    int main ()
    {
      double result = log (17.0);
      double angle = 1.5;
      double height = sin (angle);
      cout << result << endl;
      cout << angle << endl;
      cout << height << endl;
      return 0;
    }

The first example sets log to the logarithm of 17, base :math:`e`. There
is also a function called log10 that takes logarithms base 10.

The second example finds the sine of the value of the variable angle.
C++ assumes that the values you use with sin and the other trigonometric
functions (cos, tan) are in *radians*. To convert from degrees to
radians, you can divide by 360 and multiply by :math:`2 \pi`.

If you don’t happen to know :math:`\pi` to 15 digits, you can calculate
it using the acos function. The arccosine (or inverse cosine) of -1 is
:math:`\pi`, because the cosine of :math:`\pi` is -1.

.. activecode:: threethree
  :language: cpp
  :caption: Using math functions

  #include <iostream>
  #include <cmath>
  using namespace std;

    int main ()
    {
      double pi = acos(-1.0);
      double degrees = 90;
      double angle = degrees * 2 * pi / 360.0;
      cout << pi << endl;
      cout << degrees << endl;
      cout << angle << endl;
      return 0;
    }

Before you can use any of the math functions, you have to include the
math **header file**. Header files contain information the compiler
needs about functions that are defined outside your program. For
example, in the “Hello, world!” program we included a header file named
iostream using an **include** statement:

::

    #include <iostream>
    using namespace std;

iostream contains information about input and output (I/O) streams,
including the object named cout. C++ has a powerful feature called
namespaces, that allow you to write your own implementation of cout. But
in most cases, we would need to use the standard implementation. To
convey this to the compiler, we use the line

::

    using namespace std;

As a rule of the thumb, you should write using namespace std; whenever
you use iostream.

Similarly, the math header file contains information about the math
functions. You can include it at the beginning of your program along
with iostream:

::

    #include <cmath>

Such header files have an initial ‘c’ to signify that these header files
have been derived from the **C** language.

**There is one statement missing in the program below. Add it in so that the
program complies.**

.. activecode:: threefour
  :language: cpp
  :caption: Add a statement!

  #include <iostream>
  using namespace std;

    int main ()
    {
      double pi = acos(-0.5);
      double degrees = 45;
      double angle = degrees * 2 * pi / 360.0;
      cout << pi << endl;
      cout << degrees << endl;
      cout << angle << endl;
      return 0;
    }
