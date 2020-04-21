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

.. mchoice:: question11_3_1
   :answer_a: after being granted permission
   :answer_b: only inside of that specific member function
   :answer_c: using dot notation
   :answer_d: directly, without dot notation
   :correct: d
   :feedback_a: Incorrect! You don't need "permission" to access member variables inside a member function.
   :feedback_b: Incorrect! You can access member variables implicitly inside any and all member functions.
   :feedback_c: Incorrect! You don't need to use dot notation to access variables implicitly.
   :feedback_d: Correct! Implicit variable access allows us to access variables directly-- without using dot notation.

   Implicit variable access in member functions allows us to access member variables __________.