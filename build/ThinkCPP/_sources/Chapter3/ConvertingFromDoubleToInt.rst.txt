Converting from double to int
-----------------------------

As I mentioned, C++ converts ints to doubles automatically if necessary,
because no information is lost in the translation. On the other hand,
going from a double to an int requires rounding off. C++ doesn’t perform
this operation automatically, in order to make sure that you, as the
programmer, are aware of the loss of the fractional part of the number.

The simplest way to convert a floating-point value to an integer is to
use a **typecast**. Typecasting is so called because it allows you to
take a value that belongs to one type and “cast” it into another type
(in the sense of molding or reforming, not throwing).

The syntax for typecasting is like the syntax for a function call. For
example:

::

      double pi = 3.14159;
      int x = int (pi);

The int function returns an integer, so x gets the value 3. Converting
to an integer always rounds down, even if the fraction part is
0.99999999.

For every type in C++, there is a corresponding function that typecasts
its argument to the appropriate type.

**Convert this double to an int. Then use a print statement to observe the output!***

.. activecode:: threeone
  :language: cpp
  :caption: Double to int

  #include <iostream>
  using namespace std;

    int main ()
    {
      double price = 6.98;
      int sale_price = ;
      cout << sale_price;
      return 0;
    }
