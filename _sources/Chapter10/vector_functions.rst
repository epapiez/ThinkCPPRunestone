Vector functions
----------------

The best feature of a vector is its resizeability. A vector, once
declared, can be resized from anywhere within the program. Suppose we
have a situation where we input numbers from the user and store them in
a vector till he inputs ``-1``, and then display them. In such a case,
we do not know the size of the vector beforehand. So we need wish add
new values to the end of a vector as the user inputs them. We can use
then vector function ``push_back()`` for that purpose.

::

   #include<iostream>
   #include<vector>
   using namespace std;
   int main()
   {
     vector<int> values;
     int c,i,len;
     cin >> c;

     while(c != -1) {
       values.push_back(c);
       cin >> c;
     }
     len=values.size();
     for(i = 0; i < len; i++) {
       cout << values[i] << endl;
     }
   }

.. mchoice:: question10_6_1
   :answer_a: 5
   :answer_b: 6
   :answer_c: 7
   :answer_d: 8
   :correct: b
   :feedback_a: Incorrect! This is the size of the vector before we ran the command.
   :feedback_b: Correct!
   :feedback_c: Incorrect!
   :feedback_d: Incorrect! We are adding the element 3 to the end of the vector, not 3 elements!

   Let **nums** be the vector { 0, 1, 2, 3, 4 }. If we run the command ``nums.push_back(3)``, what will be returned by ``nums.size()``?
