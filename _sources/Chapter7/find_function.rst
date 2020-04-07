The ``find`` function
---------------------

The ``string`` class provides several other functions that you can
invoke on strings. The ``find`` function is like the opposite the ``[]``
operator. Instead of taking an index and extracting the character at
that index, ``find`` takes a character and finds the index where that
character appears.


.. activecode:: seveneight
  :language: cpp
  :caption: The find function

  #include <iostream>
  using namespace std;

    int main() {
     string fruit = "banana";
     int index = fruit.find('a');
     cout << index << endl;
     string dessert = "pudding";
     int another_index = fruit.find('a');
     cout << another_index << endl;
    }

This example finds the index of the letter ``’a’`` in the string. In
this case, the letter appears three times, so it is not obvious what
``find`` should do. According to the documentation, it returns the index
of the *first* appearance, so the result is 1. If the given letter does
not appear in the string, ``find`` returns -1.

In addition, there is a version of ``find`` that takes another
``string`` as an argument and that finds the index where the substring
appears in the string. For example,

.. activecode:: sevennine
  :language: cpp
  :caption: The find function

  #include <iostream>
  using namespace std;

    int main() {
     string fruit = "banana";
     int index = fruit.find("nan");
     cout << index;
    }

This example returns the value 2.

You should remember from Section `[overloading] <#overloading>`__ that
there can be more than one function with the same name, as long as they
take a different number of parameters or different types. In this case,
C++ knows which version of ``find`` to invoke by looking at the type of
the argument we provide.

.. clickablearea:: click_seven_three
    :question: Click on the name of each variable that had been initialized with the value of 0.
    :iscode:
    :feedback: Remember that the index of a string begins at 0, not 1.

    :click-incorrect:def main() {::endclick:
        :click-incorrect:string fruit = "apple";:endclick:
        int:click-incorrect: index_a :endclick:= fruit.find('e');
        int:click-correct: index_b :endclick:= fruit.find("app");
        int:click-correct: index_c :endclick:= fruit.find('a');
        int:click-incorrect: index_d :endclick:= fruit.find('l');
        }

.. parsonsprob:: question_seven_three

   Construct a block of code that correctly finds and prints where the first "B" is in the string. Declare ``city`` before ``index``.
   -----
   int main() {

      string city = "New Baltimore";

      string city = "New Baltimore" #distractor

      int index;

      index = city.find('B');

      index = city.find(B); #distractor

      index = city.find('b'); #distractor

      cout << index << endl;

   }
