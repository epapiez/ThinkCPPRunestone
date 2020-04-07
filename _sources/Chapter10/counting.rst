Counting
--------

A good approach to problems like this is to think of simple functions
that are easy to write, and that might turn out to be useful. Then you
can combine them into a solution. This approach is sometimes called
**bottom-up design**. Of course, it is not easy to know ahead of time
which functions are likely to be useful, but as you gain experience you
will have a better idea.

Also, it is not always obvious what sort of things are easy to write,
but a good approach is to look for subproblems that fit a pattern you
have seen before.

Back in Section `[loopcount] <#loopcount>`__ we looked at a loop that
traversed a string and counted the number of times a given letter
appeared. You can think of this program as an example of a pattern
called “traverse and count.” The elements of this pattern are:

-  A set or container that can be traversed, like a string or a vector.

-  A test that you can apply to each element in the container.

-  A counter that keeps track of how many elements pass the test.

In this case, I have a function in mind called ``howMany`` that counts
the number of elements in a vector that equal a given value. The
parameters are the vector and the integer value we are looking for. The
return value is the number of times the value appears.

::

   int howMany (const vector<int>& vec, int value) {
     int count = 0;
     for (int i=0; i< vec.size(); i++) {
       if (vec[i] == value) count++;
     }
     return count;
   }

.. parsonsprob:: question10_10_1

   Construct a block of code that counts how many numbers are between **lowerbound** and **upperbound** inclusive.
   -----
   int just_right(const vector<int>& vec, int lowerbound, int upperbound) {
   =====
      int count = 0;
   =====
      for (int i=0; i &#60; vec.size(); i++) {
   =====
      for (int i=0; i &#60; upperbound; i++)                         #paired
   =====
         if (vec[i] i &#62;= lowerbound && vec[i] i &#60;= upperbound) {
	    count++;
   =====
         if (vec[i] i &#62; lowerbound && vec[i] i &#60; upperbound) {                         #paired
            count++;
   =====
         }
      }
      return count;
   }
