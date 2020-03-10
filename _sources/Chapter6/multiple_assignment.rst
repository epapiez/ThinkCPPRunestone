Multiple assignment
-------------------

I haven’t said much about it, but it is legal in C++ to make more than
one assignment to the same variable. The effect of the second assignment
is to replace the old value of the variable with a new value.

.. activecode:: sixone
  :language: cpp
  :caption: Multiple assignment

  #include <iostream>
  using namespace std;

    int main ()
    {

     int fred = 5;
     cout << fred;
     fred = 7;
     cout << fred;
     return 0;
    }

The output of this program is ``57``, because the first time we print
``fred`` his value is 5, and the second time his value is 7.

.. activecode:: sixtwo
  :language: cpp
  :caption: Multiple assignment

  #include <iostream>
  using namespace std;

    int main ()
    {

     int fred = 5;
     fred = 7;
     cout << fred;
     return 0;
    }

However, if we do not print ``fred`` the first time, the output is only 7 because
the value of ``fred`` is just 7 when it is printed.

This kind of **multiple assignment** is the reason I described variables
as a *container* for values. When you assign a value to a variable, you
change the contents of the container, as shown in the figure:

When there are multiple assignments to a variable, it is especially
important to distinguish between an assignment statement and a statement
of equality. Because C++ uses the ``=`` symbol for assignment, it is
tempting to interpret a statement like ``a = b`` as a statement of
equality. It is not!

First of all, equality is commutative, and assignment is not. For
example, in mathematics if :math:`a = 7` then :math:`7 = a`. But in C++
the statement ``a = 7;`` is legal, and ``7 = a;`` is not.

Furthermore, in mathematics, a statement of equality is true for all
time. If :math:`a = b` now, then :math:`a` will always equal :math:`b`.
In C++, an assignment statement can make two variables equal, but they
don’t have to stay that way!

::

     int a = 5;
     int b = a;     // a and b are now equal
     a = 3;         // a and b are no longer equal

The third line changes the value of ``a`` but it does not change the
value of ``b``, and so they are no longer equal. In many programming
languages an alternate symbol is used for assignment, such as ``<-`` or
``:=``, in order to avoid confusion.

Although multiple assignment is frequently useful, you should use it
with caution. If the values of variables are changing constantly in
different parts of the program, it can make the code difficult to read
and debug.

.. dragndrop:: dragndrop_six_one
    :feedback: Try again!
    :match_1:  4=a|||Illegal
    :match_2: a==b|||Checking if a is equal to b
    :match_3: a=b|||Assigning a to the value of b
    :match_4: a=4|||Setting the value of a to 4

    Match the expression to the statement that best describes it.
