Member functions
================

Objects and functions
---------------------

C++ is generally considered an object-oriented programming language,
which means that it provides features that support object-oriented
programming.

It’s not easy to define object-oriented programming, but we have already
seen some features of it:

#. Programs are made up of a collection of structure definitions and
   function definitions, where most of the functions operate on specific
   kinds of structures (or objecs).

#. Each structure definition corresponds to some object or concept in
   the real world, and the functions that operate on that structure
   correspond to the ways real-world objects interact.

For example, the ``Time`` structure we defined in
Chapter `[time] <#time>`__ obviously corresponds to the way people
record the time of day, and the operations we defined correspond to the
sorts of things people do with recorded times. Similarly, the ``Point``
and ``Rectangle`` structures correspond to the mathematical concept of a
point and a rectangle.

So far, though, we have not taken advantage of the features C++ provides
to support object-oriented programming. Strictly speaking, these
features are not necessary. For the most part they provide an alternate
syntax for doing things we have already done, but in many cases the
alternate syntax is more concise and more accurately conveys the
structure of the program.

For example, in the ``Time`` program, there is no obvious connection
between the structure definition and the function definitions that
follow. With some examination, it is apparent that every function takes
at least one ``Time`` structure as a parameter.

This observation is the motivation for **member functions**. Member
function differ from the other functions we have written in two ways:

#. When we call the function, we **invoke** it on an object, rather than
   just call it. People sometimes describe this process as “performing
   an operation on an object,” or “sending a message to an object.”

#. The function is *declared* inside the ``struct`` definition, in order
   to make the relationship between the structure and the function
   explicit.

In the next few sections, we will take the functions from
Chapter `[time] <#time>`__ and transform them into member functions. One
thing you should realize is that this transformation is purely
mechanical; in other words, you can do it just by following a sequence
of steps.

As I said, anything that can be done with a member function can also be
done with a nonmember function (sometimes called a **free-standing**
function). But sometimes there is an advantage to one over the other. If
you are comfortable converting from one form to another, you will be
able to choose the best form for whatever you are doing.

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

Implicit variable access
------------------------

Actually, the new version of ``Time::print`` is more complicated than it
needs to be. We don’t really need to create a local variable in order to
refer to the instance variables of the current object.

If the function refers to ``hour``, ``minute``, or ``second``, all by
themselves with no dot notation, C++ knows that it must be referring to
the current object. So we could have written:

::

   void Time::print ()
   {
     cout << hour << ":" << minute << ":" << second << endl;
   }

This kind of variable access is called “implicit” because the name of
the object does not appear explicitly. Features like this are one reason
member functions are often more concise than nonmember functions.

Another example
---------------

Let’s convert ``increment`` to a member function. Again, we are going to
transform one of the parameters into the implicit parameter called
``this``. Then we can go through the function and make all the variable
accesses implicit.

::

   void Time::increment (double secs) {
     second += secs;

     while (second >= 60.0) {
       second -= 60.0;
       minute += 1;
     }
     while (minute >= 60) {
       minute -= 60.0;
       hour += 1;
     }
   }

By the way, remember that this is not the most efficient implementation
of this function. If you didn’t do it back in
Chapter `[time] <#time>`__, you should write a more efficient version
now.

To declare the function, we can just copy the first line into the
structure definition:

::

   struct Time {
     int hour, minute;
     double second;

     void Time::print ();
     void Time::increment (double secs);
   };

And again, to call it, we have to invoke it on a ``Time`` object:

::

     Time currentTime = { 9, 14, 30.0 };
     currentTime.increment (500.0);
     currentTime.print ();

The output of this program is ``9:22:50``.

Yet another example
-------------------

The original version of ``convertToSeconds`` looked like this:

::

   double convertToSeconds (const Time& time) {
     int minutes = time.hour * 60 + time.minute;
     double seconds = minutes * 60 + time.second;
     return seconds;
   }

It is straightforward to convert this to a member function:

::

   double Time::convertToSeconds () const {
     int minutes = hour * 60 + minute;
     double seconds = minutes * 60 + second;
     return seconds;
   }

