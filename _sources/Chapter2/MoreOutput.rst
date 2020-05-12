More output
-----------

As I mentioned in the last chapter, you can put as many statements as
you want in main. For example, to output more than one line:

.. activecode:: twoone
  :language: cpp
  :caption: Simple output

    #include <iostream>
    using namespace std;
    // main: generate some simple output

    int main ()
    {
      cout << "Hello, world." << endl;     // output one line
      cout << "How are you?" << endl;      // output another
    }

As you can see, it is legal to put comments at the end of a line, as
well as on a line by themselves.

The phrases that appear in quotation marks are called **strings**,
because they are made up of a sequence (string) of letters. Actually,
strings can contain any combination of letters, numbers, punctuation
marks, and other special characters.

Often it is useful to display the output from multiple output statements
all on one line. You can do this by leaving out the first endl:

.. activecode:: twotwo
  :language: cpp
  :caption: Cruel world!

  #include <iostream>
  using namespace std;

    int main ()
    {
      cout << "Goodbye, ";
      cout << "cruel world!" << endl;
    }

In this case the output appears on a single line as ``Goodbye, cruel
world!``. Notice that there is a space between the word “Goodbye,” and the
second quotation mark. This space appears in the output, so it affects
the behavior of the program.

Spaces that appear outside of quotation marks generally do not affect
the behavior of the program. For example, I could have written:

.. activecode:: twothree
  :language: cpp
  :caption: Cruel world! (no spaces)

  #include <iostream>
  using namespace std;

    int main ()
    {
      cout<<"Goodbye, ";
      cout<<"cruel world!"<<endl;
    }

This program would compile and run just as well as the original. The
breaks at the ends of lines (newlines) do not affect the program’s
behavior either, so I could have written:

.. activecode:: twofour
  :language: cpp
  :caption: Cruel world! (one line)

  #include <iostream>
  using namespace std;

    int main(){cout<<"Goodbye, ";cout<<"cruel world!"<<endl;}

That would work, too, although you have probably noticed that the
program is getting harder and harder to read. Newlines and spaces are
useful for organizing your program visually, making it easier to read
the program and locate syntax errors.

.. dragndrop:: dragndrop_two_one
    :feedback: Try again!
    :match_1:  cout<<"Hello"; cout<<"Hello";|||one line
    :match_2: cout<<"Hello" << endl; cout<<"Hello";|||two lines

    Match the code snippet to the correct amount of lines that would be printed.


.. fillintheblank:: fill_2.1

    The phrases that appear in quotation marks are called...

    - :(?:s|S)(?:t|T)(?:r|R)(?:i|I)(?:n|N)(?:g|G)s?: Correct!
      :.*: Try again!


.. parsonsprob:: question1_100_4

   Construct a main function that prints out "Hello, world!"
   -----
   int main () {
   =====
    cout << "Hello, world!" << endl;
   =====
    cout << Hello, world! << endl; #distractor
   =====
    cout >> "Hello, world!" >> endl; #distractor
   =====
    cout >> Hello, world! >> endl; #distractor
   =====
   }
