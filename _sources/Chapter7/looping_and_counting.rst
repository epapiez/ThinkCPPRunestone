Looping and counting
--------------------

The following program counts the number of times the letter ``’a’``
appears in a string:

.. activecode:: seveneleven
  :language: cpp
  :caption: Looping and counting

  #include <iostream>
  using namespace std;

  int main() {
     string fruit = "banana";
     int length = fruit.length();
     int count = 0;

     int index = 0;
     while (index < length) {
       if (fruit[index] == 'a') {
         count = count + 1;
       }
       index = index + 1;
     }
     cout << count << endl;

  }

This program demonstrates a common idiom, called a **counter**. The
variable ``count`` is initialized to zero and then incremented each time
we find an ``’a’``. (To **increment** is to increase by one; it is the
opposite of **decrement**, and unrelated to **excrement**, which is a
noun.) When we exit the loop, ``count`` contains the result: the total
number of a’s.

.. mchoice:: test_question_seven_one___
   :practice: T
   :answer_a: 5 4 3 2 1
   :answer_b: -5 -4 -3 -2 -1
   :answer_c: -4 -3 -2 -1 0
   :correct: c
   :feedback_a: Notice that x is negative.
   :feedback_b: Notice that the value of x is incremented before it is printed.
   :feedback_c: Correct! The value of x is incremented before it is printed so the first value printed is -4.


   What does the following code print?

   .. code-block:: cpp
      :linenos:

      int x = -5;
      while (x < 0){
        x = x + 1;
        cout << x << " ";
      }


.. parsonsprob:: question_seven_four

   As an exercise, encapsulate this code in a function named
   ``countLetters``, and generalize it so that it accepts the string and
   the letter as arguments. In the function, declare length, count, and index in that order.
   Within the main function, declare city and letter in that order.
   -----
   int countLetter(string s, char letter) {

      int length = s.length();
      int count = 0;
      int index = 0;

      while (index < length) {

        if (s[index] == letter) {

          count = count + 1; }

        index = index + 1; }

      return count; }

   int main() {

      string city = "New Baltimore";
      char letter = "e";

      cout << countLetter(city, letter); }


.. parsonsprob:: question_seven_four_four

   The following is the correct code for printing the even numbers from 0 to 10, but it also includes some extra code that you won't need. Drag the needed blocks from the left and put them in the correct order on the right.
   -----
   x = x + 1; #distractor

   x = 0;

   while (x <= 10){

   while (x < 10){ #distractor

      cout << x << endl;

      x = x + 2;}
