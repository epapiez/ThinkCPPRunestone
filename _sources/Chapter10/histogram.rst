A histogram
-----------

It is often useful to take the data from the previous tables and store
them for later access, rather than just print them. What we need is a
way to store 10 integers. We could create 10 integer variables with
names like ``howManyOnes``, ``howManyTwos``, etc. But that would require
a lot of typing, and it would be a real pain later if we decided to
change the range of values.

A better solution is to use a vector with size 10. That way we can
create all ten storage locations at once and we can access them using
indices, rather than ten different names. Here’s how:

::

     int numValues = 100000;
     int upperBound = 10;
     vector<int> vector = randomVector (numValues, upperBound);
     vector<int> histogram (upperBound);

     for (int i = 0; i<upperBound; i++) {
       int count = howMany (vector, i);
       histogram[i] = count;
     }

I called the vector **histogram** because that’s a statistical term for
a vector of numbers that counts the number of appearances of a range of
values.

The tricky thing here is that I am using the loop variable in two
different ways. First, it is an argument to ``howMany``, specifying
which value I am interested in. Second, it is an index into the
histogram, specifying which location I should store the result in.

.. shortanswer:: question10_12_1

   Why would you use a vector, rather than integer variables to store class data for a C++ exam?