The interesting thing here is that the implicit parameter should be
declared ``const``, since we don’t modify it in this function. But it is
not obvious where we should put information about a parameter that
doesn’t exist. The answer, as you can see in the example, is after the
parameter list (which is empty in this case).

The ``print`` function in the previous section should also declare that
the implicit parameter is ``const``.

A more complicated example
--------------------------

Although the process of transforming functions into member functions is
mechanical, there are some oddities. For example, ``after`` operates on
two ``Time`` structures, not just one, and we can’t make both of them
implicit. Instead, we have to invoke the function on one of them and
pass the other as an argument.

Inside the function, we can refer to one of the them implicitly, but to
access the instance variables of the other we continue to use dot
notation.

::

   bool Time::after (const Time& time2) const {
     if (hour > time2.hour) return true;
     if (hour < time2.hour) return false;

     if (minute > time2.minute) return true;
     if (minute < time2.minute) return false;

     if (second > time2.second) return true;
     return false;
   }

To invoke this function:

::

     if (doneTime.after (currentTime)) {
       cout << "The bread will be done after it starts." << endl;
     }

You can almost read the invocation like English: “If the done-time is
after the current-time, then...”

Constructors
------------

Another function we wrote in Chapter `[time] <#time>`__ was
``makeTime``:

::

   Time makeTime (double secs) {
     Time time;
     time.hour = int (secs / 3600.0);
     secs -= time.hour * 3600.0;
     time.minute = int (secs / 60.0);
     secs -= time.minute * 60.0;
     time.second = secs;
     return time;
   }

Of course, for every new type, we need to be able to create new objects.
In fact, functions like ``makeTime`` are so common that there is a
special function syntax for them. These functions are called
**constructors** and the syntax looks like this:

::

   Time::Time (double secs) {
     hour = int (secs / 3600.0);
     secs -= hour * 3600.0;
     minute = int (secs / 60.0);
     secs -= minute * 60.0;
     second = secs;
   }

First, notice that the constructor has the same name as the class, and
no return type. The arguments haven’t changed, though.

Second, notice that we don’t have to create a new time object, and we
don’t have to return anything. Both of these steps are handled
automatically. We can refer to the new object—the one we are
constructing—using the keyword ``this``, or implicitly as shown here.
When we write values to ``hour``, ``minute`` and ``second``, the
compiler knows we are referring to the instance variables of the new
object.

To invoke the constructor, you use syntax that is a cross between a
variable declaration and a function call:

::

     Time time (seconds);

This statement declares that the variable ``time`` has type ``Time``,
and it invokes the constructor we just wrote, passing the value of
``seconds`` as an argument. The system allocates space for the new
object and the constructor initializes its instance variables. The
result is assigned to the variable ``time``.

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

One last example
----------------

The final example we’ll look at is ``addTime``:

::

   Time addTime2 (const Time& t1, const Time& t2) {
     double seconds = convertToSeconds (t1) + convertToSeconds (t2);
     return makeTime (seconds);
   }

We have to make several changes to this function, including:

#. Change the name from ``addTime`` to ``Time::add``.

#. Replace the first parameter with an implicit parameter, which should
   be declared ``const``.

#. Replace the use of ``makeTime`` with a constructor invocation.

Here’s the result:

::

   Time Time::add (const Time& t2) const {
     double seconds = convertToSeconds () + t2.convertToSeconds ();
     Time time (seconds);
     return time;
   }

The first time we invoke ``convertToSeconds``, there is no apparent
object! Inside a member function, the compiler assumes that we want to
invoke the function on the current object. Thus, the first invocation
acts on ``this``; the second invocation acts on ``t2``.

The next line of the function invokes the constructor that takes a
single ``double`` as a parameter; the last line returns the resulting
object.

Header files
------------

It might seem like a nuisance to declare functions inside the structure
definition and then define the functions later. Any time you change the
interface to a function, you have to change it in two places, even if it
is a small change like declaring one of the parameters ``const``.

There is a reason for the hassle, though, which is that it is now
possible to separate the structure definition and the functions into two
files: the **header file**, which contains the structure definition, and
the implementation file, which contains the functions.

Header files usually have the same name as the implementation file, but
with the suffix ``.h`` instead of ``.cpp``. For the example we have been
looking at, the header file is called ``Time.h``, and it contains the
following:

