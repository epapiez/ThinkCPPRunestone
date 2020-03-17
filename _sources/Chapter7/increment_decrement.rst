Increment and decrement operators
---------------------------------

Incrementing and decrementing are such common operations that C++
provides special operators for them. The ``++`` operator adds one to the
current value of an ``int``, ``char`` or ``double``, and ``–`` subtracts
one. Neither operator works on ``string``\ s, and neither *should* be
used on ``bool``\ s.

Technically, it is legal to increment a variable and use it in an
expression at the same time. For example, you might see something like:

::

     cout << i++ << endl;

Looking at this, it is not clear whether the increment will take effect
before or after the value is displayed. Because expressions like this
tend to be confusing, I would discourage you from using them. In fact,
to discourage you even more, I’m not going to tell you what the result
is. If you really want to know, you can try it.

Using the increment operators, we can rewrite the letter-counter:

::

     int index = 0;
     while (index < length) {
       if (fruit[index] == 'a') {
         count++;
       }
       index++;
     }

It is a common error to write something like

::

     index = index++;             // WRONG!!

Unfortunately, this is syntactically legal, so the compiler will not
warn you. The effect of this statement is to leave the value of
``index`` unchanged. This is often a difficult bug to track down.

Remember, you can write ``index = index +1;``, or you can write
``index++;``, but you shouldn’t mix them.


.. clickablearea:: click_seven_four
    :question: Click on the **incorrect** or **not** suggested increment statements.
    :iscode:
    :feedback: Re-read the text above and try again.

    :click-incorrect:def main() {::endclick:
        :click-incorrect:count = count + 1;:endclick:
        :click-incorrect:index++;:endclick:
        :click-correct: count = count++;:endclick:
        :click-correct: cout << x++ << endl;:endclick:
        :click-incorrect: count--; :endclick:
        }
