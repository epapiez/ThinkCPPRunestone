The return statement
--------------------

The return statement allows you to terminate the execution of a function
before you reach the end. One reason to use it is if you detect an error
condition:

.. activecode:: foureight
  :language: cpp
  :caption: The return statement

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

    int main() {
      double y = -9.8;
      printLogarithm(y);
      return 0;
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

Putting **return 0;** in your code ends your program. Let's look back at a program from section 4.3. How would your answer change?

**Check your understanding!**

.. mchoice:: test_question_four_seven
   :answer_a: One! Two! Three!
   :answer_b: Three!
   :answer_c: One!
   :correct: c
   :feedback_a: Try again! Remember the function of return 0.
   :feedback_b: Try again! Remember the function of return 0.
   :feedback_c: Correct!

   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! ";
        return 0;
      }
      if (x > 6) {
        cout << "Two! ";
        return 0;
      }
      if (x >3) {
        cout << "Three!" << endl;
        return 0;
      }
      return 0;
    }

**Observe below! Try changing the values in the conditions or the value of x to see what can change!**

.. activecode:: fournine
  :language: cpp
  :caption: The return statement

    #include <iostream>
    #include <cmath>
    using namespace std;

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! ";
        return 0;
      }
      if (x > 6) {
        cout << "Two! ";
        return 0;
      }
      if (x >3) {
        cout << "Three!" << endl;
        return 0;
      }
      return 0;
    }
