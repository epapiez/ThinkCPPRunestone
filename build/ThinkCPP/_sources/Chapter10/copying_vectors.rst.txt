Copying vectors
---------------

There is one more constructor for ``vector``\ s, which is called a copy
constructor because it takes one ``vector`` as an argument and creates a
new vector that is the same size, with the same elements.

::

     vector<int> copy (count);

Although this syntax is legal, it is almost never used for ``vector``\ s
because there is a better alternative:

::

     vector<int> copy = count;

The ``=`` operator works on ``vector``\ s in pretty much the way you
would expect.

.. mchoice:: question10_3_1
   :multiple_answers:
   :answer_a: vector&#60;double&#62; nums = decimals;
   :answer_b: vector&#60;double&#62; decimals = nums;
   :answer_c: vector&#60;double&#62; nums (decimals);
   :answer_d: vector&#60;double&#62; decimals (nums);
   :correct: a,c
   :feedback_a: Correct!
   :feedback_b: Incorrect! This makes a copy of nums called decimals.
   :feedback_c: Correct!
   :feedback_d: Incorrect! This makes a copy of nums called decimals.

   How would you make a copy of ``vector<double> decimals`` called **nums**?