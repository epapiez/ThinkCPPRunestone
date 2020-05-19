File Input/Output and ``apmatrix``\ es
======================================

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

Streams
-------

To get input from a file or send output to a file, you have to create an
``ifstream`` object (for input files) or an ``ofstream`` object (for
output files). These objects are defined in the header file ``fstream``,
which you have to include.

A **stream** is an abstract object that represents the flow of data from
a source like the keyboard or a file to a destination like the screen or
a file.

We have already worked with two streams: ``cin``, which has type
``istream``, and ``cout``, which has type ``ostream``. ``cin``
represents the flow of data from the keyboard to the program. Each time
the program uses the ``>>`` operator or the ``getline`` function, it
removes a piece of data from the input stream.

Similarly, when the program uses the ``<<`` operator on an ``ostream``,
it adds a datum to the outgoing stream.

.. _finput:

File input
----------

To get data from a file, we have to create a stream that flows from the
file into the program. We can do that using the ``ifstream``
constructor.

::

     ifstream infile ("file-name");

The argument for this constructor is a string that contains the name of
the file you want to open. The result is an object named ``infile`` that
supports all the same operations as ``cin``, including ``>>`` and
``getline``.

::

     int x;
     apstring line;

     infile >> x;               // get a single integer and store in x
     getline (infile, line);    // get a whole line and store in line

If we know ahead of time how much data is in a file, it is
straightforward to write a loop that reads the entire file and then
stops. More often, though, we want to read the entire file, but don’t
know how big it is.

There are member functions for ``ifstreams`` that check the status of
the input stream; they are called ``good``, ``eof``, ``fail`` and
``bad``. We will use ``good`` to make sure the file was opened
successfully and ``eof`` to detect the “end of file.”

Whenever you get data from an input stream, you don’t know whether the
attempt succeeded until you check. If the return value from ``eof`` is
``true`` then we have reached the end of the file and we know that the
last attempt failed. Here is a program that reads lines from a file and
displays them on the screen:

::

     apstring fileName = ...;
     ifstream infile (fileName.c_str());

     if (infile.good() == false) {
       cout << "Unable to open the file named " << fileName;
       exit (1);
     }

     while (true) {
       getline (infile, line);
       if (infile.eof()) break;
       cout << line << endl;
     }

The function ``c_str`` converts an ``apstring`` to a native C string.
Because the ``ifstream`` constructor expects a C string as an argument,
we have to convert the ``apstring``.

Immediately after opening the file, we invoke the ``good`` function. The
return value is ``false`` if the system could not open the file, most
likely because it does not exist, or you do not have permission to read
it.

The statement ``while(true)`` is an idiom for an infinite loop. Usually
there will be a ``break`` statement somewhere in the loop so that the
program does not really run forever (although some programs do). In this
case, the ``break`` statement allows us to exit the loop as soon as we
detect the end of file.

It is important to exit the loop between the input statement and the
output statement, so that when ``getline`` fails at the end of the file,
we do not output the invalid data in ``line``.

File output
-----------

Sending output to a file is similar. For example, we could modify the
previous program to copy lines from one file to another.

::

     ifstream infile ("input-file");
     ofstream outfile ("output-file");

     if (infile.good() == false || outfile.good() == false) {
       cout << "Unable to open one of the files." << endl;
       exit (1);
     }

     while (true) {
       getline (infile, line);
       if (infile.eof()) break;
       outfile << line << endl;
     }

.. _parsing:

Parsing input
-------------

In Section `[formal] <#formal>`__ I defined “parsing” as the process of
analyzing the structure of a sentence in a natural language or a
statement in a formal language. For example, the compiler has to parse
your program before it can translate it into machine language.

In addition, when you read input from a file or from the keyboard you
often have to parse it in order to extract the information you want and
detect errors.

For example, I have a file called ``distances`` that contains
information about the distances between major cities in the United
States. I got this information from a randomly-chosen web page

::

   http://www.jaring.my/usiskl/usa/distance.html

so it may be wildly inaccurate, but that doesn’t matter. The format of
the file looks like this:

