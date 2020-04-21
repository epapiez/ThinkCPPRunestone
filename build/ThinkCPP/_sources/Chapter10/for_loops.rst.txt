``for`` loops
-------------

The loops we have written so far have a number of elements in common.
All of them start by initializing a variable; they have a test, or
condition, that depends on that variable; and inside the loop they do
something to that variable, like increment it.

This type of loop is so common that there is an alternate loop
statement, called ``for``, that expresses it more concisely. The general
syntax looks like this:

::

     for (INITIALIZER; CONDITION; INCREMENTOR) {
       BODY
     }

This statement is exactly equivalent to

::

     INITIALIZER;
     while (CONDITION) {
       BODY
       INCREMENTOR
     }

except that it is more concise and, since it puts all the loop-related
statements in one place, it is easier to read. For example:

::

     int i;
     for (i = 0; i < 4; i++) {
       cout << count[i] << endl;
     }

is equivalent to

::

     int i = 0;
     while (i < 4) {
       cout << count[i] << endl;
       i++;
     }

.. fillintheblank:: question10_4_1

    How many times would the following loop execute?  ``for (int i = 1; i < 4; i++)``

    - :3: Correct!
      :4: Incorrect! The loop does not execute when i = 4.
      :.*: Incorrect!

.. mchoice:: question10_4_2
   :answer_a: in the BODIES of both loops
   :answer_b: in the BODY of a for loop, and in the statement of a while loop
   :answer_c: in the statement of a for loop, and in the BODY of a while loop
   :answer_d: in the statements of both loops
   :correct: c
   :feedback_a: Incorrect!
   :feedback_b: Incorrect!
   :feedback_c: Correct!
   :feedback_d: Incorrect!

   Where are the incrementors in ``for`` loops and ``while``?
