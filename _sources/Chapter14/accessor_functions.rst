Accessor functions
------------------

By convention, accessor functions have names that begin with ``get`` and
end with the name of the instance variable they fetch. The return type,
naturally, is the type of the corresponding instance variable.

In this case, the accessor functions give us an opportunity to make sure
that the value of the variable is valid before we return it. Here’s what
``getReal`` looks like:

::

   double Complex::getReal ()
   {
     if (cartesian == false) calculateCartesian ();
     return real;
   }

If the ``cartesian`` flag is true then ``real`` contains valid data, and
we can just return it. Otherwise, we have to call ``calculateCartesian``
to convert from polar coordinates to Cartesian coordinates:

::

   void Complex::calculateCartesian ()
   {
     real = mag * cos (theta);
     imag = mag * sin (theta);
     cartesian = true;
   }

Assuming that the polar coordinates are valid, we can calculate the
Cartesian coordinates using the formulas from the previous section. Then
we set the ``cartesian`` flag, indicating that ``real`` and ``imag`` now
contain valid data.

As an exercise, write a corresponding function called ``calculatePolar``
and then write ``getMag`` and ``getTheta``. One unusual thing about
these accessor functions is that they are not ``const``, because
invoking them might modify the instance variables.

Take a look at the active code below, which uses the ``getReal``
accessor function. 

.. activecode:: fourteenfour
   :language: cpp

   #include <iostream>
   #include <cmath>
   using namespace std;

   class Complex
   {
     double real, imag;
     double mag, theta;
     bool cartesian, polar;

   public:
     Complex () { cartesian = false;  polar = false; }
     Complex (double r, double i)
     {
       real = r;  imag = i;
       cartesian = true;  polar = false;
     }
     void calculateCartesian ()
     {
       real = mag * cos (theta);
       imag = mag * sin (theta);
       cartesian = true;
     }
     double getReal ()
     {
       if (cartesian == false) calculateCartesian ();
       return real;
     }
   };

   int main() {
     Complex c1 (5, 3.5);
     cout << c1.getReal() << endl;
   }

Write your implementation of ``calculatePolar`` in the commented area of the active 
code below. Once you're done with that, write the ``getMag`` and ``getTheta`` 
accessor functions. Read the comments in ``main`` to see how we'll test if your
functions works. If you get stuck, you can reveal the extra problem at the end for help. 

.. activecode:: fourteenfive
   :language: cpp

   #include <iostream>
   #include <cmath>
   using namespace std;

   class Complex
   {
     double real, imag;
     double mag, theta;
     bool cartesian, polar;

   public:
     Complex ();
     Complex (double r, double i);
     void calculateCartesian ();
     double getReal ();
   };

   void Complex::calculatePolar () {
     // ``calculatePolar`` should convert the real and imaginary parts
     // into magnitude and theta. Use the formula in the previous section.
     // Write your implementation here.
   }

   double Complex::getMag () {
     // ``getMag`` should return the magnitude.
     // Write your implementation here.
   }

   void Complex::getTheta () {
     // ``getMag`` should return the theta.
     // Write your implementation here.
   }

   int main() {
     Complex c1 (5, 3.5);
     cout << c1.getReal() << endl;
   }
   ====
   Complex () { cartesian = false;  polar = false; }

   Complex (double r, double i) {
     real = r;  imag = i;
     cartesian = true;  polar = false;
   }

   void calculateCartesian () {
     real = mag * cos (theta);
     imag = mag * sin (theta);
     cartesian = true;
   }

   double getReal () {
     if (cartesian == false) calculateCartesian ();
     return real;
   }