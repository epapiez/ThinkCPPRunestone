Parameters and variables are local
----------------------------------

Parameters and variables only exist inside their own functions. Within
the confines of main, there is no such thing as phil. If you try to use
it, the compiler will complain. Similarly, inside printTwice there is no
such thing as argument.

.. activecode:: threenine
  :language: cpp
  :caption: Understanding parameters from previous section.

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

Variables like this are said to be **local**. In order to keep track of
parameters and local variables, it is useful to draw a **stack
diagram**. Like state diagrams, stack diagrams show the value of each
variable, but the variables are contained in larger boxes that indicate
which function they belong to.


Whenever a function is called, it creates a new **instance** of that
function. Each instance of a function contains the parameters and local
variables for that function. In the diagram an instance of a function is
represented by a box with the name of the function on the outside and
the variables and parameters inside.

In the example, main has one local variable, argument, and no
parameters. printTwice has no local variables and one parameter, named
phil.
