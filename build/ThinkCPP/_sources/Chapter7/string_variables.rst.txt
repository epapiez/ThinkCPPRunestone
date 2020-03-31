``string`` variables
--------------------

You can create a variable with type ``string`` in the usual ways:

.. activecode:: sevenone
  :language: cpp
  :caption: Creating a string variable

  #include <iostream>
  using namespace std;

  int main() {
     string first;
     first = "Hello, ";
     string second = "world.";
  }

The first line creates a ``string`` without giving it a value. The
second line assigns it the string value ``"Hello."`` The third line is a
combined declaration and assignment, also called an initialization.

Normally when string values like ``"Hello, "`` or ``"world."`` appear,
they are treated as C strings. In this case, when we assign them to an
``string`` variable, they are converted automatically to ``string``
values.

We can output strings in the usual way:

::

     cout << first << second << endl;

In order to compile this code, you will have to include the header file
for the ``string`` class, and you will have to add the file ``string``
to the list of files you want to compile. The details of how to do this
depend on your programming environment.

Before proceeding, you should type in the program above and make sure
you can compile and run it.

.. activecode:: seventwo
  :language: cpp
  :caption: Outputting a string variable

  #include <iostream>
  using namespace std;

  int main() {
     string first;
     first = "Hello, ";
     string second = "world.";
     cout << first << second << endl;
  }

.. parsonsprob:: question_seven_one

   Construct a block of code that correctly prints out a string variable.
   -----
   string x;

   x = "It is cold outside!";

   x = "It is cold outside" #paired

   cout << x << endl;
