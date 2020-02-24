Outputting variables
--------------------

You can output the value of a variable using the same commands we used
to output simple values. After observing the output, try inputting your own time!

.. activecode:: twofive
  :language: cpp
  :caption: Outputting variables

    #include <iostream>
    using namespace std;
    // main: generate some simple output

    int main ()
    {
    int hour, minute;
    char colon;

    hour = 11;
    minute = 59;
    colon = ':';

    cout << "The current time is ";
    cout << hour;
    cout << colon;
    cout << minute;
    cout << endl;

      return 0;
    }

This program creates two integer variables named hour and minute, and a
character variable named colon. It assigns appropriate values to each of
the variables and then uses a series of output statements to generate
the following:

::

    The current time is 11:59

When we talk about “outputting a variable,” we mean outputting the
*value* of the variable. To output the *name* of a variable, you have to
put it in quotes. For example: cout << "hour";

As we have seen before, you can include more than one value in a single
output statement, which can make the previous program more concise:

.. activecode:: twosix
  :language: cpp
  :caption: Outputting variables

    #include <iostream>
    using namespace std;
    // main: generate some simple output

    int main ()
    {
    int hour, minute;
    char colon;

    hour = 11;
    minute = 59;
    colon = ':';

    cout << "The current time is " << hour << colon << minute << endl;

    return 0;
    }


On one line, this program outputs a string, two integers, a character,
and the special value endl. Very impressive!

**Fix the following code so that each variable has a type!**

.. activecode:: twoseven
  :language: cpp
  :caption: Integers and chars declaration

   #include <iostream>
   using namespace std;

    int main()
    {
    x = 0;
    z = '.';
    cout << x;
    cout << z << endl;
    return 0;
    }

.. dragndrop:: dragndrop_two_four
    :feedback: Try again!
    :match_1:  x = 12|||int
    :match_2: y = "Bye!"|||string
    :match_3: z = '.'|||char

    Match the variable initialization to its correct type.
