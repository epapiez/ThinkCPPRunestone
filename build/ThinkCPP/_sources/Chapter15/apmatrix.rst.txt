``apmatrix``
------------

An ``apmatrix`` is similar to an ``apvector`` except it is
two-dimensional. Instead of a length, it has two dimensions, called
``numrows`` and ``numcols``, for “number of rows” and “number of
columns.”

Each element in the matrix is indentified by two indices; one specifies
the row number, the other the column number.

To create a matrix, there are four constructors:

::

     apmatrix<char> m1;
     apmatrix<int> m2 (3, 4);
     apmatrix<double> m3 (rows, cols, 0.0);
     apmatrix<double> m4 (m3);

The first is a do-nothing constructor that makes a matrix with both
dimensions 0. The second takes two integers, which are the initial
number of rows and columns, in that order. The third is the same as the
second, except that it takes an additional parameter that is used to
initialized the elements of the matrix. The fourth is a copy constructor
that takes another ``apmatrix`` as a parameter.

Just as with ``apvectors``, we can make ``apmatrix``\ es with any type
of elements (including ``apvector``\ s, and even ``apmatrix``\ es).

To access the elements of a matrix, we use the ``[]`` operator to
specify the row and column:

::

     m2[0][0] = 1;
     m3[1][2] = 10.0 * m2[0][0];

If we try to access an element that is out of range, the program prints
an error message and quits.

The ``numrows`` and ``numcols`` functions get the number of rows and
columns. Remember that the row indices run from 0 to ``numrows() -1``
and the column indices run from 0 to ``numcols() -1``.

The usual way to traverse a matrix is with a nested loop. This loop sets
each element of the matrix to the sum of its two indices:

::

     for (int row=0; row < m2.numrows(); row++) {
       for (int col=0; col < m2.numcols(); col++) {
         m2[row][col] = row + col;
       }
     }

This loop prints each row of the matrix with tabs between the elements
and newlines between the rows:

::

     for (int row=0; row < m2.numrows(); row++) {
       for (int col=0; col < m2.numcols(); col++) {
         cout << m2[row][col] << "\t";
       }
       cout << endl;
     }
