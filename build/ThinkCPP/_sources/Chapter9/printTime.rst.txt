``printTime``
-------------

When we define a new type it is a good idea to write function that
displays the instance variables in a human-readable form, which you attempted on the page before. Your solution should have looked something like this.

::

   void printTime (Time& t) {
     cout << t.hour << ":" << t.minute << ":" << t.second << endl;
   }

The output of this function, if we pass ``time`` an argument, is
``11:59:3.14159``.

.. activecode:: ninethree
  :language: cpp

   #include <iostream>
   using namespace std;

   struct Time {
     int hour, minute;
     double second;
   };


   void printTime (Time& t) {
     cout << t.hour << ":" << t.minute << ":" << t.second << endl;
     cout << "Time is " << t.hour << " hour " << t.minute << " minutes " << t.second << " seconds  "<<endl;
   }


   int main ()
   {
    Time time = { 11, 59, 3.14159 };
    printTime(time);

    return 0;
   }


.. mchoice:: question_nine_four
   :multiple_answers:
   :answer_a: cout << "Price is " << "p.dollar" << " dollars and" << "p.cents" << "cents." << endl;
   :answer_b: cout << "Price is " << p.dollar << " dollars and" << p.cents << "cents." << endl;
   :answer_c: cout << "Price is " << p.dollar << " dollars and" << p.cents << "cents." << endl
   :correct: b
   :feedback_a: Try again.
   :feedback_b: Correct!
   :feedback_c: There is an important character that ends nearly all statements in C++.

   Which of the following would be a correct way to display the price of an object and finish the printPrice, which we saw on the previous page?

   .. code-block:: cpp

      struct Price {
        int dollar, cents;
      };

      void printPrice(Price& p) {

      }

      int main() {
        Price sandwich = { 3, 45 };
        Price coffee = { 2, 50 };
        Price pastry = { 2, 0 };
      }
