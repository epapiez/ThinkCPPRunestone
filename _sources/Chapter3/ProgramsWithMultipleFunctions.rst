Programs with multiple functions
--------------------------------

When you look at a class definition that contains several functions, it
is tempting to read it from top to bottom, but that is likely to be
confusing, because that is not the **order of execution** of the
program.

Execution always begins at the first statement of main, regardless of
where it is in the program (often it is at the bottom). Statements are
executed one at a time, in order, until you reach a function call.
Function calls are like a detour in the flow of execution. Instead of
going to the next statement, you go to the first line of the called
function, execute all the statements there, and then come back and pick
up again where you left off.

That sounds simple enough, except that you have to remember that one
function can call another. Thus, while we are in the middle of main, we
might have to go off and execute the statements in threeLine. But while
we are executing threeLine, we get interrupted three times to go off and
execute newLine.

Fortunately, C++ is adept at keeping track of where it is, so each time
newLine completes, the program picks up where it left off in threeLine,
and eventually gets back to main so the program can terminate.

What’s the moral of this sordid tale? When you read a program, don’t
read from top to bottom. Instead, follow the flow of execution.


.. mchoice:: test_question5_6_1
   :practice: T
   :answer_a: 13, 14, 15, 16, 4, 5, 8, 10, 17, 18, 19
   :answer_b: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19
   :answer_c: 1, 2, 13, 15, 14, 16, 8, 9, 10, 4, 5, 6, 10, 4, 5, 7, 10, 4, 5, 6, 11, 17, 18
   :answer_d: 1, 2, 13, 14, 15, 16, 8, 9, 10, 4, 5, 6, 10, 4, 5, 6, 10, 4, 5, 6, 11, 17, 18
   :correct: d
   :feedback_a: Don't forget about the first two lines. Additionally, keep in mind that one of the functions is being called three times, meaning the program will enter the function three times.
   :feedback_b: Although C++ typically processes lines in order from top to bottom, function definitions and calls are an exception to this rule.
   :feedback_c: Close, but a few lines are mixed up!
   :feedback_d: Correct!


   Consider the following C++ code. Note that line numbers are included on the left.

   .. code-block:: cpp
      :linenos:

      #include <iostream>
      using namespace std;

      void newLine () {
        cout << endl;
      }

      void threeLine ()
      {
        newLine ();  newLine ();  newLine ();
      }

      int main ()
      {
        cout << "First Line." << endl;
        threeLine ();
        cout << "Second Line." << endl;
        return 0;
      }


   Which of the following best reflects the order in which these lines of code are processed in C++?
