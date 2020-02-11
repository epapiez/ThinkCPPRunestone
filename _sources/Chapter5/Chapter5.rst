Fruitful functions
==================

Return values
-------------

Some of the built-in functions we have used, like the math functions,
have produced results. That is, the effect of calling the function is to
generate a new value, which we usually assign to a variable or use as
part of an expression. For example:

::

      double e = exp (1.0);
      double height = radius * sin (angle);

But so far all the functions we have written have been **void**
functions; that is, functions that return no value. When you call a void
function, it is typically on a line by itself, with no assignment:

::

      nLines (3);
      countdown (n-1);

In this chapter, we are going to write functions that return things,
which I will refer to as **fruitful** functions, for want of a better
name. The first example is area, which takes a double as a parameter,
and returns the area of a circle with the given radius:

::

    double area (double radius) {
      double pi = acos (-1.0);
      double area = pi * radius * radius;
      return area;
    }

The first thing you should notice is that the beginning of the function
definition is different. Instead of void, which indicates a void
function, we see double, which indicates that the return value from this
function will have type double.

Also, notice that the last line is an alternate form of the return
statement that includes a return value. This statement means, “return
immediately from this function and use the following expression as a
return value.” The expression you provide can be arbitrarily
complicated, so we could have written this function more concisely:

::

    double area (double radius) {
      return acos(-1.0) * radius * radius;
    }

On the other hand, **temporary** variables like area often make
debugging easier. In either case, the type of the expression in the
return statement must match the return type of the function. In other
words, when you declare that the return type is double, you are making a
promise that this function will eventually produce a double. If you try
to return with no expression, or an expression with the wrong type, the
compiler will take you to task.

Sometimes it is useful to have multiple return statements, one in each
branch of a conditional:

::

    double absoluteValue (double x) {
      if (x < 0) {
        return -x;
      } else {
        return x;
      }
    }

Since these returns statements are in an alternative conditional, only
one will be executed. Although it is legal to have more than one return
statement in a function, you should keep in mind that as soon as one is
executed, the function terminates without executing any subsequent
statements.

Code that appears after a return statement, or any place else where it
can never be executed, is called **dead code**. Some compilers warn you
if part of your code is dead.

If you put return statements inside a conditional, then you have to
guarantee that *every possible path* through the program hits a return
statement. For example:

::

    double absoluteValue (double x) {
      if (x < 0) {
        return -x;
      } else if (x > 0) {
        return x;
      }                          // WRONG!!
    }

This program is not correct because if x happens to be 0, then neither
condition will be true and the function will end without hitting a
return statement. Unfortunately, many C++ compilers do not catch this
error. As a result, the program may compile and run, but the return
value when x==0 could be anything, and will probably be different in
different environments.

By now you are probably sick of seeing compiler errors, but as you gain
more experience, you will realize that the only thing worse than getting
a compiler error is *not* getting a compiler error when your program is
wrong.

Here’s the kind of thing that’s likely to happen: you test absoluteValue
with several values of x and it seems to work correctly. Then you give
your program to someone else and they run it in another environment. It
fails in some mysterious way, and it takes days of debugging to discover
that the problem is an incorrect implementation of absoluteValue. If
only the compiler had warned you!

From now on, if the compiler points out an error in your program, you
should not blame the compiler. Rather, you should thank the compiler for
finding your error and sparing you days of debugging. Some compilers
have an option that tells them to be extra strict and report all the
errors they can find. You should turn this option on all the time.

As an aside, you should know that there is a function in the math
library called fabs that calculates the absolute value of a
double—correctly.

.. _distance:

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

Composition
-----------

As you should expect by now, once you define a new function, you can use
it as part of an expression, and you can build new functions using
existing functions. For example, what if someone gave you two points,
the center of the circle and a point on the perimeter, and asked for the
area of the circle?

Let’s say the center point is stored in the variables xc and yc, and the
perimeter point is in xp and yp. The first step is to find the radius of
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

The name of this function is fred, which may seem odd. I will explain
why in the next section.

The temporary variables radius and area are useful for development and
debugging, but once the program is working we can make it more concise
by composing the function calls:

::

    double fred (double xc, double yc, double xp, double yp) {
      return area (distance (xc, yc, xp, yp));
    }

