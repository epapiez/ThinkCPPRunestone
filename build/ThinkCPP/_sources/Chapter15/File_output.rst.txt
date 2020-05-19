File output
-----------

Sending output to a file is similar. For example, we could modify the
previous program to copy lines from one file to another.


.. activecode:: fifteen_two_three
  :language: cpp

    #include <iostream>
    using namespace std;

    int main ()
    {
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
     }

.. parsonsprob:: question_15.3

   Create a code block that sends output to a file. First, make sure that both the input file and the output file are able to be opened.
   -----
   int main () {
   =====
    ifstream in_file ("input_file_name");
    ofstream out_file ("input_file_name");
   =====
    if (in_file.good() == false || out_file.good() == false) {
   =====
      cout << "Unable to open one of the files." << endl;
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
      outfile << line << endl;
    }
    }


.. mchoice:: test_question_fifteen_four
   :practice: T
   :answer_a: Create two "for" loops instead of an if-statement so that the statement loops through both conditions once.
   :answer_b: Create a "while" loop instead of an if-statement so that the statement loops through both conditions separately until the body of the loop is reached.
   :answer_c: Create two "if" statements, one that check whether in_file.good() is false, and another that checks whether out_file.good() is false, instead of putting them together in one "if" statement.
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct!


   The above code snippet seen in the question only checks whether the files open or not, but doesn't specify which one doesn't open. How could you specify which file does not open?

.. fillintheblank:: fill_15.4

    Finish the statement: _________ outfile ("output-file");

    - :(?:o|O)(?:f|f)(?:s|S)(?:t|T)(?:r|R)(?:e|E)(?:A|a)(?:m|M): Correct!
      :.*: Try again!
