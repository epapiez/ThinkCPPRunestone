Infinite recursion
------------------

In the examples in the previous section, notice that each time the
functions get called recursively, the argument gets smaller by one, so
eventually it gets to zero. When the argument is zero, the function
returns immediately, *without making any recursive calls*. This
case—when the function completes without making a recursive call—is
called the **base case**.

If a recursion never reaches a base case, it will go on making recursive
calls forever and the program will never terminate. This is known as
**infinite recursion**, and it is generally not considered a good idea.

In most programming environments, a program with an infinite recursion
will not really run forever. Eventually, something will break and the
program will report an error. This is the first example we have seen of
a run-time error (an error that does not appear until you run the
program).

You should write a small program that recurses forever and run it to see
what happens. Below is an example. The function adds to the number **n**
instead of subtracting, which means it is always larger than 0. Therefore,
the function executes "forever." Unfortunately, if there was a snip of live
code put in below, the ebook's page would extend down forever because a new
line is being created infinitely.

::

    #include <iostream>
    #include <cmath>
    using namespace std;

    void nLines(int n) {
      if (n > 0) {
        cout << endl;
        nLines(n+1);
      }
    }

    int main() {
      void nLines(10);
    }
