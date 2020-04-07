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
