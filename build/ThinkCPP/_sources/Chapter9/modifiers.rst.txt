Modifiers
---------

Of course, sometimes you *want* to modify one of the arguments.
Functions that do are called modifiers.

As an example of a modifier, consider ``increment``, which adds a given
number of seconds to a ``Time`` object. Again, a rough draft of this
function looks like:

::

   void increment (Time& time, double secs) {
     time.second += secs;

     if (time.second >= 60.0) {
       time.second -= 60.0;
       time.minute += 1;
     }
     if (time.minute >= 60) {
       time.minute -= 60;
       time.hour += 1;
     }
   }

The first line performs the basic operation; the remainder deals with
the special cases we saw before.

Is this function correct? What happens if the argument ``secs`` is much
greater than 60? In that case, it is not enough to subtract 60 once; we
have to keep doing it until ``second`` is below 60. We can do that by
replacing the ``if`` statements with ``while`` statements:


.. activecode:: nineseven
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

   void increment (Time& time, double secs) {
     time.second += secs;

     while (time.second >= 60.0) {
       time.second -= 60.0;
       time.minute += 1;
     }
     while (time.minute >= 60) {
       time.minute -= 60;
       time.hour += 1;
     }
   }

   int main() {
     Time currentTime = { 9, 14, 30.0 };
     increment(currentTime, 60.0);
     printTime (currentTime);
    }

This solution is correct, but not very efficient. Can you think of a
solution that does not require iteration? Try it in the space below:

.. activecode:: nineeight
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

   void increment (Time& time, double secs) {

   }

   int main() {
     Time currentTime = { 9, 14, 30.0 };
     increment(currentTime, 60.0);
     printTime (currentTime);
    }