Overloading
-----------

In the previous section you might have noticed that fred and area
perform similar functions—finding the area of a circle—but take
different parameters. For area, we have to provide the radius; for fred
we provide two points.

If two functions do the same thing, it is natural to give them the same
name. In other words, it would make more sense if fred were called area.

Having more than one function with the same name, which is called
**overloading**, is legal in C++ *as long as each version takes
different parameters*. So we can go ahead and rename fred:

::

    double area (double xc, double yc, double xp, double yp) {
      return area (distance (xc, yc, xp, yp));
    }

This looks like a recursive function, but it is not. Actually, this
version of area is calling the other version. When you call an
overloaded function, C++ knows which version you want by looking at the
arguments that you provide. If you write:

::

        double x = area (3.0);

C++ goes looking for a function named area that takes a double as an
argument, and so it uses the first version. If you write

::

        double x = area (1.0, 2.0, 4.0, 6.0);

C++ uses the second version of area.

Many of the built-in C++ commands are overloaded, meaning that there are
different versions that accept different numbers or types of parameters.

Although overloading is a useful feature, it should be used with
caution. You might get yourself nicely confused if you are trying to
debug one version of a function while accidently calling a different
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

Boolean values
--------------

The types we have seen so far are pretty big. There are a lot of
integers in the world, and even more floating-point numbers. By
comparison, the set of characters is pretty small. Well, there is
another type in C++ that is even smaller. It is called **boolean**, and
the only values in it are true and false.

Without thinking about it, we have been using boolean values for the
last couple of chapters. The condition inside an if statement or a while
statement is a boolean expression. Also, the result of a comparison
operator is a boolean value. For example:

::

      if (x == 5) {
        // do something
      }

The operator == compares two integers and produces a boolean value.

The values true and false are keywords in C++, and can be used anywhere
a boolean expression is called for. For example,

::

      while (true) {
        // loop forever
      }

is a standard idiom for a loop that should run forever (or until it
reaches a return or break statement).

Boolean variables
-----------------

As usual, for every type of value, there is a corresponding type of
variable. In C++ the boolean type is called **bool**. Boolean variables
work just like the other types:

::

      bool fred;
      fred = true;
      bool testResult = false;

The first line is a simple variable declaration; the second line is an
assignment, and the third line is a combination of a declaration and as
assignment, called an initialization.

As I mentioned, the result of a comparison operator is a boolean, so you
can store it in a bool variable

::

      bool evenFlag = (n%2 == 0);     // true if n is even
      bool positiveFlag = (x > 0);    // true if x is positive

and then use it as part of a conditional statement later

::

      if (evenFlag) {
        cout << "n was even when I checked it" << endl;
      }

A variable used in this way is called a **flag**, since it flags the
presence or absence of some condition.

Logical operators
-----------------

There are three **logical operators** in C++: AND, OR and NOT, which are
denoted by the symbols &&, \|\| and !. The semantics (meaning) of these
operators is similar to their meaning in English. For example x > 0 && x
< 10 is true only if x is greater than zero AND less than 10.

evenFlag \|\| n%3 == 0 is true if *either* of the conditions is true,
that is, if evenFlag is true OR the number is divisible by 3.

Finally, the NOT operator has the effect of negating or inverting a bool
expression, so !evenFlag is true if evenFlag is false; that is, if the
number is odd.

Logical operators often provide a way to simplify nested conditional
statements. For example, how would you write the following code using a
single conditional?

::

      if (x > 0) {
        if (x < 10) {
          cout << "x is a positive single digit." << endl;
        }
      }

.. _bool:

Bool functions
--------------

Functions can return bool values just like any other type, which is
often convenient for hiding complicated tests inside functions. For
example:

::

    bool isSingleDigit (int x)
    {
      if (x >= 0 && x < 10) {
        return true;
      } else {
        return false;
      }
    }

The name of this function is isSingleDigit. It is common to give boolean
functions names that sound like yes/no questions. The return type is
bool, which means that every return statement has to provide a bool
expression.

The code itself is straightforward, although it is a bit longer than it
needs to be. Remember that the expression x >= 0 && x < 10 has type
bool, so there is nothing wrong with returning it directly, and avoiding
the if statement altogether:

