Assignment
----------

Now that we have created some variables, we would like to store values
in them. We do that with an **assignment statement**.

::

        firstLetter = 'a';   // give firstLetter the value 'a'
        hour = 11;           // assign the value 11 to hour
        minute = 59;         // set minute to 59

This example shows three assignments, and the comments show three
different ways people sometimes talk about assignment statements. The
vocabulary can be confusing here, but the idea is straightforward:

-  When you declare a variable, you create a named storage location.

-  When you make an assignment to a variable, you give it a value.

A common way to represent variables on paper is to draw a box with the
name of the variable on the outside and the value of the variable on the
inside. This kind of figure is called a **state diagram** because is
shows what state each of the variables is in (you can think of it as the
variable’s “state of mind”). This diagram shows the effect of the three
assignment statements:




I sometimes use different shapes to indicate different variable types.
These shapes should help remind you that one of the rules in C++ is that
a variable has to have the same type as the value you assign it. For
example, you cannot store a string in an int variable. The following
statement generates a compiler error.

::

      int hour;
      hour = "Hello.";       // WRONG !!

This rule is sometimes a source of confusion, because there are many
ways that you can convert values from one type to another, and C++
sometimes converts things automatically. But for now you should remember
that as a general rule variables and values have the same type, and
we’ll talk about special cases later.

Another source of confusion is that some strings *look* like integers,
but they are not. For example, the string "123", which is made up of the
characters 1, 2 and 3, is not the same thing as the *number* 123. This
assignment is illegal:

::

      minute = "59";         // WRONG!

**Check your understanding!**

.. mchoice:: test_question_two_two
   :practice: T
   :answer_a: Change the type of variable q from int to char.
   :answer_b: Change the type of both variables (d and q) from int to char.
   :answer_c: Change the type of variable d from int to char.
   :correct: c
   :feedback_a: Variable q was assigned as 9, which is an int.
   :feedback_b: The variables were assigned as two different types, so they wouldn't both need to be changed.
   :feedback_c: Yes, variable d is a char because it was assigned as a single character with single quotes around it.


   What must be changed in order for this code block to work?

   .. code-block:: cpp

    #include <iostream>
    using namespace std;
    // main: generate some simple output

    int main ()
    {
      int d;
      int q;
      d = 'h';
      q = 9;
      return 0;
    }
