Accessing instance variables
----------------------------

You can read the values of an instance variable using the same syntax we
used to write them:

::

       int x = blank.x;

The expression ``blank.x`` means “go to the object named ``blank`` and
get the value of ``x``.” In this case we assign that value to a local
variable named ``x``. Notice that there is no conflict between the local
variable named ``x`` and the instance variable named ``x``. The purpose
of dot notation is to identify *which* variable you are referring to
unambiguously.

You can use dot notation as part of any C++ expression, so the following
are legal.

::

     cout << blank.x << ", " << blank.y << endl;
     double distance = blank.x * blank.x + blank.y * blank.y;

The first line outputs ``3, 4``; the second line calculates the value
25.