::

   "Atlanta"       "Chicago"       700
   "Atlanta"       "Boston"        1,100
   "Atlanta"       "Chicago"       700
   "Atlanta"       "Dallas"        800
   "Atlanta"       "Denver"        1,450
   "Atlanta"       "Detroit"       750
   "Atlanta"       "Orlando"       400

Each line of the file contains the names of two cities in quotation
marks and the distance between them in miles. The quotation marks are
useful because they make it easy to deal with names that have more than
one word, like “San Francisco.”

By searching for the quotation marks in a line of input, we can find the
beginning and end of each city name. Searching for special characters
like quotation marks can be a little awkward, though, because the
quotation mark is a special character in C++, used to identify string
values.

If we want to find the first appearance of a quotation mark, we have to
write something like:

::

     int index = line.find ('\"');

The argument here looks like a mess, but it represents a single
character, a double quotation mark. The outermost single-quotes indicate
that this is a character value, as usual. The backslash (``\``)
indicates that we want to treat the next character literally. The
sequence ``\"`` represents a quotation mark; the sequence ``\'``
represents a single-quote. Interestingly, the sequence ``\\`` represents
a single backslash. The first backslash indicates that we should take
the second backslash seriously.

Parsing input lines consists of finding the beginning and end of each
city name and using the ``substr`` function to extract the cities and
distance. ``substr`` is an ``apstring`` member function; it takes two
arguments, the starting index of the substring and the length.

::

   void processLine (const apstring& line)
   {
     // the character we are looking for is a quotation mark
     char quote = '\"';

     // store the indices of the quotation marks in a vector
     apvector<int> quoteIndex (4);

     // find the first quotation mark using the built-in find
     quoteIndex[0] = line.find (quote);

     // find the other quotation marks using the find from Chapter 7
     for (int i=1; i<4; i++) {
       quoteIndex[i] = find (line, quote, quoteIndex[i-1]+1);
     }

     // break the line up into substrings
     int len1 = quoteIndex[1] - quoteIndex[0] - 1;
     apstring city1 = line.substr (quoteIndex[0]+1, len1);
     int len2 = quoteIndex[3] - quoteIndex[2] - 1;
     apstring city2 = line.substr (quoteIndex[2]+1, len2);
     int len3 = line.length() - quoteIndex[2] - 1;
     apstring distString = line.substr (quoteIndex[3]+1, len3);

     // output the extracted information
     cout << city1 << "\t" << city2 << "\t" << distString << endl;
   }

Of course, just displaying the extracted information is not exactly what
we want, but it is a good starting place.

Parsing numbers
---------------

The next task is to convert the numbers in the file from strings to
integers. When people write large numbers, they often use commas to
group the digits, as in 1,750. Most of the time when computers write
large numbers, they don’t include commas, and the built-in functions for
reading numbers usually can’t handle them. That makes the conversion a
little more difficult, but it also provides an opportunity to write a
comma-stripping function, so that’s ok. Once we get rid of the commas,
we can use the library function ``atoi`` to convert to integer. ``atoi``
is defined in the header file ``cstdlib``.

To get rid of the commas, one option is to traverse the string and check
whether each character is a digit. If so, we add it to the result
string. At the end of the loop, the result string contains all the
digits from the original string, in order.

::

   int convertToInt (const apstring& s)
   {
     apstring digitString = "";

     for (int i=0; i<s.length(); i++) {
       if (isdigit (s[i])) {
         digitString += s[i];
       }
     }
     return atoi (digitString.c_str());
   }

The variable ``digitString`` is an example of an **accumulator**. It is
similar to the counter we saw in Section `[loopcount] <#loopcount>`__,
except that instead of getting incremented, it gets accumulates one new
character at a time, using string concatentation.

The expression

::

         digitString += s[i];

is equivalent to

::

         digitString = digitString + s[i];

Both statements add a single character onto the end of the existing
string.

Since ``atoi`` takes a C string as a parameter, we have to convert
``digitString`` to a C string before passing it as an argument.

The ``Set`` data structure
--------------------------

A data structure is a container for grouping a collection of data into a
single object. We have seen some examples already, including
``apstring``\ s, which are collections of characters, and
``apvector``\ s which are collections on any type.

An ordered set is a collection of items with two defining properties:

