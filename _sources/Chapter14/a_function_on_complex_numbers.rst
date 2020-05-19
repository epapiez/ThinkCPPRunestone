A function on ``Complex`` numbers
---------------------------------

A natural operation we might want to perform on complex numbers is
addition. If the numbers are in Cartesian coordinates, addition is easy:
you just add the real parts together and the imaginary parts together.
If the numbers are in polar coordinates, it is easiest to convert them
to Cartesian coordinates and then add them.

Again, it is easy to deal with these cases if we use the accessor
functions:

::

   Complex add (Complex& a, Complex& b)
   {
     double real = a.getReal() + b.getReal();
     double imag = a.getImag() + b.getImag();
     Complex sum (real, imag);
     return sum;
   }

Notice that the arguments to ``add`` are not ``const`` because they
might be modified when we invoke the accessors. To invoke this function,
we would pass both operands as arguments:

::

     Complex c1 (2.0, 3.0);
     Complex c2 (3.0, 4.0);

     Complex sum = add (c1, c2);
     sum.printCartesian();

The output of this program is

::

   5 + 7i