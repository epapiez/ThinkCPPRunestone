Values
------

A value is one of the fundamental things—like a letter or a number—that
a program manipulates. The only values we have manipulated so far are
the string values we have been outputting, like "Hello, world.". You
(and the compiler) can identify string values because they are enclosed
in quotation marks.

There are other kinds of values, including integers and characters. An
integer is a whole number like 1 or 17. You can output integer values
the same way you output strings:

::

      cout << 17 << endl;

A character value is a letter or digit or punctuation mark enclosed in
single quotes, like ’a’ or ’5’. You can output character values the same
way:

::

      cout << '}' << endl;

This example outputs a single close squiggly-brace on a line by itself.

It is easy to confuse different types of values, like "5", ’5’ and 5,
but if you pay attention to the punctuation, it should be clear that the
first is a string, the second is a character and the third is an
integer. The reason this distinction is important should become clear
soon.

**Check your understanding!**

.. mchoice:: test_question_two_one
   :practice: T
   :answer_a: 1
   :answer_b: 2
   :answer_c: 3
   :correct: b
   :feedback_a: There is only one "endl", implying that only one new line is created.
   :feedback_b: Yes, the "endl" creates one new line. The first line will say 7, while the second will print 77.
   :feedback_c: In C++, you must make sure to say "endl" every time you'd like to create a new line.


   On how many separate lines will the 7's be printed?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
      cout << 7 << endl;
      cout << 7;
      cout << 7;
    }

.. dragndrop:: dragndrop_two_two
    :feedback: Try again!
    :match_1:  1|||integer
    :match_2: "1"|||string
    :match_3: '1'|||character

    Match the value to its data type.
