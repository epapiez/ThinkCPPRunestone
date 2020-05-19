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
