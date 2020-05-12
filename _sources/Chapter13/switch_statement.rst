``switch`` statement
--------------------

It’s hard to mention enumerated types without mentioning ``switch``
statements, because they often go hand in hand. A ``switch`` statement
is an alternative to a chained conditional that is syntactically
prettier and often more efficient. It looks like this:

::

     switch (symbol) {
     case '+':
       perform_addition ();
       break;
     case '*':
       perform_multiplication ();
       break;
     default:
       cout << "I only know how to perform addition and multiplication" << endl;
       break;
     }

This ``switch`` statement is equivalent to the following chained
conditional:

::

     if (symbol == '+') {
       perform_addition ();
     } else if (symbol == '*') {
       perform_multiplication ();
     } else {
       cout << "I only know how to perform addition and multiplication" << endl;
     }

The ``break`` statements are necessary in each branch in a ``switch``
statement because otherwise the flow of execution “falls through” to the
next case. Without the ``break`` statements, the symbol ``+`` would make
the program perform addition, and then perform multiplication, and then
print the error message. Occasionally this feature is useful, but most
of the time it is a source of errors when people forget the ``break``
statements.

Take a look at the active code below that allows you to choose your starter Pokemon.
If you change the value of ``type``, it will change the Pokemon you choose. Notice how 
if you don't assign ``type`` to a valid type, it outputs the default message. Try taking out
the ``break`` statements in each case. What happens if you run the code with ``type`` as 'g' afterwards?

.. activecode:: thirteentwo
   :language: cpp

   #include <iostream>
   #include <string>
   using namespace std;

   int main() {
     char type = 'w';

     switch (type) {
     case 'g':
       cout << "You've chosen Bulbasaur!" << endl;
       break;
     case 'f':
       cout << "You've chosen Charmander!" << endl;
       break;
     case 'w':
       cout << "You've chosen Squirtle!" << endl;
       break;
     default:
       cout << "Invalid type! Please try again." << endl;
       break;
     }
   }

``switch`` statements work with integers, characters, and enumerated
types. For example, to convert a ``Suit`` to the corresponding string,
we could use something like:

::

     switch (suit) {
     case CLUBS:     return "Clubs";
     case DIAMONDS:  return "Diamonds";
     case HEARTS:    return "Hearts";
     case SPADES:    return "Spades";
     default:        return "Not a valid suit";
     }

In this case we don’t need ``break`` statements because the ``return``
statements cause the flow of execution to return to the caller instead
of falling through to the next case.

In general it is good style to include a ``default`` case in every
``switch`` statement, to handle errors or unexpected values.

.. _deck:

.. fillintheblank:: question13_2_1

    What statement is necessary for each branch in a ``switch`` statements?

    - :break: Correct!
      :.*: Incorrect! How do we prevent the flow of execution from "falling through?"

.. mchoice:: question13_2_2
   :answer_a: ints
   :answer_b: chars
   :answer_c: strings
   :answer_d: enumerated types
   :correct: c
   :feedback_a: Incorrect! We can use ints with switch statements.
   :feedback_b: Incorrect! We can use chars with switch statements.
   :feedback_c: Correct! We cannot use strings with switch statements!
   :feedback_d: Incorrect! We can use enumerated types with switch statements.

   Which one of the following types do NOT work with ``switch`` statement?