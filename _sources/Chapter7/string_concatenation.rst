String concatenation
--------------------

Interestingly, the ``+`` operator can be used on strings; it performs
string **concatenation**. To concatenate means to join the two operands
end to end. For example:

.. activecode:: seventwelve
  :language: cpp
  :caption: String concatenation

  #include <iostream>
  using namespace std;

  int main() {
     string fruit = "banana";
     string bakedGood = " nut bread";
     string dessert = fruit + bakedGood;
     cout << dessert << endl;
  }

The output of this program is ``banana nut bread``.

Unfortunately, the ``+`` operator does not work on native C strings, so
you cannot write something like

::

     string dessert = "banana" + " nut bread";

because both operands are C strings. As long as one of the operands is
a ``string``, though, C++ will automatically convert the other.

It is also possible to concatenate a character onto the beginning or end
of an ``string``. In the following example, we will use concatenation
and character arithmetic to output an abecedarian series.

“Abecedarian” refers to a series or list in which the elements appear in
alphabetical order. For example, in Robert McCloskey’s book *Make Way
for Ducklings*, the names of the ducklings are Jack, Kack, Lack, Mack,
Nack, Ouack, Pack and Quack. Here is a loop that outputs these names in
order:

.. activecode:: seventhirteen
  :language: cpp
  :caption: String concatenation

  #include <iostream>
  using namespace std;

  int main() {
     string suffix = "ack";
     char letter = 'J';
     while (letter <= 'Q') {
       cout << letter + suffix << endl;
       letter++;
     }
   }

The output of this program is:

::

   Jack
   Kack
   Lack
   Mack
   Nack
   Oack
   Pack
   Qack

Again, be careful to use string concatenation only with ``string``\ s
and not with native C strings. Unfortunately, an expression like
``letter + "ack"`` is syntactically legal in C++, although it produces a
very strange result, at least in my development environment.

.. mchoice:: test_question_seven_five
   :practice: T
   :answer_a: C++ rocks
   :answer_b: C++
   :answer_c: C++rocks
   :answer_d: Error, you cannot add two strings together.
   :correct: c
   :feedback_a: Concatenation does not automatically add a space.
   :feedback_b: The expression s+t is evaluated first, then the resulting string is printed.
   :feedback_c: Yes, the two strings are glued end to end.
   :feedback_d: The + operator has different meanings depending on the operands, in this case, two strings.


   What is printed by the following statements?

   .. code-block:: cpp

      string s = "C++";
      string t = "rocks";
      cout << s + t << endl;

.. parsonsprob:: question_seven_five

   As an exercise, put together the code below so that it prints ``C++ is so fun!""
   -----
   int main() {
   -----
      string language = "C++";
      string action = " is so ";
      string adjective = "fun!";
   -----
      string language = "C++"; #distractor
      string action = "is so";
      string adjective = "fun!";
   -----
      cout << language + action + adjective << endl;
   -----
      cout << "language" + "action" + "adjective" << endl; #distractor
   -----
   }
