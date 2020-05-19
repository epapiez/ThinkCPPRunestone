Private functions
-----------------

In some cases, there are member functions that are used internally by a
class, but that should not be invoked by client programs. For example,
``calculatePolar`` and ``calculateCartesian`` are used by the accessor
functions, but there is probably no reason clients should call them
directly (although it would not do any harm). If we wanted to protect
these functions, we could declare them ``private`` the same way we do
with instance variables. In that case the complete class definition for
``Complex`` would look like:

::

   class Complex
   {
   private:
     double real, imag;
     double mag, theta;
     bool cartesian, polar;

     void calculateCartesian ();
     void calculatePolar ();

   public:
     Complex () { cartesian = false;  polar = false; }

     Complex (double r, double i)
     {
       real = r;  imag = i;
       cartesian = true;  polar = false;
     }

     void printCartesian ();
     void printPolar ();

     double getReal ();
     double getImag ();
     double getMag ();
     double getTheta ();

     void setCartesian (double r, double i);
     void setPolar (double m, double t);
   };

The ``private`` label at the beginning is not necessary, but it is a
useful reminder.