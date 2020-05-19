.. _structs:

Structures
==========

Compound values
---------------

Most of the data types we have been working with represent a single
value—an integer, a floating-point number, a boolean value.
``string``\ s are different in the sense that they are made up of
smaller pieces, the characters. Thus, ``string``\ s are an example of a
**compound** type.

Depending on what we are doing, we may want to treat a compound type as
a single thing (or object), or we may want to access its parts (or
instance variables). This ambiguity is useful.

It is also useful to be able to create your own compound values. C++
provides two mechanisms for doing that: **structures** and **classes**.
We will start out with structures and get to classes in
Chapter `[class] <#class>`__ (there is not much difference between
them).

``Point`` objects
-----------------

As a simple example of a compound structure, consider the concept of a
mathematical point. At one level, a point is two numbers (coordinates)
that we treat collectively as a single object. In mathematical notation,
points are often written in parentheses, with a comma separating the
coordinates. For example, :math:`(0, 0)` indicates the origin, and
:math:`(x, y)` indicates the point :math:`x` units to the right and
:math:`y` units up from the origin.

A natural way to represent a point in C++ is with two ``double``\ s. The
question, then, is how to group these two values into a compound object,
or structure. The answer is a ``struct`` definition:

::

   struct Point {
     double x, y;
   };

``struct`` definitions appear outside of any function definition,
usually at the beginning of the program (after the ``include``
statements).

This definition indicates that there are two elements in this structure,
named ``x`` and ``y``. These elements are called **instance variables**,
for reasons I will explain a little later.

It is a common error to leave off the semi-colon at the end of a
structure definition. It might seem odd to put a semi-colon after a
squiggly-brace, but you’ll get used to it.

Once you have defined the new structure, you can create variables with
that type:

::

     Point blank;
     blank.x = 3.0;
     blank.y = 4.0;

The first line is a conventional variable declaration: ``blank`` has
type ``Point``. The next two lines initialize the instance variables of
the structure. The “dot notation” used here is similar to the syntax for
invoking a function on an object, as in ``fruit.length()``. Of course,
one difference is that function names are always followed by an argument
list, even if it is empty.

The result of these assignments is shown in the following state diagram:

As usual, the name of the variable ``blank`` appears outside the box and
its value appears inside the box. In this case, that value is a compound
object with two named instance variables.

Accessing instance variables
----------------------------

You can read the values of an instance variable using the same syntax we
used to write them:

::

       int x = blank.x;

The expression ``blank.x`` means “go to the object named ``blank`` and
get the value of ``x``.” In this case we assign that value to a local
variable named ``x``. Notice that there is no conflict between the local
variable named ``x`` and the instance variable named ``x``. The purpose
of dot notation is to identify *which* variable you are referring to
unambiguously.

You can use dot notation as part of any C++ expression, so the following
are legal.

::

     cout << blank.x << ", " << blank.y << endl;
     double distance = blank.x * blank.x + blank.y * blank.y;

The first line outputs ``3, 4``; the second line calculates the value
25.

Operations on structures
------------------------

Most of the operators we have been using on other types, like
mathematical operators ( ``+``, ``%``, etc.) and comparison operators
(``==``, ``>``, etc.), do not work on structures. Actually, it is
possible to define the meaning of these operators for the new type, but
we won’t do that in this book.

On the other hand, the assignment operator *does* work for structures.
It can be used in two ways: to initialize the instance variables of a
structure or to copy the instance variables from one structure to
another. An initialization looks like this:

::

     Point blank = { 3.0, 4.0 };

The values in squiggly braces get assigned to the instance variables of
the structure one by one, in order. So in this case, ``x`` gets the
first value and ``y`` gets the second.

Unfortunately, this syntax can be used only in an initialization, not in
an assignment statement. So the following is illegal.

::

     Point blank;
     blank = { 3.0, 4.0 };       // WRONG !!

You might wonder why this perfectly reasonable statement should be
illegal; I’m not sure, but I think the problem is that the compiler
doesn’t know what type the right hand side should be. If you add a
typecast:

::

     Point blank;
     blank = (Point){ 3.0, 4.0 };

That works.

It is legal to assign one structure to another. For example:

::

     Point p1 = { 3.0, 4.0 };
     Point p2 = p1;
     cout << p2.x << ", " <<  p2.y << endl;

The output of this program is ``3, 4``.

Structures as parameters
------------------------

You can pass structures as parameters in the usual way. For example,

::

   void printPoint (Point p) {
     cout << "(" << p.x << ", " << p.y << ")" << endl;
   }

``printPoint`` takes a point as an argument and outputs it in the
standard format. If you call ``printPoint (blank)``, it will output
``(3, 4)``.

