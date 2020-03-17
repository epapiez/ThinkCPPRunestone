``string``\ s are comparable
----------------------------

All the comparison operators that work on ``int``\ s and ``double``\ s
also work on ``strings``. For example, if you want to know if two
strings are equal:

::

     if (word == "banana") {
       cout << "Yes, we have no bananas!" << endl;
     }

The other comparison operations are useful for putting words in
alphabetical order.

::

     if (word < "banana") {
       cout << "Your word, " << word << ", comes before banana." << endl;
     } else if (word > "banana") {
       cout << "Your word, " << word << ", comes after banana." << endl;
     } else {
       cout << "Yes, we have no bananas!" << endl;
     }

You should be aware, though, that the ``string`` class does not handle
upper and lower case letters the same way that people do. All the upper
case letters come before all the lower case letters. As a result,

::

   Your word, Zebra, comes before banana.

A common way to address this problem is to convert strings to a standard
format, like all lower-case, before performing the comparison. The next
sections explains how. I will not address the more difficult problem,
which is making the program realize that zebras are not fruit.
