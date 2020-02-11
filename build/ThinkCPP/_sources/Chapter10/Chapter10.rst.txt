Vectors
=======

A **vector** is a set of values where each value is identified by a
number (called an index). An ``string`` is similar to a vector, since it
is made up of an indexed set of characters. The nice thing about vectors
is that they can be made up of any type of element, including basic
types like ``int``\ s and ``double``\ s, and user-defined types like
``Point`` and ``Time``.

The ``vector`` type is defined in the C++ Standard Template Library
(STL). In order to use it, you have to include the header file
``vector``; again, the details of how to do that depend on your
programming environment.

You can create a vector the same way you create other variable types:

::

     vector<int> count;
     vector<double> doubleVector;

The type that makes up the vector appears in angle brackets (``<`` and
``>``). The first line creates a vector of integers named ``count``; the
second creates a vector of ``double``\ s. Although these statements are
legal, they are not very useful because they create vectors that have no
elements (their size is zero). It is more common to specify the size of
the vector in parentheses:

::

     vector<int> count (4);

The syntax here is a little odd; it looks like a combination of a
variable declarations and a function call. In fact, that’s exactly what
it is. The function we are invoking is an ``vector`` constructor. A
**constructor** is a special function that creates new objects and
initializes their instance variables. In this case, the constructor
takes a single argument, which is the size of the new vector.

The following figure shows how vectors are represented in state
diagrams:

The large numbers inside the boxes are the **elements** of the vector.
The small numbers outside the boxes are the indices used to identify
each box. When you allocate a new vector, the elements are not
initialized. They could contain any values.

There is another constructor for ``vector``\ s that takes two
parameters; the second is a “fill value,” the value that will be
assigned to each of the elements.

::

     vector<int> count (4, 0);

This statement creates a vector of four elements and initializes all of
them to zero.

Accessing elements
------------------

The ``[]`` operator reads and writes the elements of a vector in much
the same way it accesses the characters in an ``apstring``. As with
``apstring``\ s, the indices start at zero, so ``count[0]`` refers to
the “zeroeth” element of the vector, and ``count[1]`` refers to the
“oneth” element. You can use the ``[]`` operator anywhere in an
expression:

::

     count[0] = 7;
     count[1] = count[0] * 2;
     count[2]++;
     count[3] -= 60;

All of these are legal assignment statements. Here is the effect of this
code fragment:

Since elements of this vector are numbered from 0 to 3, there is no
element with the index 4. It is a common error to go beyond the bounds
of a vector, which causes a run-time error. The program outputs an error
message like “Illegal vector index”, and then quits.

You can use any expression as an index, as long as it has type ``int``.
One of the most common ways to index a vector is with a loop variable.
For example:

::

     int i = 0;
     while (i < 4) {
       cout << count[i] << endl;
       i++;
     }

This ``while`` loop counts from 0 to 4; when the loop variable ``i`` is
4, the condition fails and the loop terminates. Thus, the body of the
loop is only executed when ``i`` is 0, 1, 2 and 3.

Each time through the loop we use ``i`` as an index into the vector,
outputting the ``i``\ th element. This type of vector traversal is very
common. Vectors and loops go together like fava beans and a nice
Chianti.

Copying vectors
---------------

There is one more constructor for ``vector``\ s, which is called a copy
constructor because it takes one ``vector`` as an argument and creates a
new vector that is the same size, with the same elements.

::

     vector<int> copy (count);

Although this syntax is legal, it is almost never used for ``vector``\ s
because there is a better alternative:

::

     vector<int> copy = count;

The ``=`` operator works on ``vector``\ s in pretty much the way you
would expect.

``for`` loops
-------------

The loops we have written so far have a number of elements in common.
All of them start by initializing a variable; they have a test, or
condition, that depends on that variable; and inside the loop they do
something to that variable, like increment it.

This type of loop is so common that there is an alternate loop
statement, called ``for``, that expresses it more concisely. The general
syntax looks like this:

::

     for (INITIALIZER; CONDITION; INCREMENTOR) {
       BODY
     }

This statement is exactly equivalent to

::

     INITIALIZER;
     while (CONDITION) {
       BODY
       INCREMENTOR
     }