As a second example, we can rewrite the ``distance`` function from
Section `[distance] <#distance>`__ so that it takes two ``Point``\ s as
parameters instead of four ``double``\ s.

::

   double distance (Point p1, Point p2) {
     double dx = p2.x - p1.x;
     double dy = p2.y - p1.y;
     return sqrt (dx*dx + dy*dy);
   }

Call by value
-------------

When you pass a structure as an argument, remember that the argument and
the parameter are not the same variable. Instead, there are two
variables (one in the caller and one in the callee) that have the same
value, at least initially. For example, when we call ``printPoint``, the
stack diagram looks like this:

If ``printPoint`` happened to change one of the instance variables of
``p``, it would have no effect on ``blank``. Of course, there is no
reason for ``printPoint`` to modify its parameter, so this isolation
between the two functions is appropriate.

This kind of parameter-passing is called “pass by value” because it is
the value of the structure (or other type) that gets passed to the
function.

Call by reference
-----------------

An alternative parameter-passing mechanism that is available in C++ is
called “pass by reference.” This mechanism makes it possible to pass a
structure to a procedure and modify it.

For example, you can reflect a point around the 45-degree line by
swapping the two coordinates. The most obvious (but incorrect) way to
write a ``reflect`` function is something like this:

::

   void reflect (Point p)      // WRONG !!
   {
     double temp = p.x;
     p.x = p.y;
     p.y = temp;
   }

But this won’t work, because the changes we make in ``reflect`` will
have no effect on the caller.

Instead, we have to specify that we want to pass the parameter by
reference. We do that by adding an ampersand (``&``) to the parameter
declaration:

::

   void reflect (Point& p)
   {
     double temp = p.x;
     p.x = p.y;
     p.y = temp;
   }

Now we can call the function in the usual way:

::

     printPoint (blank);
     reflect (blank);
     printPoint (blank);

The output of this program is as expected:

::

   (3, 4)
   (4, 3)

Here’s how we would draw a stack diagram for this program:

The parameter ``p`` is a reference to the structure named ``blank``. The
usual representation for a reference is a dot with an arrow that points
to whatever the reference refers to.

The important thing to see in this diagram is that any changes that
``reflect`` makes in ``p`` will also affect ``blank``.

Passing structures by reference is more versatile than passing by value,
because the callee can modify the structure. It is also faster, because
the system does not have to copy the whole structure. On the other hand,
it is less safe, since it is harder to keep track of what gets modified
where. Nevertheless, in C++ programs, almost all structures are passed
by reference almost all the time. In this book I will follow that
convention.

Rectangles
----------

Now let’s say that we want to create a structure to represent a
rectangle. The question is, what information do I have to provide in
order to specify a rectangle? To keep things simple let’s assume that
the rectangle will be oriented vertically or horizontally, never at an
angle.

There are a few possibilities: I could specify the center of the
rectangle (two coordinates) and its size (width and height), or I could
specify one of the corners and the size, or I could specify two opposing
corners.

The most common choice in existing programs is to specify the upper left
corner of the rectangle and the size. To do that in C++, we will define
a structure that contains a ``Point`` and two doubles.

::

   struct Rectangle {
     Point corner;
     double width, height;
   };

Notice that one structure can contain another. In fact, this sort of
thing is quite common. Of course, this means that in order to create a
``Rectangle``, we have to create a ``Point`` first:

::

     Point corner = { 0.0, 0.0 };
     Rectangle box = { corner, 100.0, 200.0 };

This code creates a new ``Rectangle`` structure and initializes the
instance variables. The figure shows the effect of this assignment.

We can access the ``width`` and ``height`` in the usual way:

::

     box.width += 50.0;
     cout << box.height << endl;

In order to access the instance variables of ``corner``, we can use a
temporary variable:

::

     Point temp = box.corner;
     double x = temp.x;

Alternatively, we can compose the two statements:

::

     double x = box.corner.x;

It makes the most sense to read this statement from right to left:
“Extract ``x`` from the ``corner`` of the ``box``, and assign it to the
local variable ``x``.”

While we are on the subject of composition, I should point out that you
can, in fact, create the ``Point`` and the ``Rectangle`` at the same
time:

::

     Rectangle box = { { 0.0, 0.0 }, 100.0, 200.0 };

The innermost squiggly braces are the coordinates of the corner point;
together they make up the first of the three values that go into the new
``Rectangle``. This statement is an example of **nested structure**.

Structures as return types
--------------------------

You can write functions that return structures. For example,
``findCenter`` takes a ``Rectangle`` as an argument and returns a
``Point`` that contains the coordinates of the center of the
``Rectangle``:

::

   Point findCenter (Rectangle& box)
   {
     double x = box.corner.x + box.width/2;
     double y = box.corner.y + box.height/2;
     Point result = {x, y};
     return result;
   }

