Structures as parameters
------------------------

You can pass structures as parameters in the usual way. For example,

::

   void printPoint (Point p) {
     cout << "(" << p.x << ", " << p.y << ")" << endl;
   }

``printPoint`` takes a point as an argument and outputs it in the
standard format. If you call ``printPoint (blank)``, it will output
``(3, 4)``.

.. activecode:: eightone_two
  :language: cpp

    #include <iostream>
    using namespace std;

    struct Point {
      double x, y;
    };

    void printPoint (Point p) {
      cout << "(" << p.x << ", " << p.y << ")" << endl;
    }

    int main() {
      Point blank = { 3.0, 4.0 };
      printPoint (blank);
    }

As a second example, we can rewrite the ``distance`` function from
Section `[distance] <#distance>`__ so that it takes two ``Point``\ s as
parameters instead of four ``double``\ s.

::

   double distance (Point p1, Point p2) {
     double dx = p2.x - p1.x;
     double dy = p2.y - p1.y;
     return sqrt (dx*dx + dy*dy);
   }