except that it is more concise and, since it puts all the loop-related
statements in one place, it is easier to read. For example:

::

     int i;
     for (i = 0; i < 4; i++) {
       cout << count[i] << endl;
     }

is equivalent to

::

     int i = 0;
     while (i < 4) {
       cout << count[i] << endl;
       i++;
     }

Vector size
-----------

There are a few functions you can invoke on an ``vector``. One of them
is very useful, though: ``size()``. Not surprisingly, it returns the
size of the vector (the number of elements).

It is a good idea to use this value as the upper bound of a loop, rather
than a constant. That way, if the size of the vector changes, you won’t
have to go through the program changing all the loops; they will work
correctly for any size vector.

::

     int i;
     for (i = 0; i < count.size(); i++) {
       cout << count[i] << endl;
     }

The last time the body of the loop gets executed, the value of ``i`` is
``count.size() - 1``, which is the index of the last element. When ``i``
is equal to ``count.size()``, the condition fails and the body is not
executed, which is a good thing, since it would cause a run-time error.
One thing that we should notice here is that the size() function is
called every time the loop is executed. Calling a function again and
again reduces execution speed, so it would be better to store the size
in some variable by calling the ``size()`` function before the loop
begins, and use this variable to check for the last element. You can try
this program as an excercise.

Vector functions
----------------

The best feature of a vector is its resizeability A vector, once
declared, can be resized from anywhere within the program. Suppose we
have a situation where we input numbers from the user and store them in
a vector till he inputs ``-1``, and then display them. In such a case,
we do not know the size of the vector beforehand. So we need wish add
new values to the end of a vector as the user inputs them. We can use
then vector function ``push_back()`` for that purpose.

::

     #include<iostream>
     #include<vector>
     using namespace std;
     int main()
     {
       vector<int> values;
       int c,i,len;
       cin>>c;

       while(c != -1) {
         values.push_back(c);
         cin >> c;
       }
       len=values.size();
       for(i = 0; i < len; i++) {
         cout << values[i] << endl;
       }
     }

.. _random:

Random numbers
--------------

[pseudorandom]

Most computer programs do the same thing every time they are executed,
so they are said to be **deterministic**. Usually, determinism is a good
thing, since we expect the same calculation to yield the same result.
For some applications, though, we would like the computer to be
unpredictable. Games are an obvious example.

Making a program truly **nondeterministic** turns out to be not so easy,
but there are ways to make it at least seem nondeterministic. One of
them is to generate pseudorandom numbers and use them to determine the
outcome of the program. Pseudorandom numbers are not truly random in the
mathematical sense, but for our purposes, they will do.

C++ provides a function called ``random`` that generates pseudorandom
numbers. It is declared in the header file ``cstdlib``, which contains a
variety of “standard library” functions, hence the name.

The return value from ``random`` is an integer between 0 and
``RAND_MAX``, where ``RAND_MAX`` is a large number (about 2 billion on
my computer) also defined in the header file. Each time you call
``random`` you get a different randomly-generated number. To see a
sample, run this loop:

::

   #include <iostream>
   #include <cstdlib>
   using namespace std;

   int main ()
   {
     for (int i = 0; i < 4; i++) {
       int x = random ();
       cout << x << endl;
     }
     return 0;
   }

On my machine I got the following output:

::

   1804289383
   846930886
   1681692777
   1714636915

You will probably get something similar, but different, on yours.

Of course, we don’t always want to work with gigantic integers. More
often we want to generate integers between 0 and some upper bound. A
simple way to do that is with the modulus operator. For example:

::

     int x = random ();
     int y = x % upperBound;

Since ``y`` is the remainder when ``x`` is divided by ``upperBound``,
the only possible values for ``y`` are between 0 and ``upperBound - 1``,
including both end points. Keep in mind, though, that ``y`` will never
be equal to ``upperBound``.

It is also frequently useful to generate random floating-point values. A
common way to do that is by dividing by ``RAND_MAX``. For example:

::

     int x = random ();
     double y = double(x) / RAND_MAX;

This code sets ``y`` to a random value between 0.0 and 1.0, including
both end points. As an exercise, you might want to think about how to
generate a random floating-point value in a given range; for example,
between 100.0 and 200.0.