To call this function, we have to pass a box as an argument (notice that
it is being passed by reference), and assign the return value to a
``Point`` variable:

::

     Rectangle box = { {0.0, 0.0}, 100, 200 };
     Point center = findCenter (box);
     printPoint (center);

The output of this program is ``(50, 100)``.

Passing other types by reference
--------------------------------

It’s not just structures that can be passed by reference. All the other
types we’ve seen can, too. For example, to swap two integers, we could
write something like:

::

   void swap (int& x, int& y)
   {
     int temp = x;
     x = y;
     y = temp;
   }

We would call this function in the usual way:

::

     int i = 7;
     int j = 9;
     swap (i, j);
     cout << i << j << endl;

The output of this program is ``97``. Draw a stack diagram for this
program to convince yourself this is true. If the parameters ``x`` and
``y`` were declared as regular parameters (without the ``&``\ s),
``swap`` would not work. It would modify ``x`` and ``y`` and have no
effect on ``i`` and ``j``.

When people start passing things like integers by reference, they often
try to use an expression as a reference argument. For example:

::

     int i = 7;
     int j = 9;
     swap (i, j+1);         // WRONG!!

This is not legal because the expression ``j+1`` is not a variable—it
does not occupy a location that the reference can refer to. It is a
little tricky to figure out exactly what kinds of expressions can be
passed by reference. For now a good rule of thumb is that reference
arguments have to be variables.

.. _input:

Getting user input
------------------

The programs we have written so far are pretty predictable; they do the
same thing every time they run. Most of the time, though, we want
programs that take input from the user and respond accordingly.

There are many ways to get input, including keyboard input, mouse
movements and button clicks, as well as more exotic mechanisms like
voice control and retinal scanning. In this text we will consider only
keyboard input.

In the header file ``iostream``, C++ defines an object named ``cin``
that handles input in much the same way that ``cout`` handles output. To
get an integer value from the user:

::

     int x;
     cin >> x;

The ``>>`` operator causes the program to stop executing and wait for
the user to type something. If the user types a valid integer, the
program converts it into an integer value and stores it in ``x``.

If the user types something other than an integer, C++ doesn’t report an
error, or anything sensible like that. Instead, it puts some meaningless
value in ``x`` and continues.

Fortunately, there is a way to check and see if an input statement
succeeds. We can invoke the ``good`` function on ``cin`` to check what
is called the **stream state**. ``good`` returns a ``bool``: if true,
then the last input statement succeeded. If not, we know that some
previous operation failed, and also that the next operation will fail.

Thus, getting input from the user might look like this:

::

   #include <iostream>

   using namespace std;

   int main ()
   {
     int x;

     // prompt the user for input
     cout << "Enter an integer: ";

     // get input
     cin >> x;

     // check and see if the input statement succeeded
     if (cin.good() == false) {
       cout << "That was not an integer." << endl;
       return -1;
     }

     // print the value we got from the user
     cout << x << endl;
     return 0;
   }

``cin`` can also be used to input a ``string``:

::

     string name;

     cout << "What is your name? ";
     cin >> name;
     cout << name << endl;

Unfortunately, this statement only takes the first word of input, and
leaves the rest for the next input statement. So, if you run this
program and type your full name, it will only output your first name.

Because of these problems (inability to handle errors and funny
behavior), I avoid using the ``>>`` operator altogether, unless I am
reading data from a source that is known to be error-free.

Instead, I use a function in the header ``string`` called ``getline``.

::

     string name;

     cout << "What is your name? ";
     getline (cin, name);
     cout << name << endl;

The first argument to ``getline`` is ``cin``, which is where the input
is coming from. The second argument is the name of the ``string`` where
you want the result to be stored.

``getline`` reads the entire line until the user hits Return or Enter.
This is useful for inputting strings that contain spaces.

In fact, ``getline`` is generally useful for getting input of any kind.
For example, if you wanted the user to type an integer, you could input
a string and then check to see if it is a valid integer. If so, you can
convert it to an integer value. If not, you can print an error message
and ask the user to try again.

To convert a string to an integer you can use the ``atoi`` function
defined in the header file ``cstdlib``. We will get to that in
Section `[parsing] <#parsing>`__.

Glossary
--------

structure:
   A collection of data grouped together and treated as a single object.

instance variable:
   One of the named pieces of data that make up a structure.

reference:
   A value that indicates or refers to a variable or structure. In a
   state diagram, a reference appears as an arrow.

pass by value:
   A method of parameter-passing in which the value provided as an
   argument is copied into the corresponding parameter, but the
   parameter and the argument occupy distinct locations.

pass by reference:
   A method of parameter-passing in which the parameter is a reference
   to the argument variable. Changes to the parameter also affect the
   argument variable.
