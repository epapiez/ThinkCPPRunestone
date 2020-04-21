Incremental development versus planning
---------------------------------------

In this chapter I have demonstrated an approach to program development I
refer to as **rapid prototyping with iterative improvement**. In each
case, I wrote a rough draft (or prototype) that performed the basic
calculation, and then tested it on a few cases, correcting flaws as I
found them.

Although this approach can be effective, it can lead to code that is
unnecessarily complicated—since it deals with many special cases—and
unreliable—since it is hard to know if you have found all the errors.

An alternative is high-level planning, in which a little insight into
the problem can make the programming much easier. In this case the
insight is that a ``Time`` is really a three-digit number in base 60!
The ``second`` is the “ones column,” the ``minute`` is the “60’s
column”, and the ``hour`` is the “3600’s column.”

When we wrote ``addTime`` and ``increment``, we were effectively doing
addition in base 60, which is why we had to “carry” from one column to
the next.

Thus an alternate approach to the whole problem is to convert
``Time``\ s into ``double``\ s and take advantage of the fact that the
computer already knows how to do arithmetic with ``double``\ s. Here is
a function that converts a ``Time`` into a ``double``:

::

   double convertToSeconds (const Time& t) {
     int minutes = t.hour * 60 + t.minute;
     double seconds = minutes * 60 + t.second;
     return seconds;
   }

Now all we need is a way to convert from a ``double`` to a ``Time``
object:

::

   Time makeTime (double secs) {
     Time time;
     time.hour = int (secs / 3600.0);
     secs -= time.hour * 3600.0;
     time.minute = int (secs / 60.0);
     secs -= time.minute * 60;
     time.second = secs;
     return time;
   }

You might have to think a bit to convince yourself that the technique I
am using to convert from one base to another is correct. Assuming you
are convinced, we can use these functions to rewrite ``addTime``:

::

   Time addTime (const Time& t1, const Time& t2) {
     double seconds = convertToSeconds (t1) + convertToSeconds (t2);
     return makeTime (seconds);
   }


.. activecode:: nineten
  :language: cpp

   #include <iostream>
   using namespace std;

   struct Time {
     int hour, minute;
     double second;
   };

   double convertToSeconds (const Time& t) {
     int minutes = t.hour * 60 + t.minute;
     double seconds = minutes * 60 + t.second;
     return seconds;
   }

   Time makeTime (double secs) {
     Time time;
     time.hour = int (secs / 3600.0);
     secs -= time.hour * 3600.0;
     time.minute = int (secs / 60.0);
     secs -= time.minute * 60;
     time.second = secs;
     return time;
   }

   Time addTime (const Time& t1, const Time& t2) {
     double seconds = convertToSeconds (t1) + convertToSeconds (t2);
     return makeTime (seconds);
   }

   int main() {
     Time currentTime = { 9, 14, 30.0 };
     Time otherTime = { 10, 32, 15.2 };
     doneTime = addTime(currentTime, otherTime);
     printTime (doneTime);
    }



This is much shorter than the original version, and it is much easier to
demonstrate that it is correct (assuming, as usual, that the functions
it calls are correct). As an exercise, rewrite ``increment`` the same
way.