Statistics
----------

The numbers generated by ``random`` are supposed to be distributed
uniformly. That means that each value in the range should be equally
likely. If we count the number of times each value appears, it should be
roughly the same for all values, provided that we generate a large
number of values.

In the next few sections, we will write programs that generate a
sequence of random numbers and check whether this property holds true.

Vector of random numbers
------------------------

The first step is to generate a large number of random values and store
them in a vector. By “large number,” of course, I mean 20. It’s always a
good idea to start with a manageable number, to help with debugging, and
then increase it later.

The following function takes a single argument, the size of the vector.
It allocates a new vector of ``int``\ s, and fills it with random values
between 0 and ``upperBound-1``.

::

   vector<int> randomVector (int n, int upperBound) {
     vector<int> vec (n);
     for (int i = 0; i<vec.size(); i++) {
       vec[i] = random () % upperBound;
     }
     return vec;
   }

The return type is ``vector<int>``, which means that this function
returns a vector of integers. To test this function, it is convenient to
have a function that outputs the contents of a vector.

::

   void printVector (const vector<int>& vec) {
     for (int i = 0; i<vec.size(); i++) {
       cout << vec[i] << " ";
     }
   }

Notice that it is legal to pass ``vector``\ s by reference. In fact it
is quite common, since it makes it unnecessary to copy the vector. Since
``printVector`` does not modify the vector, we declare the parameter
``const``.

The following code generates a vector and outputs it:

::

     int numValues = 20;
     int upperBound = 10;
     vector<int> vector = randomVector (numValues, upperBound);
     printVector (vector);

On my machine the output is

::

   3 6 7 5 3 5 6 2 9 1 2 7 0 9 3 6 0 6 2 6

which is pretty random-looking. Your results may differ.

If these numbers are really random, we expect each digit to appear the
same number of times—twice each. In fact, the number 6 appears five
times, and the numbers 4 and 8 never appear at all.

Do these results mean the values are not really uniform? It’s hard to
tell. With so few values, the chances are slim that we would get exactly
what we expect. But as the number of values increases, the outcome
should be more predictable.

To test this theory, we’ll write some programs that count the number of
times each value appears, and then see what happens when we increase
``numValues``.

Counting
--------

A good approach to problems like this is to think of simple functions
that are easy to write, and that might turn out to be useful. Then you
can combine them into a solution. This approach is sometimes called
**bottom-up design**. Of course, it is not easy to know ahead of time
which functions are likely to be useful, but as you gain experience you
will have a better idea.

Also, it is not always obvious what sort of things are easy to write,
but a good approach is to look for subproblems that fit a pattern you
have seen before.

Back in Section `[loopcount] <#loopcount>`__ we looked at a loop that
traversed a string and counted the number of times a given letter
appeared. You can think of this program as an example of a pattern
called “traverse and count.” The elements of this pattern are:

-  A set or container that can be traversed, like a string or a vector.

-  A test that you can apply to each element in the container.

-  A counter that keeps track of how many elements pass the test.

In this case, I have a function in mind called ``howMany`` that counts
the number of elements in a vector that equal a given value. The
parameters are the vector and the integer value we are looking for. The
return value is the number of times the value appears.

::

   int howMany (const vector<int>& vec, int value) {
     int count = 0;
     for (int i=0; i< vec.size(); i++) {
       if (vec[i] == value) count++;
     }
     return count;
   }

Checking the other values
-------------------------

``howMany`` only counts the occurrences of a particular value, and we
are interested in seeing how many times each value appears. We can solve
that problem with a loop:

::

     int numValues = 20;
     int upperBound = 10;
     vector<int> vector = randomVector (numValues, upperBound);

     cout << "value\thowMany";

     for (int i = 0; i<upperBound; i++) {
       cout << i << '\t' << howMany (vector, i) << endl;
     }

Notice that it is legal to declare a variable inside a ``for``
statement. This syntax is sometimes convenient, but you should be aware
that a variable declared inside a loop only exists inside the loop. If
you try to refer to ``i`` later, you will get a compiler error.

This code uses the loop variable as an argument to ``howMany``, in order
to check each value between 0 and 9, in order. The result is:

