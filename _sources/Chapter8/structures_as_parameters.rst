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

.. mchoice:: question_eight_point_five
   :multiple_answers:
   :answer_a: (-2.0, -7.0)
   :answer_b: (2.0, 7.0)
   :answer_c: (-7.0, -2.0)
   :answer_d: (7.0, 2.0)
   :correct: c
   :feedback_a: Take a close look at the printOppositeCoordinate function.
   :feedback_b: Take a close look at the printOppositeCoordinate function.
   :feedback_c: Correct!
   :feedback_d: Take a close look at the printOppositeCoordinate function.

   What will print?

   .. code-block:: cpp

      struct Coordinate {
      double x, y;
      };

      void printOppositeCoordinate (Point p) {
        cout << "(" << -p.y << ", " << -p.x << ")" << endl;
      }

      int main() {
        Coordinate coord = { 2.0, 7.0 };
        printOppositeCoordinate (coord);
      }

.. parsonsprob:: question_8_point5_1

   Construct a function that takes in three Point structures and prints the average of the x coordinates and the average of the y coordinates as a coordinate. Find the x average before the y average.
   -----
   struct Point {

      double x, y;

   };

   void printAveragePoint(Point p1, Point p2, Point p3) {

      double avgX = (p1.x + p2.x + p3.x)/3;

      double avgY = (p1.y + p2.y + p3.y)/3;

      double avgY = (y.p1 + y.p2 + y.p3)/3; #distractor

      cout << "(" << avgX << "," << avgY << ")";

      cout << "(" << "avgX" << "," << "avgY" << ")"; #distractor

    }
