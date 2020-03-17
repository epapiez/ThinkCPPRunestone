Extracting characters from a string
-----------------------------------

Strings are called “strings” because they are made up of a sequence, or
string, of characters. The first operation we are going to perform on a
string is to extract one of the characters. C++ uses square brackets
(``[`` and ``]``) for this operation:

.. activecode:: seventhree
  :language: cpp
  :caption: Accessing a string character

  #include <iostream>
  using namespace std;

    int main() {
     string fruit = "banana";
     char letter = fruit[1];
     cout << letter << endl;
    }

The expression ``fruit[1]`` indicates that I want character number 1
from the string named ``fruit``. The result is stored in a ``char``
named ``letter``. When I output the value of ``letter``, I get a
surprise:

::

   a

``a`` is not the first letter of ``"banana"``. Unless you are a computer
scientist. For perverse reasons, computer scientists always start
counting from zero. The 0th letter (“zeroeth”) of ``"banana"`` is ``b``.
The 1th letter (“oneth”) is ``a`` and the 2th (“twoeth”) letter is
``n``.

If you want the the zereoth letter of a string, you have to put zero in
the square brackets:

.. activecode:: sevenfour
  :language: cpp
  :caption: Accessing a string character

  #include <iostream>
  using namespace std;

    int main() {
     string fruit = "banana";
     char letter = fruit[0];
     cout << letter << endl;
    }

.. mchoice:: test_question_seven_one
   :practice: T
   :answer_a: 1
   :answer_b: 0
   :answer_c: 2
   :correct: b
   :feedback_a: Don't forget that computer scientists do not start counting at 1!
   :feedback_b: Correct!
   :feedback_c: This would access the letter "k"


   What would replace the "?" in order to access the letter "b" in the string below?

   .. code-block:: cpp
      :linenos:

      #include <iostream>
      using namespace std;

      int main () {
        string bake = "bake a cake!";
        char letter = bake[?];
       }

.. clickablearea:: click_seven_one
    :question: Click on each spot where a character in a string is accessed.
    :iscode:
    :feedback: Remember, square brackets [] are used to access a character in a string.

    :click-incorrect:def main() {::endclick:
        :click-incorrect:string fruit = "apple";:endclick:
        char letter = :click-correct:fruit[2];:endclick:
        :click-incorrect:cout << fruit << endl;:endclick:
        cout <<  :click-correct:fruit[4]:endclick:  << endl;
        }
