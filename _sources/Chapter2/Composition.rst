Composition
-----------

So far we have looked at the elements of a programming
language—variables, expressions, and statements—in isolation, without
talking about how to combine them.

One of the most useful features of programming languages is their
ability to take small building blocks and **compose** them. For example,
we know how to multiply integers and we know how to output values; it
turns out we can do both at the same time:

.. activecode:: twofourteen
  :language: cpp
  :caption: Outputting multiplication

    #include <iostream>
    using namespace std;

    int main ()
    {
      cout << 17 * 3;
    }

Actually, I shouldn’t say “at the same time,” since in reality the
multiplication has to happen before the output, but the point is that
any expression, involving numbers, characters, and variables, can be
used inside an output statement. We’ve already seen one example:

.. activecode:: twofifteen
  :language: cpp
  :caption: Outputting multiplication and addition

    #include <iostream>
    using namespace std;

    int main ()
    {
      int hour = 7;
      int minute = 1;
      cout << hour*60 + minute << endl;
    }

You can also put arbitrary expressions on the right-hand side of an
assignment statement:

.. activecode:: twosixteen
  :language: cpp
  :caption: Outputting multiplication and division

    #include <iostream>
    using namespace std;

    int main ()
    {
      int minute = 3;
      int percentage;
      percentage = (minute * 100) / 60;
      cout << percentage;
    }

This ability may not seem so impressive now, but we will see other
examples where composition makes it possible to express complex
computations neatly and concisely.

WARNING: There are limits on where you can use certain expressions; most
notably, the left-hand side of an assignment statement has to be a
*variable* name, not an expression. That’s because the left side
indicates the storage location where the result will go. Expressions do
not represent storage locations, only values. So the following is
illegal: ``minute+1 = hour;``.

**Check your understanding!**

.. mchoice:: test_question_two_three
   :practice: T
   :answer_a: Change the fourth line within main to **pets = dogs + cats;**
   :answer_b: Change the third line within main to **int pets = dogs;**
   :answer_c: Change the fourth line within main to **pets == dogs + cats;**
   :correct: a
   :feedback_a: Correct!
   :feedback_b: The variables were assigned as two different types, so they wouldn't both need to be changed.
   :feedback_c: Yes, variable d is a char because it was assigned as a single character with single quotes around it.


   What must be changed in order for this code block to work?

   .. code-block:: cpp

      #include <iostream>
      using namespace std;

      int main ()
      {
        int dogs = 3;
        int cats = 6;
        int pets;
        dogs + cats = pets;
        cout << "I have " << pets << " pets!";
        return 0;
        }

.. fillintheblank:: fill_2.9_one

    The left-hand side of an assignment statement has to be a ____ name, not an expression.

    - :(?:v|V)(?:A|a)(?:r|R)(?:I|i)(?:a|A)(?:b|B)(?:l|L)(?:e|e): Correct!
      :.*: Try again!
