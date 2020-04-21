``string`` variables
--------------------

You can create a variable with type ``string`` in the usual ways:

.. activecode:: sevenone
  :language: cpp
  :caption: Creating a string variable

  #include <iostream>
  using namespace std;

  int main() {
     string first;
     first = "Hello, ";
     string second = "world.";
  }

The first line creates a ``string`` without giving it a value. The
second line assigns it the string value ``"Hello."`` The third line is a
combined declaration and assignment, also called an initialization.

Normally when string values like ``"Hello, "`` or ``"world."`` appear,
they are treated as C strings. In this case, when we assign them to an
``string`` variable, they are converted automatically to ``string``
values.

We can output strings in the usual way:

::

     cout << first << second << endl;

In order to compile this code, you will have to include the header file
for the ``string`` class, and you will have to add the file ``string``
to the list of files you want to compile. The details of how to do this
depend on your programming environment.

Before proceeding, you should type in the program above and make sure
you can compile and run it.

.. activecode:: seventwo
  :language: cpp
  :caption: Outputting a string variable

  #include <iostream>
  using namespace std;

  int main() {
     string first;
     first = "Hello, ";
     string second = "world.";
     cout << first << second << endl;
  }

.. parsonsprob:: question_seven_one

   Construct a block of code that correctly prints out a string variable.
   -----
   string x;

   x = "It is cold outside!";

   x = "It is cold outside" #paired

   cout << x << endl;


.. mchoice:: test_question_seven_one__
   :practice: T
   :answer_a: string x = "Hello";
   :answer_b: x = "Hello";
   :answer_c: string x;
   :correct: a
   :feedback_a: Correct!
   :feedback_b: This is an assignment.
   :feedback_c: This is a declaration.


   How would you initialize a string?


.. clickablearea:: click_seven_one__
    :question: Click on each spot where a string assignment occurs.
    :iscode:
    :feedback: Remember, square brackets [] are used to access a character in a string.

    :click-incorrect:def main() {:endclick:
        :click-incorrect:string fruit;:endclick:
        :click-correct:fruit = "apple";:endclick:
        :click-correct:fruit = "pear";:endclick:
        :click-incorrect:string flavor;:endclick:
        :click-correct:flavor = "vanilla";:endclick:
      }
