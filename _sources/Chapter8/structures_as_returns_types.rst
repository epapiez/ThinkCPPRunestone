Structures as return types
--------------------------

You can write functions that return structures. For example,
``findCenter`` takes a ``Rectangle`` as an argument and returns a
``Point`` that contains the coordinates of the center of the
``Rectangle``:

::

   Point findCenter (Rectangle& box)
   {
     double x = box.corner.x + box.width/2;
     double y = box.corner.y + box.height/2;
     Point result = {x, y};
     return result;
   }

To call this function, we have to pass a box as an argument (notice that
it is being passed by reference), and assign the return value to a
``Point`` variable:

::

     Rectangle box = { {0.0, 0.0}, 100, 200 };
     Point center = findCenter (box);
     printPoint (center);

.. activecode:: eighttwo
  :language: cpp

    #include <iostream>
    using namespace std;

    struct Point {
      double x, y;
    };

    struct Rectangle {
      Point corner;
      double width, height;
    };

    void printPoint (Point p) {
      cout << "(" << p.x << ", " << p.y << ")" << endl;
    }

    Point findCenter (Rectangle& box)
    {
      double x = box.corner.x + box.width/2;
      double y = box.corner.y + box.height/2;
      Point result = {x, y};
      return result;
    }

    int main() {
      Rectangle box = { {0.0, 0.0}, 100, 200 };
      Point center = findCenter (box);
      printPoint (center);
    }


The output of this program is ``(50, 100)``.
