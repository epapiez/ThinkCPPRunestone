Tables
------

One of the things loops are good for is generating tabular data. For
example, before computers were readily available, people had to
calculate logarithms, sines and cosines, and other common mathematical
functions by hand. To make that easier, there were books containing long
tables where you could find the values of various functions. Creating
these tables was slow and boring, and the result tended to be full of
errors.

When computers appeared on the scene, one of the initial reactions was,
“This is great! We can use the computers to generate the tables, so
there will be no errors.” That turned out to be true (mostly), but
shortsighted. Soon thereafter computers and calculators were so
pervasive that the tables became obsolete.

Well, almost. It turns out that for some operations, computers use
tables of values to get an approximate answer, and then perform
computations to improve the approximation. In some cases, there have
been errors in the underlying tables, most famously in the table the
original Intel Pentium used to perform floating-point division.

Although a “log table” is not as useful as it once was, it still makes a
good example of iteration. The following program outputs a sequence of
values in the left column and their logarithms in the right column:

.. activecode:: sixfour
  :language: cpp
  :caption: Tables

  #include <iostream>
  #include <cmath>
  using namespace std;

  int main() {
     double x = 1.0;
     while (x < 10.0) {
       cout << x << "\t" << log(x) << "\n";
       x = x + 1.0;
     }
     return 0;
  }

The sequence ``\t`` represents a **tab** character. The sequence ``\n``
represents a newline character. These sequences can be included anywhere
in a string, although in these examples the sequence is the whole
string.

A tab character causes the cursor to shift to the right until it reaches
one of the **tab stops**, which are normally every eight characters. As
we will see in a minute, tabs are useful for making columns of text line
up.

A newline character has exactly the same effect as ``endl``; it causes
the cursor to move on to the next line. Usually if a newline character
appears by itself, I use ``endl``, but if it appears as part of a
string, I use ``\n``.

The output of this program is

::

   1      0
   2      0.693147
   3      1.09861
   4      1.38629
   5      1.60944
   6      1.79176
   7      1.94591
   8      2.07944
   9      2.19722

If these values seem odd, remember that the ``log`` function uses base
:math:`e`. Since powers of two are so important in computer science, we
often want to find logarithms with respect to base 2. To do that, we can
use the following formula:

.. math:: \log_2 x = \frac {log_e x}{log_e 2}

Changing the output statement to

::

         cout << x << "\t" << log(x) / log(2.0) << endl;

yields

::

   1      0
   2      1
   3      1.58496
   4      2
   5      2.32193
   6      2.58496
   7      2.80735
   8      3
   9      3.16993

We can see that 1, 2, 4 and 8 are powers of two, because their
logarithms base 2 are round numbers. If we wanted to find the logarithms
of other powers of two, we could modify the program like this:

.. activecode:: sixfive
  :language: cpp
  :caption: Tables

  #include <iostream>
  #include <cmath>
  using namespace std;

  int main() {
     double x = 1.0;
     while (x < 100.0) {
       cout << x << "\t" << log(x) / log(2.0) << endl;
       x = x * 2.0;
     }
     return 0;
  }

Now instead of adding something to ``x`` each time through the loop,
which yields an arithmetic sequence, we multiply ``x`` by something,
yielding a **geometric** sequence. The result is:

::

   1      0
   2      1
   4      2
   8      3
   16     4
   32     5
   64     6

Because we are using tab characters between the columns, the position of
the second column does not depend on the number of digits in the first
column.

Log tables may not be useful any more, but for computer scientists,
knowing the powers of two is! As an exercise, modify this program so
that it outputs the powers of two up to 65536 (that’s :math:`2^{16}`).
Print it out and memorize it.

.. fillintheblank:: fill_six_one

    What is the equivalent of endl, and typically used at the end of a string?

    - :(?:(?:\\n)|(?:(?:n|N)ewline\s(?:c|C)haracter)): Is the correct answer!
      :.*: Try again!

.. fillintheblank:: fill_six_two

    How would you write a tab character?

    - :\t: Is the correct answer!
      :.*: Try again!
