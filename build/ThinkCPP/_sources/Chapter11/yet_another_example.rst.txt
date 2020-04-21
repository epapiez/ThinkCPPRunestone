Yet another example
-------------------

The original version of ``convertToSeconds`` looked like this:

::

   double convertToSeconds (const Time& time) {
     int minutes = time.hour * 60 + time.minute;
     double seconds = minutes * 60 + time.second;
     return seconds;
   }

It is straightforward to convert this to a member function:

::

   double Time::convertToSeconds () const {
     int minutes = hour * 60 + minute;
     double seconds = minutes * 60 + second;
     return seconds;
   }

The interesting thing here is that the implicit parameter should be
declared ``const``, since we don’t modify it in this function. But it is
not obvious where we should put information about a parameter that
doesn’t exist. The answer, as you can see in the example, is after the
parameter list (which is empty in this case).

The ``print`` function in the previous section should also declare that
the implicit parameter is ``const``.

.. mchoice:: question11_5
   :answer_a: Before the parameter list.
   :answer_b: Inside the parameter list.
   :answer_c: After the parameter list.
   :answer_d: Implicit parameters are always const and don't need to be declared.
   :correct: c
   :feedback_a: Incorrect! Try again!
   :feedback_b: Incorrect! This would be correct if we were talking about a free-standing function.
   :feedback_c: Correct!
   :feedback_d: Incorrect! Parameters are only const if they are not modified inside the function, implicit parameters are no exception.

   When writing a member function, where should you declare the implicit parameter to be ``const``?