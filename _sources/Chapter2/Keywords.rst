Keywords
--------

A few sections ago, I said that you can make up any name you want for
your variables, but that’s not quite true. There are certain words that
are reserved in C++ because they are used by the compiler to parse the
structure of your program, and if you use them as variable names, it
will get confused. These words, called **keywords**, include ``int``, ``char``,
``void``, ``endl`` and many more.

The complete list of keywords is included in the C++ Standard, which is
the official language definition adopted by the the International
Organization for Standardization (ISO) on September 1, 1998. You can
download a copy electronically from

::

        http://www.ansi.org/

Rather than memorize the list, I would suggest that you take advantage
of a feature provided in many development environments: code
highlighting. As you type, different parts of your program should appear
in different colors. For example, keywords might be blue, strings red,
and other code black. If you type a variable name and it turns blue,
watch out! You might get some strange behavior from the compiler.

**Fix the code below so that the variable names are not keywords.**

.. activecode:: twoeight
  :language: cpp
  :caption: Code highlighting

   #include <iostream>
   using namespace std;

    int main()
    {
    int char = 20;
    char first_initial = 'E';
    char last_initial = 'P';
    cout << "My age is " << char << endl;
    cout << "My initials are " << first_initial << " and " << last_initial;
    return 0;
    }
