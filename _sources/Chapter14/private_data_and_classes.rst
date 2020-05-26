Private data and classes
------------------------

I have used the word “encapsulation” in this book to refer to the
process of wrapping up a sequence of instructions in a function, in
order to separate the function’s interface (how to use it) from its
implementation (how it does what it does).

This kind of encapsulation might be called “functional encapsulation,”
to distinguish it from “data encapsulation,” which is the topic of this
chapter. Data encapsulation is based on the idea that each structure
definition should provide a set of functions that apply to the
structure, and prevent unrestricted access to the internal
representation.

One use of data encapsulation is to hide implementation details from
users or programmers that don’t need to know them.

For example, there are many possible representations for a ``Card``,
including two integers, two strings and two enumerated types. The
programmer who writes the ``Card`` member functions needs to know which
implementation to use, but someone using the ``Card`` structure should
not have to know anything about its internal structure.

As another example, we have been using ``string`` and ``vector``
objects without ever discussing their implementations. There are many
possibilities, but as “clients” of these libraries, we don’t need to
know.

In C++, the most common way to enforce data encapsulation is to prevent
client programs from accessing the instance variables of an object. The
keyword ``private`` is used to protect parts of a structure definition.
For example, we could have written the ``Card`` definition:

::

   struct Card
   {
   private:
     int suit, rank;

   public:
     Card ();
     Card (int s, int r);

     int getRank () const { return rank; }
     int getSuit () const { return suit; }
     void setRank (int r) { rank = r; }
     void setSuit (int s) { suit = s; }
   };

There are two sections of this definition, a private part and a public
part. The functions are public, which means that they can be invoked by
client programs. The instance variables are private, which means that
they can be read and written only by ``Card`` member functions.

It is still possible for client programs to read and write the instance
variables using the **accessor functions** (the ones beginning with
``get`` and ``set``). On the other hand, it is now easy to control which
operations clients can perform on which instance variables. For example,
it might be a good idea to make cards “read only” so that after they are
constructed, they cannot be changed. To do that, all we have to do is
remove the ``set`` functions.

Another advantage of using accessor functions is that we can change the
internal representations of cards without having to change any client
programs.

.. activecode:: fourteenone 
   :language: cpp

   Run the active code below. Uncomment the commented out code to see what happens!
   ~~~~
   #include <iostream>
   #include <string>
   #include <vector>
   using namespace std;

   struct Card {
     private:
       int suit, rank;
     public:
       Card ();
       Card (int s, int r);
       int getRank () const { return rank; }
       int getSuit () const { return suit; }
       void setRank (int r) { rank = r; }
       void setSuit (int s) { suit = s; }
       void print () const;
   };

   int main() {
     Card card (3, 8);
     card.print();
     cout << "Rank: " << card.getRank() << "    Suit: " << card.getSuit() << endl;
     card.setRank(12);
     card.setSuit(2);
     card.print();
     cout << "Rank: " << card.getRank() << "    Suit: " << card.getSuit() << endl;
     
     // If you uncomment the following code, you'll get an error! We cannot directly  
     // access the private data members of Card, which is why we use accessor functions.
     
     /* 
     cout << "Rank: " << card.rank << "\t Suit: " << card.suit << endl;
     card.rank = 4;
     card.suit = 0; 
     */
   }
   ====
   Card::Card () {
     suit = 3;  rank = 0;
   }

   Card::Card (int s, int r) {
     suit = s;  rank = r;
   }

   void Card::print () const {
     vector<string> suits (4);
     suits[0] = "Clubs";
     suits[1] = "Diamonds";
     suits[2] = "Hearts";
     suits[3] = "Spades";

     vector<string> ranks (14);
     ranks[1] = "Ace";
     ranks[2] = "2";
     ranks[3] = "3";
     ranks[4] = "4";
     ranks[5] = "5";
     ranks[6] = "6";
     ranks[7] = "7";
     ranks[8] = "8";
     ranks[9] = "9";
     ranks[10] = "10";
     ranks[11] = "Jack";
     ranks[12] = "Queen";
     ranks[13] = "King";

      cout << ranks[rank] << " of " << suits[suit] << endl;
   }

.. mchoice:: question14_1_1
   :answer_a: True
   :answer_b: False
   :correct: a
   :feedback_a: Incorrect! Data encapsulation should hide implementation details.
   :feedback_b: Correct! Data encapsulation prevents unrestricted access to internal representations.

   Data encapsulation is based on the idea that each structure definition should provide a set of functions that 
   apply to the structure, and allow unrestricted access to the internal representation.

.. fillintheblank:: question14_1_2

    What type of data member cannot be directly accessed outside of the structure?

    - :(Pp)rivate||((Pp)rivate (Dd)ata (Mm)ember): Correct!
      :.*: Incorrect! Try again.

.. mchoice:: question14_1_3
   :multiple_answers:
   :answer_a: getSuit
   :answer_b: setRank
   :answer_c: print
   :answer_d: getRank
   :correct: a,b,d
   :feedback_a: Correct!
   :feedback_b: Correct! "Setter" functions are also known as "mutator" functions.
   :feedback_c: Incorrect!
   :feedback_d: Correct!

   Which of the following are examples of accessor functions?