::

   value   howMany
   0       2
   1       1
   2       3
   3       3
   4       0
   5       2
   6       5
   7       2
   8       0
   9       2

Again, it is hard to tell if the digits are really appearing equally
often. If we increase ``numValues`` to 100,000 we get the following:

::

   value   howMany
   0       10130
   1       10072
   2       9990
   3       9842
   4       10174
   5       9930
   6       10059
   7       9954
   8       9891
   9       9958

In each case, the number of appearances is within about 1% of the
expected value (10,000), so we conclude that the random numbers are
probably uniform.

A histogram
-----------

It is often useful to take the data from the previous tables and store
them for later access, rather than just print them. What we need is a
way to store 10 integers. We could create 10 integer variables with
names like ``howManyOnes``, ``howManyTwos``, etc. But that would require
a lot of typing, and it would be a real pain later if we decided to
change the range of values.

A better solution is to use a vector with size 10. That way we can
create all ten storage locations at once and we can access them using
indices, rather than ten different names. Here’s how:

::

     int numValues = 100000;
     int upperBound = 10;
     vector<int> vector = randomVector (numValues, upperBound);
     vector<int> histogram (upperBound);

     for (int i = 0; i<upperBound; i++) {
       int count = howMany (vector, i);
       histogram[i] = count;
     }

I called the vector **histogram** because that’s a statistical term for
a vector of numbers that counts the number of appearances of a range of
values.

The tricky thing here is that I am using the loop variable in two
different ways. First, it is an argument to ``howMany``, specifying
which value I am interested in. Second, it is an index into the
histogram, specifying which location I should store the result in.

A single-pass solution
----------------------

Although this code works, it is not as efficient as it could be. Every
time it calls ``howMany``, it traverses the entire vector. In this
example we have to traverse the vector ten times!

It would be better to make a single pass through the vector. For each
value in the vector we could find the corresponding counter and
increment it. In other words, we can use the value from the vector as an
index into the histogram. Here’s what that looks like:

::

     vector<int> histogram (upperBound, 0);

     for (int i = 0; i<numValues; i++) {
       int index = vector[i];
       histogram[index]++;
     }

The first line initializes the elements of the histogram to zeroes. That
way, when we use the increment operator (``++``) inside the loop, we
know we are starting from zero. Forgetting to initialize counters is a
common error.

As an exercise, encapsulate this code in a function called ``histogram``
that takes a vector and the range of values in the vector (in this case
0 through 10), and that returns a histogram of the values in the vector.

Random seeds
------------

If you have run the code in this chapter a few times, you might have
noticed that you are getting the same “random” values every time. That’s
not very random!

One of the properties of pseudorandom number generators is that if they
start from the same place they will generate the same sequence of
values. The starting place is called a **seed**; by default, C++ uses
the same seed every time you run the program.

While you are debugging, it is often helpful to see the same sequence
over and over. That way, when you make a change to the program you can
compare the output before and after the change.

If you want to choose a different seed for the random number generator,
you can use the ``srand`` function. It takes a single argument, which is
an integer between 0 and ``RAND_MAX``.

For many applications, like games, you want to see a different random
sequence every time the program runs. A common way to do that is to use
a library function like ``gettimeofday`` to generate something
reasonably unpredictable and unrepeatable, like the number of
milliseconds since the last second tick, and use that number as a seed.
The details of how to do that depend on your development environment.

Glossary
--------

vector:
   A named collection of values, where all the values have the same
   type, and each value is identified by an index.

element:
   One of the values in a vector. The ``[]`` operator selects elements
   of a vector.

index:
   An integer variable or value used to indicate an element of a vector.

constructor:
   A special function that creates a new object and initializes its
   instance variables.

deterministic:
   A program that does the same thing every time it is run.

pseudorandom:
   A sequence of numbers that appear to be random, but which are
   actually the product of a deterministic computation.

seed:
   A value used to initialize a random number sequence. Using the same
   seed should yield the same sequence of values.

bottom-up design:
   A method of program development that starts by writing small, useful
   functions and then assembling them into larger solutions.

histogram:
   A vector of integers where each integer counts the number of values
   that fall into a certain range.
