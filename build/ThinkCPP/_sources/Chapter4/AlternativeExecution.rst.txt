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


.. activecode:: fourthree
  :language: cpp
  :caption: Alternative execution within a function

  #include <iostream>
  using namespace std;

  void printParity (int x) {
    if (x%2 == 0) {
      cout << "x is even" << endl;
    } else {
      cout << "x is odd" << endl;
    }
  }

    int main ()
    {
    int number = 17;
    printParity(number);
    int otherNumber = 18;
    printParity(otherNumber);
    return 0;
    }
