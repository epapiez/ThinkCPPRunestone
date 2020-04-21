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

.. mchoice:: test_question_three_three
   :practice: T
   :answer_a: 1 local variable, 1 parameter
   :answer_b: 0 local variables, 1 parameter
   :answer_c: 2 local variables, 0 parameters
   :answer_d: 2 local variables, 1 parameter
   :correct: c
   :feedback_a: A parameter would be located within the parentheses next to the function's name.
   :feedback_b: A parameter would be located within the parentheses next to the function's name.
   :feedback_c: Correct!
   :feedback_d: A parameter would be located within the parentheses next to the function's name.

   How many local variables and parameters does main have?

   .. code-block:: cpp
      :linenos:

        void printHelloName (string name) {
          cout << "Hello " << name << "!";
          }

        int main ()
        {
          string name1 = "Phil";
          printHelloName(name1);
          string name2 = "Joe";
          printHelloName(name2);
          return 0;
          }


.. mchoice:: test_question_three_four
   :practice: T
   :answer_a: 1 local variable, 1 parameter
   :answer_b: 0 local variables, 1 parameter
   :answer_c: 2 local variables, 0 parameters
   :answer_d: 2 local variables, 1 parameter
   :correct: b
   :feedback_a: A local variable exists when a variable is declared within a function.
   :feedback_b: Correct!
   :feedback_c: A local variable exists when a variable is declared within a function.
   :feedback_d: A local variable exists when a variable is declared within a function.

   How many local variables and parameters does printHelloName have?

   .. code-block:: cpp

        void printHelloName (string name) {
          cout << "Hello " << name << "!";
          }

        int main ()
        {
          string name1 = "Phil";
          printHelloName(name1);
          string name2 = "Joe";
          printHelloName(name2);
          return 0;
        }
