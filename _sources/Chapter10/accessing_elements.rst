Accessing elements
------------------

The ``[]`` operator reads and writes the elements of a vector in much
the same way it accesses the characters in an ``apstring``. As with
``apstring``\ s, the indices start at zero, so ``count[0]`` refers to
the “zeroeth” element of the vector, and ``count[1]`` refers to the
“oneth” element. You can use the ``[]`` operator anywhere in an
expression:

::

     count[0] = 7;
     count[1] = count[0] * 2;
     count[2]++;
     count[3] -= 60;

All of these are legal assignment statements. Here is the effect of this
code fragment:

Since elements of this vector are numbered from 0 to 3, there is no
element with the index 4. It is a common error to go beyond the bounds
of a vector, which causes a run-time error. The program outputs an error
message like “Illegal vector index”, and then quits.

You can use any expression as an index, as long as it has type ``int``.
One of the most common ways to index a vector is with a loop variable.
For example:

::

     int i = 0;
     while (i < 4) {
       cout << count[i] << endl;
       i++;
     }

This ``while`` loop counts from 0 to 4; when the loop variable ``i`` is
4, the condition fails and the loop terminates. Thus, the body of the
loop is only executed when ``i`` is 0, 1, 2 and 3.

Each time through the loop we use ``i`` as an index into the vector,
outputting the ``i``\ th element. This type of vector traversal is very
common. Vectors and loops go together like fava beans and a nice
Chianti.

Let's take a look at how we can modify vectors by accessing elements!

.. activecode:: ch10_2
   :language: cpp
   
   #include <iostream>
   #include <vector>
   using namespace std;

   void print_vec(vector<int> vec);

   int main() {
      vector<int> count = {1,2,3,4};
      cout << "Before we make any changes, count = "; print_vec(count);
      count[0] = 7;
      count[1] = count[0] * 2;
      count[2]++;
      count[3] -= 60;
      cout << "After we made the above changes, count = "; print_vec(count);
   }

   ====
   
   void print_vec(vector<int> vec) {
      size_t i = 0;
      cout << "[";
      while (i < vec.size()-1) {
          cout << vec[i] << ",";
          i++;
      }
      cout << vec[vec.size()-1];
      cout << "]" << endl;
   }

.. mchoice:: question10_2_1
   :multiple_answers:
   :answer_a: vec[3] = vec[3]++;
   :answer_b: vec(3) = vec(3) + 1;
   :answer_c: vec[2] = vec[2]++;
   :answer_d: vec(2) = vec(2)++;
   :answer_e: vec[2] = vec[2] + 1;
   :correct: c,e
   :feedback_a: Incorrect! This is actually incrementing the 4th element of **vec**, since vectors are zero indexed.
   :feedback_b: Incorrect! This is not proper syntax.
   :feedback_c: Correct!
   :feedback_d: Incorrect! This is not proper syntax.
   :feedback_e: Correct!

   How would you increment the third element of ``vector<int> vec`` by one?

.. fillintheblank:: question10_2_2

    What is the highest index reached by ``while(i < 7)``?

    - :6: Correct!
      :7: The loop runs 7 times, but vectors are zero indexed, so the loop never reaches the 7th index!
      :.*: Incorrect!
