``string``\ s are comparable
----------------------------

All the comparison operators that work on ``int``\ s and ``double``\ s
also work on ``strings``. For example, if you want to know if two
strings are equal:

.. activecode:: sevenfifteen
  :language: cpp
  :caption: Strings are comparable

  #include <iostream>
  using namespace std;

  int main() {

     word = "banana";

     if (word == "banana") {
       cout << "Yes, we have no bananas!" << endl;
     }
  }

The other comparison operations are useful for putting words in
alphabetical order.

.. activecode:: sevensixteen
  :language: cpp
  :caption: Strings are comparable

    #include <iostream>
    using namespace std;

    int main() {

     string word = "Zebra";

     if (word < "banana") {
       cout << "Your word, " << word << ", comes before banana." << endl;
     } else if (word > "banana") {
       cout << "Your word, " << word << ", comes after banana." << endl;
     } else {
       cout << "Yes, we have no bananas!" << endl;
     }
    }

You should be aware, though, that the ``string`` class does not handle
upper and lower case letters the same way that people do. All the upper
case letters come before all the lower case letters. As a result,

::

   Your word, Zebra, comes before banana.

A common way to address this problem is to convert strings to a standard
format, like all lower-case, before performing the comparison. The next
sections explains how. I will not address the more difficult problem,
which is making the program realize that zebras are not fruit.

For the following questions, remember that in C++ ``1`` means true and ``0`` means false.

.. mchoice:: test_question_seven
   :practice: T
   :answer_a: 1
   :answer_b: 0
   :correct: a
   :feedback_a: Both match up to the g but Dog is shorter than Doghouse so it comes first in the dictionary.
   :feedback_b: Strings are compared character by character.

   Evaluate the following comparison:

   .. code-block:: cpp

      "Dog" < "Doghouse";

.. mchoice:: test_question_seven_eight
   :practice: T
   :answer_a: 1
   :answer_b: 0
   :answer_c: They are the same word
   :correct: b
   :feedback_a: d is greater than D
   :feedback_b: Yes, upper case is less than lower case according to the ordinal values of the characters.
   :feedback_c: C++ is case sensitive meaning that upper case and lower case characters are different.

   Evaluate the following comparison:

   .. code-block:: cpp

      "dog" < "Dog";

.. mchoice:: test_question_seven_nine
   :practice: T
   :answer_a: 1
   :answer_b: 0
   :correct: b
   :feedback_a: d is greater than D.
   :feedback_b: The length does not matter.  Lower case d is greater than upper case D.

   Evaluate the following comparison:

   .. code-block:: cpp

      "dog" < "Doghouse";
