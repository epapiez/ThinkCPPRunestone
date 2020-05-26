Variables
---------

One of the most powerful features of a programming language is the
ability to manipulate **variables**. A variable is a named location that
stores a value.

Just as there are different types of values (integer, character, etc.),
there are different types of variables. When you create a new variable,
you have to declare what type it is. The following statement creates a 
new variable named fred that has type char.

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

.. fillintheblank:: question2_3_1

   Take a look at the code block below:
   
   .. code-block:: cpp

      char tom;

   It's an example of a(n) |blank| statement.

   - :[Dd][Ee][Cc][Ll][Aa][Rr][Aa][Tt][Ii][Oo][Nn]: Correct!
     :.*: Try again!

.. dragndrop:: question2_3_2
    :feedback: Try again!
    :match_1:  char joe;|||'x'
    :match_2: string ten;|||"Joe"
    :match_3: int x;|||10

    Match the variable to the kind of value it can store.

.. fillintheblank:: question2_3_3

   A(n) |blank| is a name given to a location in memory used to keep track of a value.

   - :[Vv][Aa][Rr][Ii][Aa][Bb][Ll][Ee]: Correct!
     :.*: Try again!
