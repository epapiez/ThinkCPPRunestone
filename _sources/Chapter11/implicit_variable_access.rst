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

    True or False: We need to create a local variable and use dot notation in order to refer to the instance variables of the current object inside of a member function.

    - :([Ff]alse|FALSE): Correct! The member function has implicit variable access, thus, instance variables can be referenced directly inside of the member function.
      :.*: Incorrect! Remember, the member function has implicit variable access!
