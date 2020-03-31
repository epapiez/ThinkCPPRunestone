Call by reference
-----------------

An alternative parameter-passing mechanism that is available in C++ is
called “pass by reference.” This mechanism makes it possible to pass a
structure to a procedure and modify it.

For example, you can reflect a point around the 45-degree line by
swapping the two coordinates. The most obvious (but incorrect) way to
write a ``reflect`` function is something like this:

::

   void reflect (Point p)      // WRONG !!
   {
     double temp = p.x;
     p.x = p.y;
     p.y = temp;
   }

But this won’t work, because the changes we make in ``reflect`` will
have no effect on the caller.

Instead, we have to specify that we want to pass the parameter by
reference. We do that by adding an ampersand (``&``) to the parameter
declaration:

::

   void reflect (Point& p)
   {
     double temp = p.x;
     p.x = p.y;
     p.y = temp;
   }

Now we can call the function in the usual way:

::

     printPoint (blank);
     reflect (blank);
     printPoint (blank);

The output of this program is as expected:

.. activecode:: eightone
  :language: cpp


    #include <iostream>
    using namespace std;

    struct Point {
      double x, y;
    };

    void reflect (Point& p)
    {
      double temp = p.x;
      p.x = p.y;
      p.y = temp;
    }

    void printPoint (Point p) {
      cout << "(" << p.x << ", " << p.y << ")" << endl;
    }

    int main() {
      Point blank = { 3.0, 4.0 };
      printPoint (blank);
      reflect (blank);
      printPoint (blank);
    }

::

   (3, 4)
   (4, 3)


The parameter ``p`` is a reference to the structure named ``blank``. The
usual representation for a reference is a dot with an arrow that points
to whatever the reference refers to.

The important thing to see in this diagram is that any changes that
``reflect`` makes in ``p`` will also affect ``blank``.

Passing structures by reference is more versatile than passing by value,
because the callee can modify the structure. It is also faster, because
the system does not have to copy the whole structure. On the other hand,
it is less safe, since it is harder to keep track of what gets modified
where. Nevertheless, in C++ programs, almost all structures are passed
by reference almost all the time. In this book I will follow that
convention.
