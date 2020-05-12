Variables
---------

One of the most powerful features of a programming language is the
ability to manipulate **variables**. A variable is a named location that
stores a value.

Just as there are different types of values (integer, character, etc.),
there are different types of variables. When you create a new variable,
you have to declare what type it is. For example, the character type in
C++ is called char. The following statement creates a new variable named
fred that has type char.

::

        char fred;

This kind of statement is called a **declaration**.

The type of a variable determines what kind of values it can store. A
char variable can contain characters, and it should come as no surprise
that int variables can store integers.

There are several types in C++ that can store string values, but we are
going to skip that for now (see Chapter 7).

To create an integer variable, the syntax is

::

      int bob;

where bob is the arbitrary name you made up for the variable. In
general, you will want to make up variable names that indicate what you
plan to do with the variable. For example, if you saw these variable
declarations:

::

        char firstLetter;
        char lastLetter;
        int hour, minute;

you could probably make a good guess at what values would be stored in
them. This example also demonstrates the syntax for declaring multiple
variables with the same type: hour and minute are both integers (int
type).

.. mchoice:: test_question_2.3
   :practice: T
   :answer_a: storage
   :answer_b: declaration
   :answer_c: strings
   :correct: b
   :feedback_a: Try again!
   :feedback_b: Correct!
   :feedback_c: Try again!

   What is the following statement called?

   .. code-block:: cpp

    char x;


.. fillintheblank:: fill_2.3

    A statement that creates a new variable is called a...

    - :(?:d|D)(?:e|E)(?:c|C)(?:l|L)(?:a|A)(?:r|R)(?:a|A)(?:T|t)(?:i|I)(?:o|O)(?:n|N): Correct!
      :.*: Try again!

.. dragndrop:: dragndrop_two_three
    :feedback: Try again!
    :match_1:  char tree;|||'x'
    :match_2: string blue;|||"Coding is fun!"
    :match_3: int joe;|||17

    Match the variable to the kind of value it can store.
