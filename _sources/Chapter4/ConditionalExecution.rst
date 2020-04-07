Conditional execution
---------------------

In order to write useful programs, we almost always need the ability to
check certain conditions and change the behavior of the program
accordingly. **Conditional statements** give us this ability. The
simplest form is the if statement:

::

      if (x > 0) {
        cout << "x is positive" << endl;
      }

The expression in parentheses is called the condition. If it is true,
then the statements in brackets get executed. If the condition is not
true, nothing happens.

The condition can contain any of the comparison operators:

::

        x == y               // x equals y
        x != y               // x is not equal to y
        x > y                // x is greater than y
        x < y                // x is less than y
        x >= y               // x is greater than or equal to y
        x <= y               // x is less than or equal to y

Although these operations are probably familiar to you, the syntax C++
uses is a little different from mathematical symbols like :math:`=`,
:math:`\neq` and :math:`\le`. A common error is to use a single ``=``
instead of a double ``==``. Remember that = is the assignment operator, and
``==`` is a comparison operator. Also, there is no such thing as ``=<``or ``=>``.

The two sides of a condition operator have to be the same type. You can
only compare ints to ints and doubles to doubles. Unfortunately, at this
point you can’t compare Strings at all! There is a way to compare
Strings, but we won’t get to it for a couple of chapters.

Observe the conditional statement below.

.. activecode:: fourtwo
  :language: cpp
  :caption: Conditional execution

    #include <iostream>
    using namespace std;

    int main ()
    {
      int x = 12;
      if (x == 12) {
        cout << "Equal!" << endl;
      }
      if (x != 13) {
        cout << "Not equal!" << endl;
      }
      if (x < 6) {
        cout << "Bigger!" << endl;
      }
      return 0;
    }

**Check your understanding!**

.. mchoice:: test_question_four_two
   :answer_a: Change the value of x to 2
   :answer_b: Change the last conditional statement to **x > 6**
   :answer_c: Add a semicolon to the end of the conditional statement.
   :correct: b
   :feedback_a: While "Bigger" would now print, the other two statements would not!
   :feedback_b: Correct!
   :feedback_c: Conditional statements do not need semicolons because they have curly braces, just like the main function.
   :feedback_d: Make sure to use the math keywords reserved in C++ when using math functions. Using **cosine** instead of *cos* is incorrect.


   Observe the code above. "Bigger" never prints! How can you fix this so that all of the statements print?

.. dragndrop:: dragndrop_four_one
    :feedback: Try again!
    :match_1:  x == y|||x equals y
    :match_2: x != y|||x is not equal to y
    :match_3: x > y|||x is greater than y
    :match_4: x < y|||x is less than y
    :match_5: x >= y|||x is greater than or equal to y
    :match_6: x <= y|||x is less than or equal to y

    Match the operator to its definition in words.
