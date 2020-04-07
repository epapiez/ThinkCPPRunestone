Vector size
-----------

There are a few functions you can invoke on an ``vector``. One of them
is very useful, though: ``size()``. Not surprisingly, it returns the
size of the vector (the number of elements).

It is a good idea to use this value as the upper bound of a loop, rather
than a constant. That way, if the size of the vector changes, you won’t
have to go through the program changing all the loops; they will work
correctly for any size vector.

::

     int i;
     for (i = 0; i < count.size(); i++) {
       cout << count[i] << endl;
     }

The last time the body of the loop gets executed, the value of ``i`` is
``count.size() - 1``, which is the index of the last element. When ``i``
is equal to ``count.size()``, the condition fails and the body is not
executed, which is a good thing, since it would cause a run-time error.
One thing that we should notice here is that the size() function is
called every time the loop is executed. Calling a function again and
again reduces execution speed, so it would be better to store the size
in some variable by calling the ``size()`` function before the loop
begins, and use this variable to check for the last element. You can try
this program as an excercise.

.. fillintheblank:: question10_5_1

    Let **nums** be the vector { 0, 1, 2, 3, 4 }. What is the value *of* ``nums.size()``?

    - :5: Correct!
      :.*: Incorrect, Try again!

.. mchoice:: question10_5_2
   :answer_a: 5
   :answer_b: 4
   :answer_c: 3
   :answer_d: none of the above
   :correct: d
   :feedback_a: Incorrect! This is what gets returned by nums.size()
   :feedback_b: Incorrect! This is the element before nums[nums.size()]
   :feedback_c: Incorrect!
   :feedback_d: Correct! This would be indexing out of bounds and would cause a runtime error.

   Let **nums** be the vector { 0, 1, 2, 3, 4 }. What is the value *at* ``nums[nums.size()]``?