::

    bool isSingleDigit (int x)
    {
      return (x >= 0 && x < 10);
    }

In main you can call this function in the usual ways:

::

      cout << isSingleDigit (2) << endl;
      bool bigFlag = !isSingleDigit (17);

The first line outputs the value true because 2 is a single-digit
number. Unfortunately, when C++ outputs bools, it does not display the
words true and false, but rather the integers 1 and 0. [1]_

The second line assigns the value true to bigFlag only if 17 is *not* a
single-digit number.

The most common use of bool functions is inside conditional statements

::

      if (isSingleDigit (x)) {
        cout << "x is little" << endl;
      } else {
        cout << "x is big" << endl;
      }

Returning from main
-------------------

Now that we have functions that return values, I can let you in on a
secret. main is not really supposed to be a void function. It’s supposed
to return an integer:

::

    int main ()
    {
      return 0;
    }

The usual return value from main is 0, which indicates that the program
succeeded at whatever it was supposed to to. If something goes wrong, it
is common to return -1, or some other value that indicates what kind of
error occurred.

Of course, you might wonder who this value gets returned to, since we
never call main ourselves. It turns out that when the system executes a
program, it starts by calling main in pretty much the same way it calls
all the other functions.

There are even some parameters that are passed to main by the system,
but we are not going to deal with them for a little while.

More recursion
--------------

So far we have only learned a small subset of C++, but you might be
interested to know that this subset is now a **complete** programming
language, by which I mean that anything that can be computed can be
expressed in this language. Any program ever written could be rewritten
using only the language features we have used so far (actually, we would
need a few commands to control devices like the keyboard, mouse, disks,
etc., but that’s all).

Proving that claim is a non-trivial exercise first accomplished by Alan
Turing, one of the first computer scientists (well, some would argue
that he was a mathematician, but a lot of the early computer scientists
started as mathematicians). Accordingly, it is known as the Turing
thesis. If you take a course on the Theory of Computation, you will have
a chance to see the proof.

To give you an idea of what you can do with the tools we have learned so
far, we’ll evaluate a few recursively-defined mathematical functions. A
recursive definition is similar to a circular definition, in the sense
that the definition contains a reference to the thing being defined. A
truly circular definition is typically not very useful:

frabjuous:
    an adjective used to describe something that is frabjuous.

If you saw that definition in the dictionary, you might be annoyed. On
the other hand, if you looked up the definition of the mathematical
function **factorial**, you might get something like:

.. math::

   \begin{aligned}
   &&  0! = 1 \\
   &&  n! = n \cdot (n-1)!\end{aligned}

(Factorial is usually denoted with the symbol :math:`!`, which is not to
be confused with the C++ logical operator ! which means NOT.) This
definition says that the factorial of 0 is 1, and the factorial of any
other value, :math:`n`, is :math:`n` multiplied by the factorial of
:math:`n-1`. So :math:`3!` is 3 times :math:`2!`, which is 2 times
:math:`1!`, which is 1 times 0!. Putting it all together, we get
:math:`3!` equal to 3 times 2 times 1 times 1, which is 6.

If you can write a recursive definition of something, you can usually
write a C++ program to evaluate it. The first step is to decide what the
parameters are for this function, and what the return type is. With a
little thought, you should conclude that factorial takes an integer as a
parameter and returns an integer:

::

    int factorial (int n)
    {
    }

If the argument happens to be zero, all we have to do is return 1:

::

    int factorial (int n)
    {
      if (n == 0) {
        return 1;
      }
    }

Otherwise, and this is the interesting part, we have to make a recursive
call to find the factorial of :math:`n-1`, and then multiply it by
:math:`n`.

::

    int factorial (int n)
    {
      if (n == 0) {
        return 1;
      } else {
        int recurse = factorial (n-1);
        int result = n * recurse;
        return result;
      }
    }

If we look at the flow of execution for this program, it is similar to
nLines from the previous chapter. If we call factorial with the value 3:

