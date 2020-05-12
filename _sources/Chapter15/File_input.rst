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

.. activecode:: fifteen_one_one
  :language: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
     int x;
     apstring line;

     infile >> x;               // get a single integer and store in x
     getline (infile, line);    // get a whole line and store in line
    }

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


.. activecode:: fifteen_one_two
  :language: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
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

.. dragndrop:: dragndrop_fifteen_two
    :feedback: Try again!
    :match_1:  The constructor is|||ifstream.
    :match_2: The argument and the name of the file you want to open is|||"file-name".
    :match_3: The result of this code snippet is an object named|||infile.
    :match_4: The result of this code snippet supports the same operators as|||cin.

    Consider this code snippet: ``ifstream infile ("file-name");`` Finish each sentence.

.. fillintheblank:: fill_15.3

    The ``ifstream`` member function called ____ makes sure the file was opened successfully.

    - :(?:g|G)(?:o|O)(?:o|O)(?:d|D): Correct!
      :.*: Try again!

.. fillintheblank:: fill_15.3_two

    The ``ifstream`` member function called ____ detects the end of the file.

    - :(?:e|E)(?:o|O)(?:f|F): Correct!
      :.*: Try again!

.. mchoice:: test_question_fifteen_one
   :practice: T
   :answer_a: ...the ifstream constructor expects a C string as an argument.
   :answer_b: ...you need to make sure you have permission to read the file.
   :answer_c: ...it will check whether you have an infinite loop or not.
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again!
   :feedback_c: Try again!


   We need to use the function c_str to convert an apstring to a native C string because...


.. fillintheblank:: fill_15.3_three

    The ____ statement allows us to exit the loop as soon as we detect the end of the file.

    - :(?:b|B)(?:r|R)(?:e|E)(?:a|A)(?:k|K): Correct!
      :.*: Try again!

.. parsonsprob:: question_15.3

   Create a code block that reads lines from a file and prints them out. First, make sure that the file is able to be opened.
   -----
   int main () {
   =====
    aprstring name_of_file = ...;
   =====
    ifstream in_file (name_of_file.c_str());
   =====
    if (in_file.good() == false) {
   =====
      cout << "Unable to open the file named " << name_of_file;
   =====
      exit(1);
    }
   =====
    while (true) {
   =====
      getline(in_file, line);
   =====
      if (in_file.eof()) break;
   =====
      cout << line << endl;
    }
    }
