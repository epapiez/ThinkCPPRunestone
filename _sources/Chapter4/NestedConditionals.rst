Nested conditionals
-------------------

In addition to chaining, you can also nest one conditional within
another. We could have written the previous example as:

.. activecode:: fourseven
  :language: cpp
  :caption: Nested conditionals

  #include <iostream>
  using namespace std;

    int main ()
    {
      int x = 9;
      if (x == 0) {
        cout << "x is zero" << endl;
      }
      else {
        if (x > 0) {
          cout << "x is positive" << endl;
        } else {
          cout << "x is negative" << endl;
        }
      }
      return 0;
    }

There is now an outer conditional that contains two branches. The first
branch contains a simple output statement, but the second branch
contains another if statement, which has two branches of its own.
Fortunately, those two branches are both output statements, although
they could have been conditional statements as well.

Notice again that indentation helps make the structure apparent, but
nevertheless, nested conditionals get difficult to read very quickly. In
general, it is a good idea to avoid them when you can.

On the other hand, this kind of **nested structure** is common, and we
will see it again, so you better get used to it.


**Check your understanding!**

.. mchoice:: test_question_four_five
   :answer_a: Hey!
   :answer_b: Hi!
   :answer_c: Hello!
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Remember that the program would only enter the "else" if x was not equal to 0.
   :feedback_c: Remember that the program would only enter the "else" if x was not equal to 0.

   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 0;
      if (x == 0) {
        cout << "Hey!" << endl;
      }
      else {
        if (x > 0) {
          cout << "Hi!" << endl;
        } else {
          cout << "Hello!" << endl;
        }
      }
      return 0;
    }

.. mchoice:: test_question_four_five_one
   :answer_a: Hey!
   :answer_b: Hi!
   :answer_c: Hello!
   :correct: c
   :feedback_a: Remember that the program would only enter the first "if" if x was equal to 0.
   :feedback_b: Remember that the program would only enter the nested "if" if x was greater than 0.
   :feedback_c: Correct!

   What will print?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = -4;
      if (x == 0) {
        cout << "Hey!" << endl;
      }
      else {
        if (x > 0) {
          cout << "Hi!" << endl;
        } else {
          cout << "Hello!" << endl;
        }
      }
      return 0;
    }
