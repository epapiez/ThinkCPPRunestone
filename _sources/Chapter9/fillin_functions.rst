Fill-in functions
-----------------

Occasionally you will see functions like ``addTime`` written with a
different interface (different arguments and return values). Instead of
creating a new object every time ``addTime`` is called, we could require
the caller to provide an “empty” object where ``addTime`` can store the
result. Compare the following with the previous version:

::

   void addTimeFill (const Time& t1, const Time& t2, Time& sum) {
     sum.hour = t1.hour + t2.hour;
     sum.minute = t1.minute + t2.minute;
     sum.second = t1.second + t2.second;

     if (sum.second >= 60.0) {
       sum.second -= 60.0;
       sum.minute += 1;
     }
     if (sum.minute >= 60) {
       sum.minute -= 60;
       sum.hour += 1;
     }
   }

One advantage of this approach is that the caller has the option of
reusing the same object repeatedly to perform a series of additions.
This can be slightly more efficient, although it can be confusing enough
to cause subtle errors. For the vast majority of programming, it is
worth a spending a little run time to avoid a lot of debugging time.

.. mchoice:: question_nine_six
   :multiple_answers:
   :answer_a: Time& t1
   :answer_b: Time& t2
   :answer_c: Time& sum
   :correct: c
   :feedback_a: Try again.
   :feedback_b: Try again.
   :feedback_c: Correct!

   Which parameter is not declared as a ``const``?

   .. code-block:: cpp

      void addTimeFill (const Time& t1, const Time& t2, Time& sum) {
        sum.hour = t1.hour + t2.hour;
        sum.minute = t1.minute + t2.minute;
        sum.second = t1.second + t2.second;

        if (sum.second >= 60.0) {
          sum.second -= 60.0;
          sum.minute += 1;
        }
        if (sum.minute >= 60) {
          sum.minute -= 60;
          sum.hour += 1;
        }
      }
