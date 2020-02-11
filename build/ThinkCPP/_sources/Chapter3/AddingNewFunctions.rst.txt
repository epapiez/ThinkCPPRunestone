Adding new functions
--------------------

So far we have only been using the functions that are built into C++,
but it is also possible to add new functions. Actually, we have already
seen one function definition: main. The function named main is special
because it indicates where the execution of the program begins, but the
syntax for main is the same as for any other function definition:

::

      void NAME ( LIST OF PARAMETERS ) {
        STATEMENTS
      }

You can make up any name you want for your function, except that you
can’t call it main or any other C++ keyword. The list of parameters
specifies what information, if any, you have to provide in order to use
(or **call**) the new function.

main doesn’t take any parameters, as indicated by the empty parentheses
() in it’s definition. The first couple of functions we are going to
write also have no parameters, so the syntax looks like this:

::

      void newLine () {
        cout << endl;
      }

This function is named newLine; it contains only a single statement,
which outputs a newline character, represented by the special value
endl.

In main we can call this new function using syntax that is similar to
the way we call the built-in C++ commands:

::

    int main ()
    {
      cout << "First Line." << endl;
      newLine ();
      cout << "Second Line." << endl;
      return 0;
    }

The output of this program is

::

    First line.

    Second line.

Notice the extra space between the two lines. What if we wanted more
space between the lines? We could call the same function repeatedly:

::

    int main ()
    {
      cout << "First Line." << endl;
      newLine ();
      newLine ();
      newLine ();
      cout << "Second Line." << endl;
      return 0;
    }

Or we could write a new function, named threeLine, that prints three new
lines:

.. activecode:: threesix
  :language: cpp
  :caption: threeLine function

  #include <iostream>
  using namespace std;

  void newLine () {
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

You should notice a few things about this program:

-  You can call the same procedure repeatedly. In fact, it is quite
   common and useful to do so.

-  You can have one function call another function. In this case, main
   calls threeLine and threeLine calls newLine. Again, this is common
   and useful.

-  In threeLine I wrote three statements all on the same line, which is
   syntactically legal (remember that spaces and new lines usually don’t
   change the meaning of a program). On the other hand, it is usually a
   better idea to put each statement on a line by itself, to make your
   program easy to read. I sometimes break that rule in this book to
   save space.

So far, it may not be clear why it is worth the trouble to create all
these new functions. Actually, there are a lot of reasons, but this
example only demonstrates two:

#. Creating a new function gives you an opportunity to give a name to a
   group of statements. Functions can simplify a program by hiding a
   complex computation behind a single command, and by using English
   words in place of arcane code. Which is clearer, newLine or cout <<
   endl?

#. Creating a new function can make a program smaller by eliminating
   repetitive code. For example, a short way to print nine consecutive
   new lines is to call threeLine three times. How would you print 27
   new lines?
