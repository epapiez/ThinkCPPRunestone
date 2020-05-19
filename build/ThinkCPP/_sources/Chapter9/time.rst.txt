Time
----

As a second example of a user-defined structure, we will define a type
called ``Time``, which is used to record the time of day. The various
pieces of information that form a time are the hour, minute and second,
so these will be the instance variables of the structure.

The first step is to decide what type each instance variable should be.
It seems clear that ``hour`` and ``minute`` should be integers. Just to
keep things interesting, let’s make ``second`` a ``double``, so we can
record fractions of a second.

Here’s what the structure definition looks like. We can create a ``Time`` object in the usual way:

.. activecode:: nineone
  :language: cpp

    #include <iostream>
    using namespace std;

    struct Time {
      int hour, minute;
      double second;
      };

    int main() {
        Time time = { 11, 59, 3.14159 };
        cout << time.hour << ":" << time.minute << ":" << time.second;
     }

The state diagram for this object looks like this:

.. figure:: Images/9.1stackdiagram.png
   :scale: 50%
   :align: center
   :alt: image

The word “instance” is sometimes used when we talk about objects,
because every object is an instance (or example) of some type. The
reason that instance variables are so-named is that every instance of a
type has a copy of the instance variables for that type.


.. mchoice:: question_nine_one
   :multiple_answers:
   :answer_a: sandwich, coffee, pastry
   :answer_b: dollar, cents
   :answer_c: Price, struct
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again.
   :feedback_c: Try again.

   Which of the following words are variables of type Price?

   .. code-block:: cpp

      struct Price {
        int dollar, cents;
      };

      int main() {
        Price sandwich = { 3, 45 };
        Price coffee = { 2, 50 };
        Price pastry = { 2, 0 };
      }

.. mchoice:: question_nine_two
   :multiple_answers:
   :answer_a: sandwich, coffee, pastry
   :answer_b: dollar, cents
   :answer_c: Price, struct
   :correct: b
   :feedback_a: These are variables of type Price.
   :feedback_b: Correct!
   :feedback_c: Try again.

   Which of the following words are instance variables of the Price structure?

   .. code-block:: cpp

      struct Price {
        int dollar, cents;
      };

      int main() {
        Price sandwich = { 3, 45 };
        Price coffee = { 2, 50 };
        Price pastry = { 2, 0 };
      }

.. mchoice:: question_nine_three
   :multiple_answers:
   :answer_a: sandwich, coffee, pastry
   :answer_b: dollar, cents
   :answer_c: Price
   :correct: c
   :feedback_a: These are variables of type Price.
   :feedback_b: These are instance variables of the Price structure.
   :feedback_c: Correct!

   Which of the following words are a user-defined structure?

   .. code-block:: cpp

      struct Price {
        int dollar, cents;
      };

      int main() {
        Price sandwich = { 3, 45 };
        Price coffee = { 2, 50 };
        Price pastry = { 2, 0 };
      }

**Complete the ``printTime`` function, which should print out the time in the HOUR:MINUTE:SECONDS format, just like above.**

.. activecode:: ninetwo
  :language: cpp

    #include <iostream>
    using namespace std;

    struct Time {
      int hour, minute;
      double second;
      };

    void printTime(Time& x) {

    }

    int main() {
        Time time = { 11, 59, 3.14159 };
        printTime(time);
     }
