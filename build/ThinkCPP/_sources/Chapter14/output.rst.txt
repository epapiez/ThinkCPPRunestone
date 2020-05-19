Output
------

As usual when we define a new class, we want to be able to output
objects in a human-readable form. For ``Complex`` objects, we could use
two functions:

::

   void Complex::printCartesian ()
   {
     cout << getReal() << " + " << getImag() << "i" << endl;
   }

   void Complex::printPolar ()
   {
     cout << getMag() << " e^ " << getTheta() << "i" << endl;
   }

The nice thing here is that we can output any ``Complex`` object in
either format without having to worry about the representation. Since
the output functions use the accessor functions, the program will
compute automatically any values that are needed.

The following code creates a ``Complex`` object using the second
constructor. Initially, it is in Cartesian format only. When we invoke
``printCartesian`` it accesses ``real`` and ``imag`` without having to
do any conversions.

::

     Complex c1 (2.0, 3.0);

     c1.printCartesian();
     c1.printPolar();

When we invoke ``printPolar``, and ``printPolar`` invokes ``getMag``,
the program is forced to convert to polar coordinates and store the
results in the instance variables. The good news is that we only have to
do the conversion once. When ``printPolar`` invokes ``getTheta``, it
will see that the polar coordinates are valid and return ``theta``
immediately.

The output of this code is:

::

   2 + 3i
   3.60555 e^ 0.982794i