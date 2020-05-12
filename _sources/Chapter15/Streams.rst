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

.. fillintheblank:: fill_15.1

    To get input from a file, you have to create an _______ object.

    - :(?:i|I)(?:f|F)(?:s|S)(?:t|T)(?:r|R)(?:e|E)(?:a|A)(?:m|M): Is the correct answer!
      :.*: 25 in octal please

.. fillintheblank:: fill_15.1_2

    To send output to a file, you have to create an _______ object.

    - :(?:o|O)(?:f|F)(?:s|S)(?:t|T)(?:r|R)(?:e|E)(?:a|A)(?:m|M): Is the correct answer!
      :.*: 25 in octal please

.. fillintheblank:: fill_15.1_3

    In order to define objects to input from a file or send output to a file, you must include the _____ header file.

    - :(?:f|F)(?:s|S)(?:t|T)(?:r|R)(?:e|E)(?:a|A)(?:m|M): Is the correct answer!
      :.*: 25 in octal please

.. fillintheblank:: fill_15.1_4

    A _________ is an abstract object that represents the flow of data from a source like the keyboard or a file to a destination like the screen or a file.

    - :(?:s|S)(?:t|T)(?:r|R)(?:e|E)(?:a|A)(?:m|M): Is the correct answer!
      :.*: 25 in octal please

.. dragndrop:: dragndrop_fifteen_one
    :feedback: Try again!
    :match_1: cin|||istream
    :match_2: cout|||ofstream

    Match the stream to its type.
