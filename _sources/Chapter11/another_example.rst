Another example
---------------

Let’s convert ``increment`` to a member function. Again, we are going to
transform one of the parameters into the implicit parameter called
``this``. Then we can go through the function and make all the variable
accesses implicit.

::

   void Time::increment (double secs) {
     second += secs;

     while (second >= 60.0) {
       second -= 60.0;
       minute += 1;
     }
     while (minute >= 60) {
       minute -= 60.0;
       hour += 1;
     }
   }

By the way, remember that this is not the most efficient implementation
of this function. If you didn’t do it back in
Chapter `[time] <#time>`__, you should write a more efficient version
now.

To declare the function, we can just copy the first line into the
structure definition:

::

   struct Time {
     int hour, minute;
     double second;

     print ();
     increment (double secs);
   };

And again, to call it, we have to invoke it on a ``Time`` object:

::

     Time currentTime = { 9, 14, 30.0 };
     currentTime.increment (500.0);
     currentTime.print ();

The output of this program is ``9:22:50``.

Let's try changing the input!

.. activecode:: 11_4
   :language: cpp

   #include <iostream>
   using namespace std;

   struct Time {
     int hour, minute;
     double second;
     void print ();
     void increment (double secs);
   };

   int main() {
     Time currentTime = { 9, 14, 30.0 };
     currentTime.increment (500.0);
     currentTime.print ();
   }

   ====
   void Time::print () {
     cout << hour << ":" << minute << ":" << second << endl;
   }

   void Time::increment (double secs) {
     second += secs;
     while (second >= 60.0) {
       second -= 60.0;
       minute += 1;
     }
     while (minute >= 60) {
       minute -= 60.0;
       hour += 1;
     }
   }

.. fillintheblank:: question11_4_1

    Suppose we have previously declared ``Time currentTime = {9, 14, 30.0}``.  What should be printed by ``time.print()`` after calling ``time.increment(645.0)``? Type your response in the form **hh:mm:ss**.
    
    - :(9:25:15): Correct!
      :.*: Incorrect! Try plugging the given input into the active code above!

.. fillintheblank:: question11_4_2

    When we call a member function, we __________ the function on the data structure.
    
    - :([Ii]nvoke)|(INVOKE): Correct!
      :.*: Incorrect! Try reading the past few pages again!
