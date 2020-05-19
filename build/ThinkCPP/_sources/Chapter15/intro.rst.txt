File Input/Output and ``apmatrix``\ es
---------------------------------------

In this chapter we will develop a program that reads and writes files,
parses input, and demonstrates the ``apmatrix`` class. We will also
implement a data structure called ``Set`` that expands automatically as
you add elements.

Aside from demonstrating all these features, the real purpose of the
program is to generate a two-dimensional table of the distances between
cities in the United States. The output is a table that looks like this:

::

   Atlanta 0
   Chicago 700     0
   Boston  1100    1000    0
   Dallas  800     900     1750    0
   Denver  1450    1000    2000    800     0
   Detroit 750     300     800     1150    1300    0
   Orlando 400     1150    1300    1100    1900    1200    0
   Phoenix 1850    1750    2650    1000    800     2000    2100    0
   Seattle 2650    2000    3000    2150    1350    2300    3100    1450    0
           Atlanta Chicago Boston  Dallas  Denver  Detroit Orlando Phoenix Seattle

The diagonal elements are all zero because that is the distance from a
city to itself. Also, because the distance from A to B is the same as
the distance from B to A, there is no need to print the top half of the
matrix.
