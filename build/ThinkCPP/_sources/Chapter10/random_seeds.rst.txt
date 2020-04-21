Random seeds
------------

If you have run the code in this chapter a few times, you might have
noticed that you are getting the same “random” values every time. That’s
not very random!

One of the properties of pseudorandom number generators is that if they
start from the same place they will generate the same sequence of
values. The starting place is called a **seed**; by default, C++ uses
the same seed every time you run the program.

While you are debugging, it is often helpful to see the same sequence
over and over. That way, when you make a change to the program you can
compare the output before and after the change.

If you want to choose a different seed for the random number generator,
you can use the ``srand`` function. It takes a single argument, which is
an integer between 0 and ``RAND_MAX``.

For many applications, like games, you want to see a different random
sequence every time the program runs. A common way to do that is to use
a library function like ``gettimeofday`` to generate something
reasonably unpredictable and unrepeatable, like the number of
milliseconds since the last second tick, and use that number as a seed.
The details of how to do that depend on your development environment.

.. mchoice:: question10_14_1
   :answer_a: random()
   :answer_b: srand(int)
   :answer_c: srand(gettimeofday())
   :correct: c
   :feedback_a: Incorrect! This always generates the same set of values, using the default seed in C++.
   :feedback_b: Incorrect! This always generates the same set of values, using the specified seed.
   :feedback_c: Correct! Get time of day will generate something reasonably random, which you can then use as a random seed.

   Which of the following will generate a different random number every time the programs runs?