Boolean variables
-----------------

As usual, for every type of value, there is a corresponding type of
variable. In C++ the boolean type is called **bool**. Boolean variables
work just like the other types:

::

      bool fred;
      fred = true;
      bool testResult = false;

The first line is a simple variable declaration; the second line is an
assignment, and the third line is a combination of a declaration and as
assignment, called an initialization.

As I mentioned, the result of a comparison operator is a boolean, so you
can store it in a bool variable

::

      bool evenFlag = (n%2 == 0);     // true if n is even
      bool positiveFlag = (x > 0);    // true if x is positive

and then use it as part of a conditional statement later

::

      if (evenFlag) {
        cout << "n was even when I checked it" << endl;
      }

A variable used in this way is called a **flag**, since it flags the
presence or absence of some condition.

.. dragndrop:: dragndrop_five_one
    :feedback: Try again!
    :match_1: x / 2 > 4|||false
    :match_2: x >= 2|||true

    Match the conditional statement to the correct boolean, given x = 2.


.. dragndrop:: dragndrop_five_one_
    :feedback: Try again!
    :match_1: bool fred;|||variable declaration
    :match_2: fred = true;|||assignment
    :match_3: bool testResult = false;|||initialization

    Match the statement to the word that describes it best.


.. mchoice:: test_question_five_three_two_
   :answer_a: n was even when I checked it x was positive when I checked it
   :answer_b: x was positive when I checked it
   :answer_c: n was even when I checked itx was positive when I checked it
   :correct: c
   :feedback_a: A space is not automatically added, it must also be outputted
   :feedback_b: Try again!
   :feedback_c: Correct!

   What will print?

   .. code-block:: cpp

     int n = 16;
     int x = 4;

     bool evenFlag = (n%2 == 0);
     bool positiveFlag = (x > 0);

     if (evenFlag) {
       cout << "n was even when I checked it" << endl;
     }

     if (positiveFlag) {
       cout << "x was positive when I checked it"
     }
