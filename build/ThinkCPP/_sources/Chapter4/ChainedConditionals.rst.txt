Chained conditionals
--------------------

Sometimes you want to check for a number of related conditions and
choose one of several actions. One way to do this is by **chaining** a
series of ifs and elses:

.. activecode:: fourfour
  :language: cpp
  :caption: Chained conditionals

  #include <iostream>
  using namespace std;

    int main ()
    {
      int x = -4;
      if (x > 0) {
        cout << "x is positive" << endl;
      }
      else if (x < 0) {
        cout << "x is negative" << endl;
      }
      else {
        cout << "x is zero" << endl;
      }
    return 0;
    }

**Try changing the value of x above to see how the output is impacted!**

These chains can be as long as you want, although they can be difficult
to read if they get out of hand. One way to make them easier to read is
to use standard indentation, as demonstrated in these examples. If you
keep all the statements and squiggly-braces lined up, you are less
likely to make syntax errors and you can find them more quickly if you
do.

**Check your understanding!**

.. mchoice:: test_question_four_three
   :answer_a: One! Two! Three!
   :answer_b: Three!
   :answer_c: One!
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again! Make note of the use of "if" instead of "else if" or "else"
   :feedback_c: Try again! Make note of the use of "if" instead of "else if" or "else"


   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! ";
      }
      if (x > 6) {
        cout << "Two! ";
      }
      if (x >3) {
        cout << "Three!" << endl;
      }
      return 0;
    }

**Observe below!**

.. activecode:: fourfive
  :language: cpp
  :caption: Chained conditionals

  #include <iostream>
  using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! ";
      }
      if (x > 6) {
        cout << "Two! ";
      }
      if (x >3) {
        cout << "Three!" << endl;
      }
      return 0;
    }

**Check your understanding!**

.. mchoice:: test_question_four_four
   :answer_a: One! Two! Three!
   :answer_b: One!
   :answer_c: Three!
   :correct: b
   :feedback_a: Remember that a chain of "ifs", "else ifs", and "elses" will result in only one action being completed.
   :feedback_b: Correct!
   :feedback_c: Remember that only one action will be satisfied in a chain of "ifs", "else ifs", and "ifs"


   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! " ;
      }
      else if (x > 6) {
        cout << "Two! ";
      }
      else {
        cout << "Three!" << endl;
      }
      return 0;
    }

**Observe below!**

.. activecode:: foursix
  :language: cpp
  :caption: Chained conditionals

  #include <iostream>
  using namespace std;

    int main ()
    {
      int x = 10;
      if (x > 8) {
        cout << "One! ";
      }
      else if (x > 6) {
        cout << "Two! ";
      }
      else {
        cout << "Three!" << endl;
      }
      return 0;
    }
