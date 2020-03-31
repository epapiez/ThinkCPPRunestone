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