::

   struct Time {
     // instance variables
     int hour, minute;
     double second;

     // constructors
     Time (int hour, int min, double secs);
     Time (double secs);

     // modifiers
     void increment (double secs);

     // functions
     void print () const;
     bool after (const Time& time2) const;
     Time add (const Time& t2) const;
     double convertToSeconds () const;
   };

Notice that in the structure definition I don’t really have to include
the prefix ``Time::`` at the beginning of every function name. The
compiler knows that we are declaring functions that are members of the
``Time`` structure.

``Time.cpp`` contains the definitions of the member functions (I have
elided the function bodies to save space):

::

   #include <iostream>
   using namespace std;
   #include "Time.h"

   Time::Time (int h, int m, double s)  ...

   Time::Time (double secs) ...

   void Time::increment (double secs) ...

   void Time::print () const ...

   bool Time::after (const Time& time2) const ...

   Time Time::add (const Time& t2) const ...

   double Time::convertToSeconds () const ...

In this case the definitions in ``Time.cpp`` appear in the same order as
the declarations in ``Time.h``, although it is not necessary.

On the other hand, it is necessary to include the header file using an
``include`` statement. That way, while the compiler is reading the
function definitions, it knows enough about the structure to check the
code and catch errors.

Finally, ``main.cpp`` contains the function ``main`` along with any
functions we want that are not members of the ``Time`` structure (in
this case there are none):

::

   #include <iostream>
   using namespace std;
   #include "Time.h"

   int main ()
   {
     Time currentTime (9, 14, 30.0);
     currentTime.increment (500.0);
     currentTime.print ();

     Time breadTime (3, 35, 0.0);
     Time doneTime = currentTime.add (breadTime);
     doneTime.print ();

     if (doneTime.after (currentTime)) {
       cout << "The bread will be done after it starts." << endl;
     }
     return 0;
   }

Again, ``main.cpp`` has to include the header file.

It may not be obvious why it is useful to break such a small program
into three pieces. In fact, most of the advantages come when we are
working with larger programs:

Reuse:
   Once you have written a structure like ``Time``, you might find it
   useful in more than one program. By separating the definition of
   ``Time`` from ``main.cpp``, you make is easy to include the ``Time``
   structure in another program.

Managing interactions:
   As systems become large, the number of interactions between
   components grows and quickly becomes unmanageable. It is often useful
   to minimize these interactions by separating modules like
   ``Time.cpp`` from the programs that use them.

Separate compilation:
   Separate files can be compiled separately and then linked into a
   single program later. The details of how to do this depend on your
   programming environment. As the program gets large, separate
   compilation can save a lot of time, since you usually need to compile
   only a few files at a time.

For small programs like the ones in this book, there is no great
advantage to splitting up programs. But it is good for you to know about
this feature, especially since it explains one of the statements that
appeared in the first program we wrote:

::

   #include <iostream>
   using namespace std;

``iostream`` is the header file that contains declarations for ``cin``
and ``cout`` and the functions that operate on them. When you compile
your program, you need the information in that header file.

The implementations of those functions are stored in a library,
sometimes called the “Standard Library” that gets linked to your program
automatically. The nice thing is that you don’t have to recompile the
library every time you compile a program. For the most part the library
doesn’t change, so there is no reason to recompile it.

Glossary
--------

member function:
   A function that operates on an object that is passed as an implicit
   parameter named ``this``.

nonmember function:
   A function that is not a member of any structure definition. Also
   called a “free-standing” function.

invoke:
   To call a function “on” an object, in order to pass the object as an
   implicit parameter.

current object:
   The object on which a member function is invoked. Inside the member
   function, we can refer to the current object implicitly, or by using
   the keyword ``this``.

this:
   A keyword that refers to the current object. ``this`` is a pointer,
   which makes it difficult to use, since we do not cover pointers in
   this book.

interface:
   A description of how a function is used, including the number and
   types of the parameters and the type of the return value.

function declaration:
   A statement that declares the interface to a function without
   providing the body. Declarations of member functions appear inside
   structure definitions even if the definitions appear outside.

implementation:
   The body of a function, or the details of how a function works.

constructor:
   A special function that initializes the instance variables of a
   newly-created object.
