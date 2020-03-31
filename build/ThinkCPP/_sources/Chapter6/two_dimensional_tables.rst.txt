Two-dimensional tables
----------------------

A two-dimensional table is a table where you choose a row and a column
and read the value at the intersection. A multiplication table is a good
example. Let’s say you wanted to print a multiplication table for the
values from 1 to 6.

A good way to start is to write a simple loop that prints the multiples
of 2, all on one line.

.. activecode:: sixsix
  :language: cpp
  :caption: Two-dimensional tables

  #include <iostream>
  using namespace std;

  int main() {
     int i = 1;
     while (i <= 6) {
       cout << 2*i << "   ";
       i = i + 1;
     }
     cout << endl;
     return 0;
  }

The first line initializes a variable named ``i``, which is going to act
as a counter, or **loop variable**. As the loop executes, the value of
``i`` increases from 1 to 6, and then when ``i`` is 7, the loop
terminates. Each time through the loop, we print the value ``2*i``
followed by three spaces. By omitting the ``endl`` from the first output
statement, we get all the output on a single line.

The output of this program is:

::

   2   4   6   8   10   12

So far, so good. The next step is to **encapsulate** and **generalize**.
