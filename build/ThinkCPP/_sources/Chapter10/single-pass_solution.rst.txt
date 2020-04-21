A single-pass solution
----------------------

Although this code works, it is not as efficient as it could be. Every
time it calls ``howMany``, it traverses the entire vector. In this
example we have to traverse the vector ten times!

It would be better to make a single pass through the vector. For each
value in the vector we could find the corresponding counter and
increment it. In other words, we can use the value from the vector as an
index into the histogram. Here’s what that looks like:

::

     vector<int> histogram (upperBound, 0);

     for (int i = 0; i < numValues; i++) {
       int index = vector[i];
       histogram[index]++;
     }

The first line initializes the elements of the histogram to zeroes. That
way, when we use the increment operator (``++``) inside the loop, we
know we are starting from zero. Forgetting to initialize counters is a
common error.

As an exercise, encapsulate this code in a function called ``histogram``
that takes a vector and the range of values in the vector (in this case
0 through 10), and that returns a histogram of the values in the vector.

.. parsonsprob:: question10_13_1

   Construct a function called **histogram** that takes a vector and the range of values in the vector, and that returns a histogram of values in the vector.
   -----
   vector&#60;int&#62; histogram(const vector&#60;int&#62;& vec, int range) {
   =====
      vector&#60;int&#62; histogram (range, 0);
   =====
      vector&#60;int&#62; histogram (range);                         #paired
   =====
      for (int i = 0; i &#60; vec.size(); i++) {
   =====
      for (int i = 0; i &#60; range; i++) {                         #paired
   =====
         int index = vec[i];
   =====
         int index = i;                         #paired
   =====
         histogram[index]++;
   =====
      }
      return histogram;
   }
