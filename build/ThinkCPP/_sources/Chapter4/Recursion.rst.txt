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
countdown—itself—passing ``n-1`` as an argument.

What happens if we call this function like this:

.. activecode:: fourten
  :language: cpp
  :caption: Recursion

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

The execution of countdown begins with ``n=3``, and since n is not zero, it
outputs the value 3, and then calls itself...

    The execution of countdown begins with ``n=2``, and since n is not zero,
    it outputs the value 2, and then calls itself...

        The execution of countdown begins with ``n=1``, and since n is not
        zero, it outputs the value 1, and then calls itself...

            The execution of countdown begins with ``n=0``, and since n is
            zero, it outputs the word “Blastoff!” and then returns.

        The countdown that got ``n=1`` returns.

    The countdown that got ``n=2`` returns.

The countdown that got ``n=3`` returns.

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
it outputs one newline, and then calls itself to output ``n-1`` additional
newlines. Thus, the total number of newlines is ``1 + (n-1)``, which usually
comes out to roughly n.

The process of a function calling itself is called **recursion**, and
such functions are said to be **recursive**.

.. mchoice:: test_question_four_seven_three
   :answer_a: !!
   :answer_b: !!!
   :answer_c: !!!!
   :correct: b
   :feedback_a: Try again!
   :feedback_b: Correct! First, the program enters the if statement within exclamationPoint because n is greater than 0. Then the function prints a "!" and calls itself again, but with n-1, which is 2. This repeats until n is 0, which is when the program exits the function.
   :feedback_c: The function keeps executing while n is greater than 0. Therefore, when n is 0, it will not print a "!"

   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    void exclamationPoint(int n) {
      if (n > 0) {
        cout << "!";
        exclamationPoint (n-1);
      }
    }

    int main ()
    {
      exclamationPoint(3);
    }

.. mchoice:: test_question_four_seven_four
   :answer_a: Nothing prints.
   :answer_b: !
   :answer_c: 0
   :correct: a
   :feedback_a: Correct! The program never enters the "if" statement within the function because n is never greater than 0.
   :feedback_b: Try again!
   :feedback_c: The only output statement in this program prints a "!", therefore "0" would never print.

   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    void exclamationPoint(int n) {
      if (n > 0) {
        cout << "!";
        exclamationPoint (n-1);
      }
    }

    int main ()
    {
      exclamationPoint(0);
    }
