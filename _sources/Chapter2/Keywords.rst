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
and other code black. 

.. Warning::
   If you type a variable name and it turns blue, watch out! You might get 
   some strange behavior from the compiler.

.. fillintheblank:: question2_6_1

    Words that are reserved in C++ because they are used by the compiler to parse the structure of your program
    are called |blank|.

    - :[Kk][Ee][Yy][Ww][Oo][Rr][Dd][Ss]: Correct!
      :.*: Try again!

.. mchoice:: question2_6_2
   :answer_a: integer
   :answer_b: cout
   :answer_c: variable
   :answer_d: string
   :answer_e: char
   :correct: b,d,e
   :feedback_a: integer is not a keyword, but int is.
   :feedback_b: cout cannot be used as a variable name!
   :feedback_c: variable is fair game to use to name a variable.
   :feedback_d: string cannot be used as a variable name.
   :feedback_e: char is a keyword and cannot be used as a variable name.

   Which of the following are keywords or will otherwise generate some error from the compiler if used as a variable name?

.. activecode:: twoeight
   :language: cpp
   :caption: Code highlighting

   Fix the code below so that the variable names are not keywords.

   ~~~~
   #include <iostream>
   using namespace std;

   int main() {
      int char = 20;
      char first_initial = 'E';
      char last_initial = 'P';
      cout << "My age is " << char << endl;
      cout << "My initials are " << first_initial << " and " << last_initial;
   }
