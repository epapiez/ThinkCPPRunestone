Parameters and arguments
------------------------

Some of the built-in functions we have used have **parameters**, which
are values that you provide to let the function do its job. For example,
if you want to find the sine of a number, you have to indicate what the
number is. Thus, sin takes a double value as a parameter.

Some functions take more than one parameter, like pow, which takes two
doubles, the base and the exponent.

Notice that in each of these cases we have to specify not only how many
parameters there are, but also what type they are. So it shouldn’t
surprise you that when you write a class definition, the parameter list
indicates the type of each parameter. For example:

::

      void printTwice (char phil) {
        cout << phil << phil << endl;
      }

This function takes a single parameter, named phil, that has type char.
Whatever that parameter is (and at this point we have no idea what it
is), it gets printed twice, followed by a newline. I chose the name phil
to suggest that the name you give a parameter is up to you, but in
general you want to choose something more illustrative than phil.

In order to call this function, we have to provide a char. For example,
we might have a main function like this:

::

      int main () {
        printTwice ('a');
        return 0;
      }

The char value you provide is called an **argument**, and we say that
the argument is **passed** to the function. In this case the value ’a’
is passed as an argument to printTwice where it will get printed twice.

Alternatively, if we had a char variable, we could use it as an argument
instead:

::

      int main () {
        char argument = 'b';
        printTwice (argument);
        return 0;
      }

Notice something very important here: the name of the variable we pass
as an argument (argument) has nothing to do with the name of the
parameter (phil). Let me say that again:

    **The name of the variable we pass as an argument has nothing to do
    with the name of the parameter.**

They can be the same or they can be different, but it is important to
realize that they are not the same thing, except that they happen to
have the same value (in this case the character ’b’).

The value you provide as an argument must have the same type as the
parameter of the function you call. This rule is important, but it is
sometimes confusing because C++ sometimes converts arguments from one
type to another automatically. For now you should learn the general
rule, and we will deal with exceptions later.


.. activecode:: threeeight
  :language: cpp
  :caption: Understanding parameters.

  #include <iostream>
  using namespace std;

  void printTwice (char phil) {
    cout << phil << phil << endl;
  }

  int main () {
    char argument = 'b';
    printTwice (argument);
    return 0;
  }

.. mchoice:: test_question_three_two
   :practice: T
   :answer_a: 1
   :answer_b: 2
   :answer_c: 3
   :correct: b
   :feedback_a: There is only one "endl", implying that only one new line is created.
   :feedback_b: Yes, the "endl" creates one new line. The first line will say "o", while the second will print "oo"
   :feedback_c: In C++, you must make sure to say "endl" every time you'd like to create a new line.


   On how many separate lines will the "o"'s be printed?

   .. code-block:: cpp
    #include <iostream>
    using namespace std;

    void printTwice (char phil) {
      cout << phil << phil << endl;
    }

    int main () {
      char argument = 'b';
      printTwice (argument);
      return 0;
    }