Ordering:
   The elements of the set have indices associated with them. We can use
   these indices to identify elements of the set.

Uniqueness:
   No element appears in the set more than once. If you try to add an
   element to a set, and it already exists, there is no effect.

In addition, our implementation of an ordered set will have the
following property:

Arbitrary size:
   As we add elements to the set, it expands to make room for new
   elements.

Both ``apstring``\ s and ``apvector``\ s have an ordering; every element
has an index we can use to identify it. Both none of the data structures
we have seen so far have the properties of uniqueness or arbitrary size.

To achieve uniqueness, we have to write an ``add`` function that
searches the set to see if it already exists. To make the set expand as
elements are added, we can take advantage of the ``resize`` function on
``apvector``\ s.

Here is the beginning of a class definition for a ``Set``.

::

   class Set {
   private:
     apvector<apstring> elements;
     int numElements;

   public:
     Set (int n);

     int getNumElements () const;
     apstring getElement (int i) const;
     int find (const apstring& s) const;
     int add (const apstring& s);
   };

   Set::Set (int n)
   {
     apvector<apstring> temp (n);
     elements = temp;
     numElements = 0;
   }

The instance variables are an ``apvector`` of strings and an integer
that keeps track of how many elements there are in the set. Keep in mind
that the number of elements in the set, ``numElements``, is not the same
thing as the size of the ``apvector``. Usually it will be smaller.

The ``Set`` constructor takes a single parameter, which is the initial
size of the ``apvector``. The initial number of elements is always zero.

``getNumElements`` and ``getElement`` are accessor functions for the
instance variables, which are private. ``numElements`` is a read-only
variable, so we provide a ``get`` function but not a ``set`` function.

::

   int Set::getNumElements () const
   {
     return numElements;
   }

Why do we have to prevent client programs from changing
``getNumElements``? What are the invariants for this type, and how could
a client program break an invariant. As we look at the rest of the
``Set`` member function, see if you can convince yourself that they all
maintain the invariants.

When we use the ``[]`` operator to access the ``apvector``, it checks to
make sure the index is greater than or equal to zero and less than the
length of the ``apvector``. To access the elements of a set, though, we
need to check a stronger condition. The index has to be less than the
number of elements, which might be smaller than the length of the
``apvector``.

::

   apstring Set::getElement (int i) const
   {
     if (i < numElements) {
       return elements[i];
     } else {
       cout << "Set index out of range." << endl;
       exit (1);
     }
   }

If ``getElement`` gets an index that is out of range, it prints an error
message (not the most useful message, I admit), and exits.

The interesting functions are ``find`` and ``add``. By now, the pattern
for traversing and searching should be old hat:

::

   int Set::find (const apstring& s) const
   {
     for (int i=0; i<numElements; i++) {
       if (elements[i] == s) return i;
     }
     return -1;
   }

So that leaves us with ``add``. Often the return type for something like
``add`` would be void, but in this case it might be useful to make it
return the index of the element.

::

   int Set::add (const apstring& s)
   {
     // if the element is already in the set, return its index
     int index = find (s);
     if (index != -1) return index;

     // if the apvector is full, double its size
     if (numElements == elements.length()) {
       elements.resize (elements.length() * 2);
     }

     // add the new elements and return its index
     index = numElements;
     elements[index] = s;
     numElements++;
     return index;
   }

The tricky thing here is that ``numElements`` is used in two ways. It is
the number of elements in the set, of course, but it is also the index
of the next element to be added.

It takes a minute to convince yourself that that works, but consider
this: when the number of elements is zero, the index of the next element
is 0. When the number of elements is equal to the length of the
``apvector``, that means that the vector is full, and we have to
allocate more space (using ``resize``) before we can add the new
element.

Here is a state diagram showing a ``Set`` object that initially contains
space for 2 elements.

Now we can use the ``Set`` class to keep track of the cities we find in
the file. In ``main`` we create the ``Set`` with an initial size of 2:

::

     Set cities (2);

Then in ``processLine`` we add both cities to the ``Set`` and store the
index that gets returned.

::

     int index1 = cities.add (city1);
     int index2 = cities.add (city2);

I modified ``processLine`` to take the ``cities`` object as a second
parameter.

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

