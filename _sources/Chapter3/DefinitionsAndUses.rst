Definitions and uses
--------------------

Pulling together all the code fragments from the previous section, the
whole program looks like this:

::

    #include <iostream>
    using namespace std;

    void newLine ()
    {
      cout << endl;
    }

    void threeLine ()
    {
      newLine ();  newLine ();  newLine ();
    }

    int main ()
    {
      cout << "First Line." << endl;
      threeLine ();
      cout << "Second Line." << endl;
      return 0;
    }

This program contains three function definitions: newLine, threeLine,
and main.

Inside the definition of main, there is a statement that uses or calls
threeLine. Similarly, threeLine calls newLine three times. Notice that
the definition of each function appears above the place where it is
used.

This is necessary in C++; the definition of a function must appear
before (above) the first use of the function. You should try compiling
this program with the functions in a different order and see what error
messages you get.

**Call the function called newBorder in your main function. This adds a divider
in between sections of your output.**

.. activecode:: threeseven
  :language: cpp
  :caption: Creating a border function.

  #include <iostream>
  using namespace std;

  void newBorder () {
    cout << "..................." << endl;
  }

  int main ()
  {
    cout << "First Line." << endl;
    #Call function here!
    cout << "Second Line." << endl;
    return 0;
  }

.. parsonsprob:: question_three_one

   Construct a block of code that correctly defines a function.
   -----
   int addTwo(int x) {

   int addTwo(int x); #distractor

   int addTwo(int x) #distractor

      int new = x + 2;

      return new;

      return x; #distractor
    }
