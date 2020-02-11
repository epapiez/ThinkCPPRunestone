Functions with multiple parameters
----------------------------------

The syntax for declaring and invoking functions with multiple parameters
is a common source of errors. First, remember that you have to declare
the type of every parameter. For example

::

      void printTime (int hour, int minute) {
        cout << hour;
        cout << ":";
        cout << minute;
      }

It might be tempting to write (int hour, minute), but that format is
only legal for variable declarations, not for parameters.

Another common source of confusion is that you do not have to declare
the types of arguments. The following is wrong!

::

        int hour = 11;
        int minute = 59;
        printTime (int hour, int minute);   // WRONG!

In this case, the compiler can tell the type of hour and minute by
looking at their declarations. It is unnecessary and illegal to include
the type when you pass them as arguments. The correct syntax is
printTime (hour, minute).

.. activecode:: threeten
  :language: cpp
  :caption: Understanding parameters from previous section.

  #include <iostream>
  using namespace std;

  void printPrice (int dollars, int cents) {
    cout << "Price is " << dollars << " dollars and " << cents << " cents." << endl;
  }

  int main () {
    int dollar_amount = 2;
    int cent_amount = 92;
    printPrice (dollar_amount, cent_amount);
    return 0;
  }
