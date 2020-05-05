Call by value
-------------

When you pass a structure as an argument, remember that the argument and
the parameter are not the same variable. Instead, there are two
variables (one in the caller and one in the callee) that have the same
value, at least initially. For example, when we call ``printPoint``, the stack diagram looks like this:

.. figure:: Images/8.6stackdiagram.png
   :scale: 50%
   :align: center
   :alt: image

If ``printPoint`` happened to change one of the instance variables of
``p``, it would have no effect on ``blank``. Of course, there is no
reason for ``printPoint`` to modify its parameter, so this isolation
between the two functions is appropriate.

This kind of parameter-passing is called “pass by value” because it is
the value of the structure (or other type) that gets passed to the
function.

Observe the output of the code below. The function ``addTwo`` changes the instance variables, but not on ``blank`` itself.

.. activecode:: eightone_two_one_____
  :language: cpp

    #include <iostream>
    using namespace std;

    struct Point {
      double x, y;
    };

    void addTwo (Point p) {
      cout << "(" << p.x + 2 << ", " << p.y + 2 << ")" << endl;
    }

    int main() {
      Point blank = { 3.0, 4.0 };
      addTwo (blank);
      cout << "(" << blank.x << "," << blank.y << ")" << endl;
    }

.. mchoice:: question_eight_point_six_two
   :practice: T
   :answer_a: 2 4
   :answer_b: 2 4 2
   :answer_c: 4 4 2
   :answer_d: 2 4 4
   :correct: b
   :feedback_a: Take a look at exactly what is being outputted.
   :feedback_b: Correct!
   :feedback_c: Take a look at exactly what is being outputted.
   :feedback_d: Remember the rules of pass by value.

   What will print?

   .. code-block:: cpp

      int addTwo(int x) {
        cout << x << " ";
        x = x + 2;
        cout << x << " ";
        return x;
      }

      int main() {
        int num = 2;
        addTwo(num);
        cout << num << endl;
      }


.. mchoice:: question_eight_point_six_one
   :practice: T
   :answer_a: 6.0, 8.0, 3.0, 4.0
   :answer_b: 6.0, 8.0, 6.0, 8.0
   :answer_c: 6.08.03.04.0
   :answer_d: 6.08.06.08.0
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Remember the rules of pass by value.
   :feedback_c: Take a look at exactly what is being outputted.
   :feedback_d: Take a look at exactly what is being outputted.

   What will print?

   .. code-block:: cpp

      struct Point {
        double x, y;
      };

      void timesTwo (Point p) {
        cout << "(" << p.x * 2 << ", " << p.y * 2 << ")";
      }

      int main() {
        Point blank = { 3.0, 4.0 };
        timesTwo (blank);
        cout << ", " << blank << endl;
      }
