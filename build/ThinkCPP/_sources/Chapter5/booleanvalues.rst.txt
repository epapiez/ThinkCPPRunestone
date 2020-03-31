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
