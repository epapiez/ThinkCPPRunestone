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

    True or False: ``for`` loops are incremented in the body of the loop?

    - :([Ff]alse|FALSE): Correct!
      :.*: Incorrect! For loops are incremented inside of the parentheses!

.. fillintheblank:: question10_4_2

    True or False: the initialization happens before the ``while`` loop?

    - :([Tt]rue|TRUE): Correct!
      :.*: Incorrect! We must initialize before we can increment!
