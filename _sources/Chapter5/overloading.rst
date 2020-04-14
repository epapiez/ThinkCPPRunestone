Overloading
-----------

In the previous section you might have noticed that ''fred'' and ''area''
perform similar functions—finding the area of a circle—but take
different parameters. For ''area'', we have to provide the radius; for ''fred''
we provide two points.

If two functions do the same thing, it is natural to give them the same
name. In other words, it would make more sense if ''fred'' were called ''area''.

Having more than one function with the same name, which is called
**overloading**, is legal in C++ *as long as each version takes
different parameters*. So we can go ahead and rename ''fred'':

::

    double area (double xc, double yc, double xp, double yp) {
      return area (distance (xc, yc, xp, yp));
    }

This looks like a recursive function, but it is not. Actually, this
version of ''area'' is calling the other version. When you call an
overloaded function, C++ knows which version you want by looking at the
arguments that you provide. If you write:

::

        double x = area (3.0);

C++ goes looking for a function named ''area'' that takes a double as an
argument, and so it uses the first version. If you write

::

        double x = area (1.0, 2.0, 4.0, 6.0);

C++ uses the second version of ''area''.

Many of the built-in C++ commands are overloaded, meaning that there are
different versions that accept different numbers or types of parameters.

Although overloading is a useful feature, it should be used with
caution. You might get yourself nicely confused if you are trying to
debug one version of a function while accidentally calling a different
one.

Actually, that reminds me of one of the cardinal rules of debugging:
**make sure that the version of the program you are looking at is the
version of the program that is running!** Some time you may find
yourself making one change after another in your program, and seeing the
same thing every time you run it. This is a warning sign that for one
reason or another you are not running the version of the program you
think you are. To check, stick in an output statement (it doesn’t matter
what it says) and make sure the behavior of the program changes
accordingly.

**Check your understanding!**

.. mchoice:: test_question_five_two
   :answer_a: double price(int a, int b);
   :answer_b: double price(int a, string b, string c);
   :answer_c: double price(double x, int y, string z);
   :correct: b
   :feedback_a: This function has the same parameters as the first function below.
   :feedback_b: Correct! While this function has the same number of parameters as the second function, it takes different types of parameters.
   :feedback_c: This function has the same parameters as the second function below.

   Which of the following function declarations would be legal if it was added to the program below?

   .. code-block:: cpp

     double price (int x, int y);

     double price (double a, int b, string c);

.. mchoice:: test_question_five_two_one
   :answer_a: recursiveness
   :answer_b: debugging
   :answer_c: overloading
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct!

   What can be the use of the same name for different functions, such as seen below, be called?

   .. code-block:: cpp

     double price(int x, int y);

     double price(double a, int b, string c);
