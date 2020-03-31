Encapsulation and generalization
--------------------------------

Encapsulation usually means taking a piece of code and wrapping it up in
a function, allowing you to take advantage of all the things functions
are good for. We have seen two examples of encapsulation, when we wrote
``printParity`` in Section `[alternative] <#alternative>`__ and
``isSingleDigit`` in Section `[bool] <#bool>`__.

Generalization means taking something specific, like printing multiples
of 2, and making it more general, like printing the multiples of any
integer.

Here’s a function that encapsulates the loop from the previous section
and generalizes it to print multiples of ``n``.

::

   void printMultiples (int n)
   {
     int i = 1;
     while (i <= 6) {
       cout << n*i << "   ";
       i = i + 1;
     }
     cout << endl;
   }

To encapsulate, all I had to do was add the first line, which declares
the name, parameter, and return type. To generalize, all I had to do was
replace the value 2 with the parameter ``n``.

If we call this function with the argument 2, we get the same output as
before. With argument 3, the output is:

::

   3   6   9   12   15   18

and with argument 4, the output is

::

   4   8   12   16   20   24

By now you can probably guess how we are going to print a multiplication
table: we’ll call ``printMultiples`` repeatedly with different
arguments. In fact, we are going to use another loop to iterate through
the rows.

::

     int i = 1;
     while (i <= 6) {
       printMultiples (i);
       i = i + 1;
     }

First of all, notice how similar this loop is to the one inside
``printMultiples``. All I did was replace the print statement with a
function call.


.. activecode:: sixseven
  :language: cpp
  :caption: Two-dimensional tables

  #include <iostream>
  using namespace std;

  void printMultiples (int n)
  {
    int i = 1;
    while (i <= 6) {
      cout << n*i << "   ";
      i = i + 1;
    }
    cout << endl;
  }

  int main() {
    int i = 1;
    while (i <= 6) {
      printMultiples (i);
      i = i + 1;
    }
  }

The output of this program is

::

   1   2   3   4   5   6
   2   4   6   8   10   12
   3   6   9   12   15   18
   4   8   12   16   20   24
   5   10   15   20   25   30
   6   12   18   24   30   36

which is a (slightly sloppy) multiplication table. If the sloppiness
bothers you, you can also use tab characters, like below.

.. activecode:: sixeight
  :language: cpp
  :caption: Two-dimensional tables

  #include <iostream>
  using namespace std;

  void printMultiples (int n)
  {
    int i = 1;
    while (i <= 6) {
      cout << n*i << '\t';
      i = i + 1;
    }
    cout << endl;
  }

  int main() {
    int i = 1;
    while (i <= 6) {
      printMultiples (i);
      i = i + 1;
    }
  }
