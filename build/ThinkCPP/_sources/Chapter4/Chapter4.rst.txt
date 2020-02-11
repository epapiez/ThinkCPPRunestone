.. _condrecursion:

Conditionals and recursion
==========================

The modulus operator
--------------------

The modulus operator works on integers (and integer expressions) and
yields the *remainder* when the first operand is divided by the second.
In C++, the modulus operator is a percent sign, %. The syntax is exactly
the same as for other operators:

::

      int quotient = 7 / 3;
      int remainder = 7 % 3;

The first operator, integer division, yields 2. The second operator
yields 1. Thus, 7 divided by 3 is 2 with 1 left over.

The modulus operator turns out to be surprisingly useful. For example,
you can check whether one number is divisible by another: if x % y is
zero, then x is divisible by y.

Also, you can use the modulus operator to extract the rightmost digit or
digits from a number. For example, x % 10 yields the rightmost digit of
x (in base 10). Similarly x % 100 yields the last two digits.

Conditional execution
---------------------

In order to write useful programs, we almost always need the ability to
check certain conditions and change the behavior of the program
accordingly. **Conditional statements** give us this ability. The
simplest form is the if statement:

::

      if (x > 0) {
        cout << "x is positive" << endl;
      }

The expression in parentheses is called the condition. If it is true,
then the statements in brackets get executed. If the condition is not
true, nothing happens.

The condition can contain any of the comparison operators:

::

        x == y               // x equals y
        x != y               // x is not equal to y
        x > y                // x is greater than y
        x < y                // x is less than y
        x >= y               // x is greater than or equal to y
        x <= y               // x is less than or equal to y

Although these operations are probably familiar to you, the syntax C++
uses is a little different from mathematical symbols like :math:`=`,
:math:`\neq` and :math:`\le`. A common error is to use a single =
instead of a double ==. Remember that = is the assignment operator, and
== is a comparison operator. Also, there is no such thing as =< or =>.

The two sides of a condition operator have to be the same type. You can
only compare ints to ints and doubles to doubles. Unfortunately, at this
point you can’t compare Strings at all! There is a way to compare
Strings, but we won’t get to it for a couple of chapters.

.. _alternative:

Alternative execution
---------------------

A second form of conditional execution is alternative execution, in
which there are two possibilities, and the condition determines which
one gets executed. The syntax looks like:

::

      if (x%2 == 0) {
        cout << "x is even" << endl;
      } else {
        cout << "x is odd" << endl;
      }

If the remainder when x is divided by 2 is zero, then we know that x is
even, and this code displays a message to that effect. If the condition
is false, the second set of statements is executed. Since the condition
must be true or false, exactly one of the alternatives will be executed.

As an aside, if you think you might want to check the parity (evenness
or oddness) of numbers often, you might want to “wrap” this code up in a
function, as follows:

::

    void printParity (int x) {
      if (x%2 == 0) {
        cout << "x is even" << endl;
      } else {
        cout << "x is odd" << endl;
      }
    }

Now you have a function named printParity that will display an
appropriate message for any integer you care to provide. In main you
would call this function as follows:

::

        printParity (17);

Always remember that when you *call* a function, you do not have to
declare the types of the arguments you provide. C++ can figure out what
type they are. You should resist the temptation to write things like:

::

      int number = 17;
      printParity (int number);         // WRONG!!!

Chained conditionals
--------------------

Sometimes you want to check for a number of related conditions and
choose one of several actions. One way to do this is by **chaining** a
series of ifs and elses:

::

      if (x > 0) {
        cout << "x is positive" << endl;
      } else if (x < 0) {
        cout << "x is negative" << endl;
      } else {
        cout << "x is zero" << endl;
      }

These chains can be as long as you want, although they can be difficult
to read if they get out of hand. One way to make them easier to read is
to use standard indentation, as demonstrated in these examples. If you
keep all the statements and squiggly-braces lined up, you are less
likely to make syntax errors and you can find them more quickly if you
do.

Nested conditionals
-------------------

In addition to chaining, you can also nest one conditional within
another. We could have written the previous example as:

::

      if (x == 0) {
        cout << "x is zero" << endl;
      } else {
        if (x > 0) {
          cout << "x is positive" << endl;
        } else {
          cout << "x is negative" << endl;
        }
      }

There is now an outer conditional that contains two branches. The first
branch contains a simple output statement, but the second branch
contains another if statement, which has two branches of its own.
Fortunately, those two branches are both output statements, although
they could have been conditional statements as well.

Notice again that indentation helps make the structure apparent, but
nevertheless, nested conditionals get difficult to read very quickly. In
general, it is a good idea to avoid them when you can.

On the other hand, this kind of **nested structure** is common, and we
will see it again, so you better get used to it.

The return statement
--------------------

The return statement allows you to terminate the execution of a function
before you reach the end. One reason to use it is if you detect an error
condition:

::

    #include <cmath>

    void printLogarithm (double x) {
      if (x <= 0.0) {
        cout << "Positive numbers only, please." << endl;
        return;
      }

      double result = log (x);
      cout << "The log of x is " << result;
    }