A distance matrix
-----------------

Finally, we are ready to put the data from the file into a matrix.
Specifically, the matrix will have one row and one column for each city.

We’ll create the matrix in ``main``, with plenty of space to spare:

::

     apmatrix<int> distances (50, 50, 0);

Inside ``processLine``, we add new information to the matrix by getting
the indices of the two cities from the ``Set`` and using them as matrix
indices:

::

     int dist = convertToInt (distString);
     int index1 = cities.add (city1);
     int index2 = cities.add (city2);

     distances[index1][index2] = distance;
     distances[index2][index1] = distance;

Finally, in ``main`` we can print the information in a human-readable
form:

::

     for (int i=0; i<cities.getNumElements(); i++) {
       cout << cities.getElement(i) << "\t";

       for (int j=0; j<=i; j++) {
         cout << distances[i][j] << "\t";
       }
       cout << endl;
     }

     cout << "\t";
     for (int i=0; i<cities.getNumElements(); i++) {
       cout << cities.getElement(i) << "\t";
     }
     cout << endl;

This code produces the output shown at the beginning of the chapter. The
original data is available from this book’s web page.

A proper distance matrix
------------------------

Although this code works, it is not as well organized as it should be.
Now that we have written a prototype, we are in a good position to
evaluate the design and improve it.

What are some of the problems with the existing code?

#. We did not know ahead of time how big to make the distance matrix, so
   we chose an arbitrary large number (50) and made it a fixed size. It
   would be better to allow the distance matrix to expand in the same
   way a ``Set`` does. The ``apmatrix`` class has a function called
   ``resize`` that makes this possible.

#. The data in the distance matrix is not well-encapsulated. We have to
   pass the set of city names and the matrix itself as arguments to
   ``processLine``, which is awkward. Also, use of the distance matrix
   is error prone because we have not provided accessor functions that
   perform error-checking. It might be a good idea to take the ``Set``
   of city names and the ``apmatrix`` of distances, and combine them
   into a single object called a ``DistMatrix``.

Here is a draft of what the header for a ``DistMatrix`` might look like:

::

   class DistMatrix {
   private:
     Set cities;
     apmatrix<int> distances;

   public:
     DistMatrix (int rows);

     void add (const apstring& city1, const apstring& city2, int dist);
     int distance (int i, int j) const;
     int distance (const apstring& city1, const apstring& city2) const;
     apstring cityName (int i) const;
     int numCities () const;
     void print ();
   };

Using this interface simplifies ``main``:

::

   #include <iostream>
   #include <fstream>
   using namespace std;


   int main ()
   {
     apstring line;
     ifstream infile ("distances");
     DistMatrix distances (2);

     while (true) {
       getline (infile, line);
       if (infile.eof()) break;
       processLine (line, distances);
     }

     distances.print ();
     return 0;
   }

It also simplifies ``processLine``:

::

   void processLine (const apstring& line, DistMatrix& distances)
   {
     char quote = '\"';
     apvector<int> quoteIndex (4);
     quoteIndex[0] = line.find (quote);
     for (int i=1; i<4; i++) {
       quoteIndex[i] = find (line, quote, quoteIndex[i-1]+1);
     }

     // break the line up into substrings
     int len1 = quoteIndex[1] - quoteIndex[0] - 1;
     apstring city1 = line.substr (quoteIndex[0]+1, len1);
     int len2 = quoteIndex[3] - quoteIndex[2] - 1;
     apstring city2 = line.substr (quoteIndex[2]+1, len2);
     int len3 = line.length() - quoteIndex[2] - 1;
     apstring distString = line.substr (quoteIndex[3]+1, len3);
     int distance = convertToInt (distString);

     // add the new datum to the distances matrix
     distances.add (city1, city2, distance);
   }

I will leave it as an exercise to you to implement the member functions
of ``DistMatrix``.

Glossary
--------

ordered set:
   A data structure in which every element appears only once and every
   element has an index that identifies it.

stream:
   A data structure that represents a “flow” or sequence of data items
   from one place to another. In C++ streams are used for input and
   output.

accumulator:
   A variable used inside a loop to accumulate a result, often by
   getting something added or concatenated during each iteration.
