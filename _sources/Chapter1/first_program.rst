.. _hello:

The first program
-----------------

Traditionally the first program people write in a new language is called
“Hello, World.” because all it does is print the words “Hello, World.”
In C++, this program looks like this:


.. activecode:: oneone
   :language: cpp
   :caption: Hello World


   #include <iostream>
   using namespace std;

   // main: generate some simple output

   int main () {
     cout << "Hello, World." << endl;
     return 0;
   }

Some people judge the quality of a programming language by the
simplicity of the “Hello, World.” program. By this standard, C++ does
reasonably well. Even so, this simple program contains several features
that are hard to explain to beginning programmers. For now, we will
ignore some of them, like the first two lines.

The third line begins with ``//``, which indicates that it is a **comment**.
A comment is a bit of English text that you can put in the middle of a
program, usually to explain what the program does. When the compiler
sees a ``//``, it ignores everything from there until the end of the line.

In the fourth line, you can ignore the word ``int`` for now, but notice the
word ``main``.  ``main`` is a special name that indicates the place in the
program where execution begins. When the program runs, it starts by
executing the first statement in ``main`` and it continues, in order, until
it gets to the last statement, and then it quits.

There is no limit to the number of statements that can be in main, but
the example contains only one. It is a basic **output** statement,
meaning that it outputs or displays a message on the screen.

``cout`` is a special object provided by the system to allow you to send
output to the screen. The symbol ``<<`` is an **operator** that you apply to
``cout`` and a string, and that causes the string to be displayed.

``endl`` is a special symbol that represents the end of a line. When you
send an ``endl`` to ``cout``, it causes the cursor to move to the next line of
the display. The next time you output something, the new text appears on
the next line.

Like all statements, the output statement ends with a semi-colon (``;``).

.. warning::
   Forgetting to terminate a statement with a semicolon will result in a compile error.

There are a few other things you should notice about the syntax of this
program. First, C++ uses squiggly-braces (``{`` and ``}``) to group things
together. In this case, the output statement is enclosed in
squiggly-braces, indicating that it is *inside* the definition of ``main``.
Also, notice that the statement is indented, which helps to show
visually which lines are inside the definition.

As I mentioned, the C++ compiler is a real stickler for syntax. If you
make any errors when you type in the program, chances are that it will
not compile successfully. For example, if you misspell ``iostream``, you
might get an error message like the following:

::

    hello.cpp:1: oistream.h: No such file or directory

There is a lot of information on this line, but it is presented in a
dense format that is not easy to interpret. A more friendly compiler
might say something like:

    “On line 1 of the source code file named hello.cpp, you tried to
    include a header file named ``oistream.h``. I didn’t find anything with
    that name, but I did find something named ``iostream``. Is that what you
    meant, by any chance?”

Unfortunately, few compilers are so accomodating. The compiler is not
really very smart, and in most cases the error message you get will be
only a hint about what is wrong. It will take some time to gain facility
at interpreting compiler messages.

Nevertheless, the compiler can be a useful tool for learning the syntax
rules of a language. Starting with a working program above,
modify it in various ways and see what happens. If you get an error
message, try to remember what the message says and what caused it, so if
you see it again in the future you will know what it means.

.. fillintheblank:: question1_6_1

    How do you indicate a comment in C++?
    
    - :[//][//]: Correct!
      :.*: Try again!

.. mchoice:: question1_6_2
   :multiple_answers:
   :answer_a: It marks the spot in the program where execution begins.
   :answer_b: There is a limit the number of statements you can put in int main() because they occupy system memory.
   :answer_c: Inside int main(), program execution happens in order, from top to bottom.
   :answer_d: int main() is enclosed by square brackets ( [ and ] ).
   :answer_e: The end of a statement is marked with a semicolon ( ; ).
   :correct: a,c,e
   :feedback_a: int main() indicates where the program begins executing!
   :feedback_b: There is no limit to the number of statements you can put in int main(), but it is good practice to keep the main as short as possible.
   :feedback_c: When the program runs, it starts by executing the first statement in main, and it continues until the last.
   :feedback_d: int main() and all functions in C++ are enclosed by squiggly brackets ( { and }).
   :feedback_e: Forgetting a semicolol will cause a compile error!

   Which is true about the ``int main()``?

.. fillintheblank:: question1_6_3

    |blank| is an object that allows you to send output to the terminal.  It requires you to use the |blank| operator.
    
    - :(cout): Correct!
      :.*: Try again!
    - :(\<\<): Correct!
      :.*: Try again!