This defines a function named printLogarithm that takes a double named x
as a parameter. The first thing it does is check whether x is less than
or equal to zero, in which case it displays an error message and then
uses return to exit the function. The flow of execution immediately
returns to the caller and the remaining lines of the function are not
executed.

I used a floating-point value on the right side of the condition because
there is a floating-point variable on the left.

Remember that any time you want to use one a function from the math
library, you have to include the header file math.h.

Recursion
---------

I mentioned in the last chapter that it is legal for one function to
call another, and we have seen several examples of that. I neglected to
mention that it is also legal for a function to call itself. It may not
be obvious why that is a good thing, but it turns out to be one of the
most magical and interesting things a program can do.

For example, look at the following function:

::

    void countdown (int n) {
      if (n == 0) {
        cout << "Blastoff!" << endl;
      } else {
        cout << n << endl;
        countdown (n-1);
      }
    }

The name of the function is countdown and it takes a single integer as a
parameter. If the parameter is zero, it outputs the word “Blastoff.”
Otherwise, it outputs the parameter and then calls a function named
countdown—itself—passing n-1 as an argument.

What happens if we call this function like this:

::

    #include <iostream>
    #include <cmath>
    using namespace std;
    void printLogarithm (double x) {
      if (x <= 0.0) {
        cout << "Positive numbers only, please." << endl;
        return;
      }

      double result = log (x);
      cout << "The log of x is " << result;
    }

    void countdown (int n) {
      if (n == 0) {
        cout << "Blastoff!" << endl;
      } else {
        cout << n << endl;
        countdown (n-1);
      }
    }

    int main ()
    {
      countdown (3);
      return 0;
    }

The execution of countdown begins with n=3, and since n is not zero, it
outputs the value 3, and then calls itself...

    The execution of countdown begins with n=2, and since n is not zero,
    it outputs the value 2, and then calls itself...

        The execution of countdown begins with n=1, and since n is not
        zero, it outputs the value 1, and then calls itself...

            The execution of countdown begins with n=0, and since n is
            zero, it outputs the word “Blastoff!” and then returns.

        The countdown that got n=1 returns.

    The countdown that got n=2 returns.

The countdown that got n=3 returns.

And then you’re back in main (what a trip). So the total output looks
like:

::

    3
    2
    1
    Blastoff!

As a second example, let’s look again at the functions newLine and
threeLine.

::

    void newLine () {
      cout << endl;
    }

    void threeLine () {
      newLine ();  newLine ();  newLine ();
    }

Although these work, they would not be much help if I wanted to output 2
newlines, or 106. A better alternative would be

::

    void nLines (int n) {
      if (n > 0) {
        cout << endl;
        nLines (n-1);
      }
    }

This program is similar to countdown; as long as n is greater than zero,
it outputs one newline, and then calls itself to output n-1 additional
newlines. Thus, the total number of newlines is 1 + (n-1), which usually
comes out to roughly n.

The process of a function calling itself is called **recursion**, and
such functions are said to be **recursive**.

Infinite recursion
------------------

In the examples in the previous section, notice that each time the
functions get called recursively, the argument gets smaller by one, so
eventually it gets to zero. When the argument is zero, the function
returns immediately, *without making any recursive calls*. This
case—when the function completes without making a recursive call—is
called the **base case**.

If a recursion never reaches a base case, it will go on making recursive
calls forever and the program will never terminate. This is known as
**infinite recursion**, and it is generally not considered a good idea.

In most programming environments, a program with an infinite recursion
will not really run forever. Eventually, something will break and the
program will report an error. This is the first example we have seen of
a run-time error (an error that does not appear until you run the
program).

You should write a small program that recurses forever and run it to see
what happens.

Stack diagrams for recursive functions
--------------------------------------

In the previous chapter we used a stack diagram to represent the state
of a program during a function call. The same kind of diagram can make
it easier to interpret a recursive function.

Remember that every time a function gets called it creates a new
instance that contains the function’s local variables and parameters.

This figure shows a stack diagram for countdown, called with n = 3:





There is one instance of main and four instances of countdown, each with
a different value for the parameter n. The bottom of the stack,
countdown with n=0 is the base case. It does not make a recursive call,
so there are no more instances of countdown.

The instance of main is empty because main does not have any parameters
or local variables. As an exercise, draw a stack diagram for nLines,
invoked with the parameter n=4.

Glossary
--------

modulus:
    An operator that works on integers and yields the remainder when one
    number is divided by another. In C++ it is denoted with a percent
    sign (%).

conditional:
    A block of statements that may or may not be executed depending on
    some condition.

chaining:
    A way of joining several conditional statements in sequence.

nesting:
    Putting a conditional statement inside one or both branches of
    another conditional statement.

recursion:
    The process of calling the same function you are currently
    executing.

infinite recursion:
    A function that calls itself recursively without every reaching the
    base case. Eventually an infinite recursion will cause a run-time
    error.
