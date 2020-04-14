Returning from main
-------------------

Now that we have functions that return values, I can let you in on a
secret. main is not really supposed to be a void function. It’s supposed
to return an integer:

::

    int main ()
    {
      return 0;
    }

The usual return value from main is 0, which indicates that the program
succeeded at whatever it was supposed to do. If something goes wrong, it
is common to return -1, or some other value that indicates what kind of
error occurred.

Of course, you might wonder who this value gets returned to, since we
never call main ourselves. It turns out that when the system executes a
program, it starts by calling main in pretty much the same way it calls
all the other functions.

There are even some parameters that are passed to main by the system,
but we are not going to deal with them for a little while.

.. mchoice:: test_question_five_three_two_seven
   :answer_a: nothing, it is void
   :answer_b: an integer
   :answer_c: a string
   :correct: b
   :feedback_a: Try again!
   :feedback_b: Correct!
   :feedback_c: Try again!

   What data type is the main function supposed to return?

.. mchoice:: test_question_five_three_two_eight
   :answer_a: 0
   :answer_b: -1
   :answer_c: nothing
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again!
   :feedback_c: Try again!

   What is the usual return value of the main function?
