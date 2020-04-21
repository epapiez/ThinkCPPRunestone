Composition
-----------

As you should expect by now, once you define a new function, you can use
it as part of an expression, and you can build new functions using
existing functions. For example, what if someone gave you two points,
the center of the circle and a point on the perimeter, and asked for the
area of the circle?

Let’s say the center point is stored in the variables ''xc'' and ''yc'', and the
perimeter point is in ''xp'' and ''yp''. The first step is to find the radius of
the circle, which is the distance between the two points. Fortunately,
we have a function, distance, that does that.

::

      double radius = distance (xc, yc, xp, yp);

The second step is to find the area of a circle with that radius, and
return it.

::

      double result = area (radius);
      return result;

Wrapping that all up in a function, we get:

::

    double fred (double xc, double yc, double xp, double yp) {
      double radius = distance (xc, yc, xp, yp);
      double result = area (radius);
      return result;
    }

The name of this function is ''fred'', which may seem odd. I will explain
why in the next section.

The temporary variables radius and area are useful for development and
debugging, but once the program is working we can make it more concise
by composing the function calls:

::

    double fred (double xc, double yc, double xp, double yp) {
      return area (distance (xc, yc, xp, yp));
    }

**See everything come together below!**

.. activecode:: fivethreee
  :language: cpp
  :caption: Composition

  #include <iostream>
  #include <cmath>
  using namespace std;

    double distance (double x1, double y1, double x2, double y2) {
      double dx = x2 - x1;
      double dy = y2 - y1;
      double dsquared = dx*dx + dy*dy;
      double result = sqrt (dsquared);
      return result;
    }

    double area (double radius) {
      double area = 3.14 * (radius * radius);
      return area;
    }

    double fred (double xc, double yc, double xp, double yp) {
      return area (distance (xc, yc, xp, yp));
    }

    int main ()
    {
      double circle_area = fred (1.0, 2.0, 4.0, 6.0);
      cout << circle_area << endl;
      return 0;
    }

.. mchoice:: test_question_five_three_one_one
   :answer_a: print_hello_name
   :answer_b: love_cupcakes
   :answer_c: eat_pizza
   :answer_d: All of the above
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Try again!
   :feedback_d: Correct! While it is not good style to name a function something that doesn't describe its function, it is technically legal and does not have any effect on the function's execution.

   Technically, what can the name of the following function also be?

   .. code-block:: cpp

    void printHelloName (string name) {
      cout << "Hello " << name << "!" <<  endl;
    }
