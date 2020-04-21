Getting user input
------------------

The programs we have written so far are pretty predictable; they do the
same thing every time they run. Most of the time, though, we want
programs that take input from the user and respond accordingly.

There are many ways to get input, including keyboard input, mouse
movements and button clicks, as well as more exotic mechanisms like
voice control and retinal scanning. In this text we will consider only
keyboard input.

In the header file ``iostream``, C++ defines an object named ``cin``
that handles input in much the same way that ``cout`` handles output. To
get an integer value from the user:

::

     int x;
     cin >> x;

The ``>>`` operator causes the program to stop executing and wait for
the user to type something. If the user types a valid integer, the
program converts it into an integer value and stores it in ``x``.

If the user types something other than an integer, C++ doesn’t report an
error, or anything sensible like that. Instead, it puts some meaningless
value in ``x`` and continues.

Fortunately, there is a way to check and see if an input statement
succeeds. We can invoke the ``good`` function on ``cin`` to check what
is called the **stream state**. ``good`` returns a ``bool``: if true,
then the last input statement succeeded. If not, we know that some
previous operation failed, and also that the next operation will fail.

Thus, getting input from the user might look like this:

.. activecode:: eightfour
  :language: cpp

   #include <iostream>

   using namespace std;

   int main ()
   {
     int x;

     // prompt the user for input
     cout << "Enter an integer: ";

     // get input
     cin >> x;

     // check and see if the input statement succeeded
     if (cin.good() == false) {
       cout << "That was not an integer." << endl;
       return -1;
     }

     // print the value we got from the user
     cout << x << endl;
     return 0;
   }

``cin`` can also be used to input a ``string``:

::

     string name;

     cout << "What is your name? ";
     cin >> name;
     cout << name << endl;

Unfortunately, this statement only takes the first word of input, and
leaves the rest for the next input statement. So, if you run this
program and type your full name, it will only output your first name.

Because of these problems (inability to handle errors and funny
behavior), I avoid using the ``>>`` operator altogether, unless I am
reading data from a source that is known to be error-free.

Instead, I use a function in the header ``string`` called ``getline``.

::

     string name;

     cout << "What is your name? ";
     getline (cin, name);
     cout << name << endl;

The first argument to ``getline`` is ``cin``, which is where the input
is coming from. The second argument is the name of the ``string`` where
you want the result to be stored.

``getline`` reads the entire line until the user hits Return or Enter.
This is useful for inputting strings that contain spaces.

In fact, ``getline`` is generally useful for getting input of any kind.
For example, if you wanted the user to type an integer, you could input
a string and then check to see if it is a valid integer. If so, you can
convert it to an integer value. If not, you can print an error message
and ask the user to try again.

To convert a string to an integer you can use the ``atoi`` function
defined in the header file ``cstdlib``. We will get to that in
Section `[parsing] <#parsing>`__.

.. mchoice:: test_question_eight_point_eleven_one
   :practice: T
   :answer_a: getline only takes the first word of input while getline reads the entire line until the user hits Return or Enter.
   :answer_b: cin only takes the first word of input while cin reads the entire line until the user hits Return or Enter.
   :answer_c: cin only takes the first two words of input while getline reads the entire line until there is a space.
   :correct: b
   :feedback_a: Try again.
   :feedback_b: Correct!
   :feedback_c: Try again.


   What is the difference between ``cin`` and ``getline``?


.. mchoice:: test_question_eight_point_eleven_two
   :practice: T
   :answer_a: John
   :answer_b: J
   :answer_c: John Doe
   :correct: b
   :feedback_a: Try again! Pay attention to the data type of name.
   :feedback_b: Correct!
   :feedback_c: Try again!


   The user types in ``John Doe``. What prints?

   .. code-block:: cpp

      int main(){
        char name;

        cout << "What is your name? ";
        cin >> name;
        cout << name << endl;

      }

.. mchoice:: test_question_eight_point_eleven_three
   :practice: T
   :answer_a: John
   :answer_b: J
   :answer_c: John Doe
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again!
   :feedback_c: Try again!


   The user types in ``John Doe``. What prints?

   .. code-block:: cpp

      int main(){
        string name;

        cout << "What is your name? ";
        cin >> name;
        cout << name << endl;

      }

.. mchoice:: test_question_eight_point_eleven_four
   :practice: T
   :answer_a: John
   :answer_b: J
   :answer_c: John Doe
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct!


   The user types in ``John Doe``. What prints?

   .. code-block:: cpp

      int main(){
        string name;

        cout << "What is your name? ";
        getline (cin, name);
        cout << name << endl;

      }
