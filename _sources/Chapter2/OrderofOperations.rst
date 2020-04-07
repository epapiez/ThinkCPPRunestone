Order of operations
-------------------

When more than one operator appears in an expression the order of
evaluation depends on the rules of **precedence**. A complete
explanation of precedence can get complicated, but just to get you
started:

-  Multiplication and division happen before addition and subtraction.
   So ``2*3-1`` yields 5, not 4, and ``2/3-1`` yields -1, not 1 (remember that
   in integer division ``2/3`` is 0).

-  If the operators have the same precedence they are evaluated from
   left to right. So in the expression ``minute*100/60``, the multiplication
   happens first, yielding 5900/60, which in turn yields 98. If the
   operations had gone from right to left, the result would be 59*1
   which is 59, which is wrong.

-  Any time you want to override the rules of precedence (or you are not
   sure what they are) you can use parentheses. Expressions in
   parentheses are evaluated first, so ``2 \* (3-1) is 4``. You can also use
   parentheses to make an expression easier to read, as in ``(minute \*
   100) / 60``, even though it doesn’t change the result.

**Observe the output of the code below to see how parentheses can change a value.**

.. activecode:: twoeleven
  :language: cpp
  :caption: Order of operations

    #include <iostream>
    using namespace std;

    int main ()
    {
      cout << (2 * 3) - 1 << endl;
      cout << 2 * (3 - 1) << endl;
      cout << 2 / 3 - 1 << endl;
      cout << 2 / (3 -1) << endl;
      return 0;
    }

.. dragndrop:: dragndrop_two_six
    :feedback: Try again!
    :match_1:  (6*4)+1|||11
    :match_2: 6*(4+1)|||30
    :match_3: (6/4)+1|||2
    :match_4: 6/(4+1)|||1

    Match the expression to its correct output. Don't forget to consider integer division!
