Preconditions
-------------

Often when you write a function you make implicit assumptions about the
parameters you receive. If those assumptions turn out to be true, then
everything is fine; if not, your program might crash.

To make your programs more robust, it is a good idea to think about your
assumptions explicitly, document them as part of the program, and maybe
write code that checks them.

For example, let’s take another look at ``calculateCartesian``. Is there
an assumption we make about the current object? Yes, we assume that the
``polar`` flag is set and that ``mag`` and ``theta`` contain valid data.
If that is not true, then this function will produce meaningless
results.

One option is to add a comment to the function that warns programmers
about the **precondition**.

::

   void Complex::calculateCartesian ()
   // precondition: the current object contains valid polar coordinates
       and the polar flag is set
   // postcondition: the current object will contain valid Cartesian
       coordinates and valid polar coordinates, and both the cartesian
       flag and the polar flag will be set
   {
     real = mag * cos (theta);
     imag = mag * sin (theta);
     cartesian = true;
   }

At the same time, I also commented on the **postconditions**, the things
we know will be true when the function completes.

These comments are useful for people reading your programs, but it is an
even better idea to add code that *checks* the preconditions, so that we
can print an appropriate error message:

::

   void Complex::calculateCartesian ()
   {
     if (polar == false) {
       cout <<
       "calculateCartesian failed because the polar representation is invalid"
        << endl;
       exit (1);
     }
     real = mag * cos (theta);
     imag = mag * sin (theta);
     cartesian = true;
   }

The ``exit`` function causes the program to quit immediately. The return
value is an error code that tells the system (or whoever executed the
program) that something went wrong.

This kind of error-checking is so common that C++ provides a built-in
function to check preconditions and print error messages. If you include
the ``assert.h`` header file, you get a function called ``assert`` that
takes a boolean value (or a conditional expression) as an argument. As
long as the argument is true, ``assert`` does nothing. If the argument
is false, assert prints an error message and quits. Here’s how to use
it:

::

   void Complex::calculateCartesian ()
   {
     assert (polar);
     real = mag * cos (theta);
     imag = mag * sin (theta);
     cartesian = true;
     assert (polar && cartesian);
   }

The first ``assert`` statement checks the precondition (actually just
part of it); the second ``assert`` statement checks the postcondition.

In my development environment, I get the following message when I
violate an assertion:

::

   Complex.cpp:63: void Complex::calculatePolar(): Assertion `cartesian' failed.
   Abort

There is a lot of information here to help me track down the error,
including the file name and line number of the assertion that failed,
the function name and the contents of the assert statement.