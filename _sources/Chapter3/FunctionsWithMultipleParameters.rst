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

It might be tempting to write ``(int hour, minute)``, but that format is
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

.. mchoice:: test_question_three_five
   :practice: T
   :answer_a: int addNumbers (int num, string int) {
   :answer_b: int addNumbers (int num, new) {
   :answer_c: int addNumbers (int num, int new) {
   :answer_d: integer addNumbers (int num, int new) {
   :correct: c
   :feedback_a: A parameter cannot be a reserved keyword.
   :feedback_b: Each parameter needs a data type.
   :feedback_c: Correct!
   :feedback_d: Make sure the return type is legal.


   Which of the following would be a legal first line of a function definition in C++?


.. mchoice:: test_question_three_six
   :practice: T
   :answer_a: multiplyTwo (int x, string phil);
   :answer_b: multiplyTwo (x, phil);
   :answer_c: void multiplyTwo (int num, string name) {
   :answer_d: void multiplyTwo (int x, string phil);
   :correct: b
   :feedback_a: Data types are not needed when calling a function.
   :feedback_b: Correct!
   :feedback_c: This is the start of a function definition.
   :feedback_d: Data types are not needed when calling a function.


   Which of the following is a legal function call of the function below?

   .. code-block:: cpp
      :linenos:

      void multiplyTwo (int num, string name) {
        int total = num * 2;
        cout << "Hi " << name << ", your total is " << total << "!" << endl;
      }

      int main() {
        int x = 2;
        string phil = "Phil";
        #FUNCTION CALL HERE
      }
