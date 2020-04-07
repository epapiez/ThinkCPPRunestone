``print``
---------

In Chapter `[time] <#time>`__ we defined a structure named ``Time`` and
wrote a function named ``printTime``

::

   struct Time {
     int hour, minute;
     double second;
   };

   void printTime (const Time& time) {
     cout << time.hour << ":" << time.minute << ":" << time.second << endl;
   }

To call this function, we had to pass a ``Time`` object as a parameter.

::

     Time currentTime = { 9, 14, 30.0 };
     printTime (currentTime);

To make ``printTime`` into a member function, the first step is to
change the name of the function from ``printTime`` to ``Time::print``.
The ``::`` operator separates the name of the structure from the name of
the function; together they indicate that this is a function named
``print`` that can be invoked on a ``Time`` structure.

The next step is to eliminate the parameter. Instead of passing an
object as an argument, we are going to invoke the function on an object.

As a result, inside the function, we no longer have a parameter named
``time``. Instead, we have a **current object**, which is the object the
function is invoked on. We can refer to the current object using the C++
keyword ``this``.

One thing that makes life a little difficult is that ``this`` is
actually a **pointer** to a structure, rather than a structure itself. A
pointer is similar to a reference, but I don’t want to go into the
details of using pointers yet. The only pointer operation we need for
now is the ```` operator, which converts a structure pointer into a
structure. In the following function, we use it to assign the value of
``this`` to a local variable named ``time``:

::

   void Time::print () {
     Time time = *this;
     cout << time.hour << ":" << time.minute << ":" << time.second << endl;
   }

The first two lines of this function changed quite a bit as we
transformed it into a member function, but notice that the output
statement itself did not change at all.

In order to invoke the new version of ``print``, we have to invoke it on
a ``Time`` object:

::

     Time currentTime = { 9, 14, 30.0 };
     currentTime.print ();

The last step of the transformation process is that we have to declare
the new function inside the structure definition:

::

   struct Time {
     int hour, minute;
     double second;

     void Time::print ();
   };

A **function declaration** looks just like the first line of the
function definition, except that it has a semi-colon at the end. The
declaration describes the **interface** of the function; that is, the
number and types of the arguments, and the type of the return value.

When you declare a function, you are making a promise to the compiler
that you will, at some point later on in the program, provide a
definition for the function. This definition is sometimes called the
**implementation** of the function, since it contains the details of how
the function works. If you omit the definition, or provide a definition
that has an interface different from what you promised, the compiler
will complain.
