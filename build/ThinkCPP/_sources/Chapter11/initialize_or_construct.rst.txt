Initialize or construct?
------------------------

Earlier we declared and initialized some ``Time`` structures using
squiggly-braces:

::

     Time currentTime = { 9, 14, 30.0 };
     Time breadTime = { 3, 35, 0.0 };

Now, using constructors, we have a different way to declare and
initialize:

::

     Time time (seconds);

These two functions represent different programming styles, and
different points in the history of C++. Maybe for that reason, the C++
compiler requires that you use one or the other, and not both in the
same program.

If you define a constructor for a structure, then you have to use the
constructor to initialize all new structures of that type. The alternate
syntax using squiggly-braces is no longer allowed.

Fortunately, it is legal to overload constructors in the same way we
overloaded functions. In other words, there can be more than one
constructor with the same “name,” as long as they take different
parameters. Then, when we initialize a new object the compiler will try
to find a constructor that takes the appropriate parameters.

For example, it is common to have a constructor that takes one parameter
for each instance variable, and that assigns the values of the
parameters to the instance variables:

::

   Time::Time (int h, int m, double s)
   {
     hour = h;  minute = m;  second = s;
   }

To invoke this constructor, we use the same funny syntax as before,
except that the arguments have to be two integers and a ``double``:

::

     Time currentTime (9, 14, 30.0);

.. mchoice:: question11_8_1
   :multiple_answers:
   :answer_a: You can have many constructors with the same name.
   :answer_b: You can always initialize an object using squiggly-braces.
   :answer_c: When we initialize a new object, the compiler automatically finds the correct constructor to use.
   :answer_d: Once you define a constructor for a structure, you MUST use it to initialize any new structures of that type.
   :correct: b
   :feedback_a: Incorrect! This statement is true, as long as the constructors take different parameters.
   :feedback_b: Correct! Once you define a constructor, you can no longer use squiggly-braces to initialize an object.
   :feedback_c: Incorrect! This statement is true!
   :feedback_d: Incorrect! This statement is true!

   Which statement is **false** about constructors?