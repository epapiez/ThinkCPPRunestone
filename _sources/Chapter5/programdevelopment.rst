Program development
-------------------

At this point you should be able to look at complete C++ functions and
tell what they do. But it may not be clear yet how to go about writing
them. I am going to suggest one technique that I call **incremental
development**.

As an example, imagine you want to find the distance between two points,
given by the coordinates :math:`(x_1, y_1)` and :math:`(x_2, y_2)`. By
the usual definition,

.. math:: distance = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}

The first step is to consider what a distance function should look like
in C++. In other words, what are the inputs (parameters) and what is the
output (return value).

In this case, the two points are the parameters, and it is natural to
represent them using four doubles. The return value is the distance,
which will have type double.

Already we can write an outline of the function:

::

    double distance (double x1, double y1, double x2, double y2) {
      return 0.0;
    }

The return statement is a placekeeper so that the function will compile
and return something, even though it is not the right answer. At this
stage the function doesn’t do anything useful, but it is worthwhile to
try compiling it so we can identify any syntax errors before we make it
more complicated.

In order to test the new function, we have to call it with sample
values. Somewhere in main I would add:

::

      double dist = distance (1.0, 2.0, 4.0, 6.0);
      cout << dist << endl;

I chose these values so that the horizontal distance is 3 and the
vertical distance is 4; that way, the result will be 5 (the hypotenuse
of a 3-4-5 triangle). When you are testing a function, it is useful to
know the right answer.

Once we have checked the syntax of the function definition, we can start
adding lines of code one at a time. After each incremental change, we
recompile and run the program. That way, at any point we know exactly
where the error must be—in the last line we added.

The next step in the computation is to find the differences
:math:`x_2 - x_1` and :math:`y_2 - y_1`. I will store those values in
temporary variables named dx and dy.

::

    double distance (double x1, double y1, double x2, double y2) {
      double dx = x2 - x1;
      double dy = y2 - y1;
      cout << "dx is " << dx << endl;
      cout << "dy is " << dy << endl;
      return 0.0;
    }

I added output statements that will let me check the intermediate values
before proceeding. As I mentioned, I already know that they should be
3.0 and 4.0.

When the function is finished I will remove the output statements. Code
like that is called **scaffolding**, because it is helpful for building
the program, but it is not part of the final product. Sometimes it is a
good idea to keep the scaffolding around, but comment it out, just in
case you need it later.

The next step in the development is to square dx and dy. We could use
the pow function, but it is simpler and faster to just multiply each
term by itself.

::

    double distance (double x1, double y1, double x2, double y2) {
      double dx = x2 - x1;
      double dy = y2 - y1;
      double dsquared = dx*dx + dy*dy;
      cout << "dsquared is " << dsquared;
      return 0.0;
    }

Again, I would compile and run the program at this stage and check the
intermediate value (which should be 25.0).

Finally, we can use the sqrt function to compute and return the result.

::

    double distance (double x1, double y1, double x2, double y2) {
      double dx = x2 - x1;
      double dy = y2 - y1;
      double dsquared = dx*dx + dy*dy;
      double result = sqrt (dsquared);
      return result;
    }

Then in main, we should output and check the value of the result.

.. activecode:: fivetwo
  :language: cpp
  :caption: Program development

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

    int main ()
    {
      double dist = distance (1.0, 2.0, 4.0, 6.0);
      cout << dist << endl;
      return 0;
    }

As you gain more experience programming, you might find yourself writing
and debugging more than one line at a time. Nevertheless, this
incremental development process can save you a lot of debugging time.

The key aspects of the process are:

-  Start with a working program and make small, incremental changes. At
   any point, if there is an error, you will know exactly where it is.

-  Use temporary variables to hold intermediate values so you can output
   and check them.

-  Once the program is working, you might want to remove some of the
   scaffolding or consolidate multiple statements into compound
   expressions, but only if it does not make the program difficult to
   read.

.. mchoice:: test_question_five_two_one_test__
   :answer_a: combining the parameters
   :answer_b: printing out the parameters
   :answer_c: returning something
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct! Return something of the same data type as the return type of the function.

   What is a helpful first placekeeper when outlining a function?


.. mchoice:: test_question_five_two_one_
   :answer_a: Use temporary variables to hold intermediate values so you can output and check them.
   :answer_b: Start with a working program and make small, incremental changes. That way you know exactly where the error is if you have one.
   :answer_c: Writing a program from start to finish, and then testing at the end in order to understand all of the errors at once.
   :answer_d: Once the program is working, you might want to remove some of the or consolidate multiple statements into compound expressions, but only if it does not make the program difficult to read.
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct! Trying to understand all of the errors in your program at once can make it very difficult to understand.
   :feedback_d: Try again!

   Which of the following is not a key aspect of the incremental development process?


.. mchoice:: test_question_five_two_one_one
   :answer_a: Scaffolding - the use of more than 5 lines in a function with no indentation
   :answer_b: Placekeeping - allows the function to compile and return something
   :answer_c: Scaffolding - code that is helpful for testing values, but is not included in the final product
   :answer_d: Placekeeping - the use of parameters in a function
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct! Printing out the values can help you understand whether the function is working or not.
   :feedback_d: Try again!

   The print statements in the distance function will be removed after testing. What is this called, and what is its purpose?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    double distance (double x1, double y1, double x2, double y2) {
      double dx = x2 - x1;
      double dy = y2 - y1;
      cout << "dx is " << dx << endl;
      cout << "dy is " << dy << endl;
      return 0.0;
    }