Since 3 is not zero, we take the second branch and calculate the
factorial of :math:`n-1`...

    Since 2 is not zero, we take the second branch and calculate the
    factorial of :math:`n-1`...

        Since 1 is not zero, we take the second branch and calculate the
        factorial of :math:`n-1`...

            Since 0 *is* zero, we take the first branch and return the
            value 1 immediately without making any more recursive calls.

        The return value (1) gets multiplied by n, which is 1, and the
        result is returned.

    The return value (1) gets multiplied by n, which is 2, and the
    result is returned.

The return value (2) gets multiplied by n, which is 3, and the result,
6, is returned to main, or whoever called factorial (3).

Here is what the stack diagram looks like for this sequence of function
calls:

.. raw:: latex

   \vspace{0.1in}

.. raw:: latex

   \vspace{0.1in}

The return values are shown being passed back up the stack.

Notice that in the last instance of factorial, the local variables
recurse and result do not exist because when n=0 the branch that creates
them does not execute.

Leap of faith
-------------

Following the flow of execution is one way to read programs, but as you
saw in the previous section, it can quickly become labarynthine. An
alternative is what I call the “leap of faith.” When you come to a
function call, instead of following the flow of execution, you *assume*
that the function works correctly and returns the appropriate value.

In fact, you are already practicing this leap of faith when you use
built-in functions. When you call cos or exp, you don’t examine the
implementations of those functions. You just assume that they work,
because the people who wrote the built-in libraries were good
programmers.

Well, the same is true when you call one of your own functions. For
example, in Section \ `8 <#bool>`__ we wrote a function called
isSingleDigit that determines whether a number is between 0 and 9. Once
we have convinced ourselves that this function is correct—by testing and
examination of the code—we can use the function without ever looking at
the code again.

The same is true of recursive programs. When you get to the recursive
call, instead of following the flow of execution, you should *assume*
that the recursive call works (yields the correct result), and then ask
yourself, “Assuming that I can find the factorial of :math:`n-1`, can I
compute the factorial of :math:`n`?” In this case, it is clear that you
can, by multiplying by :math:`n`.

Of course, it is a bit strange to assume that the function works
correctly when you have not even finished writing it, but that’s why
it’s called a leap of faith!

One more example
----------------

In the previous example I used temporary variables to spell out the
steps, and to make the code easier to debug, but I could have saved a
few lines:

::

    int factorial (int n) {
      if (n == 0) {
        return 1;
      } else {
        return n * factorial (n-1);
      }
    }

From now on I will tend to use the more concise version, but I recommend
that you use the more explicit version while you are developing code.
When you have it working, you can tighten it up, if you are feeling
inspired.

After factorial, the classic example of a recursively-defined
mathematical function is fibonacci, which has the following definition:

.. math::

   \begin{aligned}
   && fibonacci(0) = 1 \\
   && fibonacci(1) = 1 \\
   && fibonacci(n) = fibonacci(n-1) + fibonacci(n-2);\end{aligned}

Translated into C++, this is

::

    int fibonacci (int n) {
      if (n == 0 || n == 1) {
        return 1;
      } else {
        return fibonacci (n-1) + fibonacci (n-2);
      }
    }

If you try to follow the flow of execution here, even for fairly small
values of n, your head explodes. But according to the leap of faith, if
we assume that the two recursive calls (yes, you can make two recursive
calls) work correctly, then it is clear that we get the right result by
adding them together.

Glossary
--------

return type:
    The type of value a function returns.

return value:
    The value provided as the result of a function call.

dead code:
    Part of a program that can never be executed, often because it
    appears after a return statement.

scaffolding:
    Code that is used during program development but is not part of the
    final version.

void:
    A special return type that indicates a void function; that is, one
    that does not return a value.

overloading:
    Having more than one function with the same name but different
    parameters. When you call an overloaded function, C++ knows which
    version to use by looking at the arguments you provide.

boolean:
    A value or variable that can take on one of two states, often called
    :math:`true` and :math:`false`. In C++, boolean values can be stored
    in a variable type called bool.

flag:
    A variable (usually type bool) that records a condition or status
    information.

comparison operator:
    An operator that compares two values and produces a boolean that
    indicates the relationship between the operands.

logical operator:
    An operator that combines boolean values in order to test compound
    conditions.

.. [1]
   There is a way to fix that using the boolalpha flag, but it is too
   hideous to mention.
