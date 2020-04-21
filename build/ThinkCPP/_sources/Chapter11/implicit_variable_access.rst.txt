Implicit variable access
------------------------

Actually, the new version of ``Time::print`` is more complicated than it
needs to be. We don’t really need to create a local variable in order to
refer to the instance variables of the current object.

If the function refers to ``hour``, ``minute``, or ``second``, all by
themselves with no dot notation, C++ knows that it must be referring to
the current object. So we could have written:

::

   void Time::print ()
   {
     cout << hour << ":" << minute << ":" << second << endl;
   }

This kind of variable access is called “implicit” because the name of
the object does not appear explicitly. Features like this are one reason
member functions are often more concise than nonmember functions.

.. fillintheblank:: question11_3_1

    When we refer to the instance variables of objects without dot notation, we are using __________ variable acccess.

    - :([Ii]mplicit|IMPLICIT): Correct! Implicit variable access is one reason why member functions are more concise than free-standing functions!
      :.*: Incorrect, try again!