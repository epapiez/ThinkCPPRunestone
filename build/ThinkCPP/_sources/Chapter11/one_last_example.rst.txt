One last example
----------------

The final example we’ll look at is ``addTime``:

::

   Time addTime2 (const Time& t1, const Time& t2) {
     double seconds = convertToSeconds (t1) + convertToSeconds (t2);
     return makeTime (seconds);
   }

We have to make several changes to this function, including:

#. Change the name from ``addTime`` to ``Time::add``.

#. Replace the first parameter with an implicit parameter, which should
   be declared ``const``.

#. Replace the use of ``makeTime`` with a constructor invocation.

Here’s the result:

::

   Time Time::add (const Time& t2) const {
     double seconds = convertToSeconds () + t2.convertToSeconds ();
     Time time (seconds);
     return time;
   }

The first time we invoke ``convertToSeconds``, there is no apparent
object! Inside a member function, the compiler assumes that we want to
invoke the function on the current object. Thus, the first invocation
acts on ``this``; the second invocation acts on ``t2``.

The next line of the function invokes the constructor that takes a
single ``double`` as a parameter; the last line returns the resulting
object.
