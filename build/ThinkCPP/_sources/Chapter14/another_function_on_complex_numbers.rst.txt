Another function on ``Complex`` numbers
---------------------------------------

Another operation we might want is multiplication. Unlike addition,
multiplication is easy if the numbers are in polar coordinates and hard
if they are in Cartesian coordinates (well, a little harder, anyway).

In polar coordinates, we can just multiply the magnitudes and add the
angles. As usual, we can use the accessor functions without worrying
about the representation of the objects.

::

   Complex mult (Complex& a, Complex& b)
   {
     double mag = a.getMag() * b.getMag()
     double theta = a.getTheta() + b.getTheta();
     Complex product;
     product.setPolar (mag, theta);
     return product;
   }

A small problem we encounter here is that we have no constructor that
accepts polar coordinates. It would be nice to write one, but remember
that we can only overload a function (even a constructor) if the
different versions take different parameters. In this case, we would
like a second constructor that also takes two ``double``\ s, and we
can’t have that.

An alternative it to provide an accessor function that *sets* the
instance variables. In order to do that properly, though, we have to
make sure that when ``mag`` and ``theta`` are set, we also set the
``polar`` flag. At the same time, we have to make sure that the
``cartesian`` flag is unset. That’s because if we change the polar
coordinates, the cartesian coordinates are no longer valid.

::

   void Complex::setPolar (double m, double t)
   {
     mag = m;  theta = t;
     cartesian = false;  polar = true;
   }

As an exercise, write the corresponding function named ``setCartesian``.

To test the ``mult`` function, we can try something like:

::

     Complex c1 (2.0, 3.0);
     Complex c2 (3.0, 4.0);

     Complex product = mult (c1, c2);
     product.printCartesian();

The output of this program is

::

   -6 + 17i

There is a lot of conversion going on in this program behind the scenes.
When we call ``mult``, both arguments get converted to polar
coordinates. The result is also in polar format, so when we invoke
``printCartesian`` it has to get converted back. Really, it’s amazing
that we get the right answer!