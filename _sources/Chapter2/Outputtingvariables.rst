Outputting variables
--------------------

You can output the value of a variable using the same commands we used
to output simple values. After observing the output, try inputting your own time!

.. activecode:: twofive
   :language: cpp
   :caption: Outputting variables

   #include <iostream>
   using namespace std;
   // main: generate some simple output

   int main () {
      int hour, minute;
      char colon;

      hour = 11;
      minute = 59;
      colon = ':';

      cout << "The current time is ";
      cout << hour;
      cout << colon;
      cout << minute;
      cout << endl;

      return 0;
   }

This program creates two integer variables named hour and minute, and a
character variable named colon. It assigns appropriate values to each of
the variables and then uses a series of output statements to generate
the following:

::

    The current time is 11:59

When we talk about “outputting a variable,” we mean outputting the
*value* of the variable. To output the *name* of a variable, you have to
put it in quotes. For example: ``cout << "hour";``

As we have seen before, you can include more than one value in a single
output statement, which can make the previous program more concise:

.. activecode:: twosix
   :language: cpp
   :caption: Outputting variables

   #include <iostream>
   using namespace std;
   // main: generate some simple output

   int main () {
      int hour, minute;
      char colon;

      hour = 11;
      minute = 59;
      colon = ':';

      cout << "The current time is " << hour << colon << minute << endl;

      return 0;
   }

On one line, this program outputs a string, two integers, a character,
and the special value endl. Very impressive!

.. mchoice:: question2_5_1
   :answer_a: a
   :answer_b: b
   :answer_c: z
   :answer_d: 8
   :answer_e: Nothing! There will be a compile error!
   :correct: a
   :feedback_a: The string, not the variable, a will be printed.
   :feedback_b: b will not be printed.
   :feedback_c: The cout statement prints a, not the value of the variable a.
   :feedback_d: z is the value of a and will not be printed
   :feedback_e: There is no type mismatch, so there will not be a compile error.

   What prints?

   .. code-block:: cpp

    int main () {
      char a;
      char b;
      a = 'z';
      b = '8';
      cout << "a";
    }

.. mchoice:: question2_5_2
   :answer_a: a
   :answer_b: b
   :answer_c: z
   :answer_d: 8
   :answer_e: Nothing! There will be a compile error!
   :correct: d
   :feedback_a: The string a will not be printed.
   :feedback_b: The string b will not be printed.
   :feedback_c: z is the value of a and will not be printed.
   :feedback_d: 8 is the value of b will not be printed!
   :feedback_e: There is no type mismatch, so there will not be a compile error.

   Now, what prints?

   .. code-block:: cpp

    int main () {
      char a;
      char b;
      a = 'z';
      b = '8';
      cout << b;
    }

.. mchoice:: question2_5_3
   :answer_a: x
   :answer_b: y
   :answer_c: 3
   :answer_d: e
   :answer_e: Nothing! There will be a compile error!
   :correct: e
   :feedback_a: Take a look at the code again.
   :feedback_b: Take a look at the code again.
   :feedback_c: Take a look at the code again.
   :feedback_d: Take a look at the code again.
   :feedback_e: There is a type mismatch, so there will be a compile error!

   And now, what prints?

   .. code-block:: cpp

    int main () {
      int x;
      char y;
      x = '3';
      y = 'e';
      cout << 'y';
    }

.. dragndrop:: question2_5_4
    :feedback: Try again!
    :match_1:  x = 2|||int
    :match_2: y = "2"|||string
    :match_3: z = '2'|||char

    Match the variable initialization to its correct type.

.. activecode:: twoseven
  :language: cpp
  :caption: Integers and chars declaration
  
  Fix the following code so that each variable has a type!

  ~~~~

  #include <iostream>
  using namespace std;

  int main() {
    x = 0;
    z = '.';
    cout << x;
    cout << z << endl;
    return 0;
  }
