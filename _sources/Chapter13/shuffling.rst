Shuffling
---------

For most card games you need to be able to shuffle the deck; that is,
put the cards in a random order. In Section `[random] <#random>`__ we
saw how to generate random numbers, but it is not obvious how to use
them to shuffle a deck.

One possibility is to model the way humans shuffle, which is usually by
dividing the deck in two and then reassembling the deck by choosing
alternately from each deck. Since humans usually don’t shuffle
perfectly, after about 7 iterations the order of the deck is pretty well
randomized. But a computer program would have the annoying property of
doing a perfect shuffle every time, which is not really very random. In
fact, after 8 perfect shuffles, you would find the deck back in the same
order you started in. For a discussion of that claim, see
``http://www.wiskit.com/marilyn/craig.html`` or do a web search with the
keywords “perfect shuffle.”

A better shuffling algorithm is to traverse the deck one card at a time,
and at each iteration choose two cards and swap them.

Here is an outline of how this algorithm works. To sketch the program, I
am using a combination of C++ statements and English words that is
sometimes called **pseudocode**:

::

     for (size_t i=0; i<cards.size(); i++) {
       // choose a random number between i and cards.size()
       // swap the ith card and the randomly-chosen card
     }

The nice thing about using pseudocode is that it often makes it clear
what functions you are going to need. In this case, we need something
like ``randomInt``, which chooses a random integer between the
parameters ``low`` and ``high``, and ``swapCards`` which takes two
indices and switches the cards at the indicated positions.

You can probably figure out how to write ``randomInt`` by looking at
Section `[random] <#random>`__, although you will have to be careful
about possibly generating indices that are out of range.

You can also figure out ``swapCards`` yourself. I will leave the
remaining implementation of these functions as an exercise to the
reader.

.. mchoice:: question13_6_1
   :answer_a: cstdlib
   :answer_b: iostream
   :answer_c: strings
   :answer_d: cmath
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Incorrect!
   :feedback_c: Incorrect!
   :feedback_d: Incorrect!

   Which library do we need to include to create random numbers?

.. parsonsprob:: question13_6_2

   Let's write the code for the ``randomInt`` function. ``randomInt`` should take two parameters
   low and high and return a random integer between them, inclusive.
   -----
   int randomInt (int low, int high) {
   =====
   int randomInt () {                         #paired
   =====
      int x = random ();
   =====
      int y = x % (high - low + 1) + low; 
   =====
      int y = x % high;                         #paired
   =====
      return y;
   }
   =====
      return x;                         #paired
   }

.. parsonsprob:: question13_6_3

   Now let's write the code for the ``swapCards`` function. We'll write ``swapCards``
   as a ``Deck`` member function that takes two indices as parameters.
   -----
   void Deck::swapCards (int index1, int index2) {
   =====
   void Card::swapCards (int index1, int index2) {                         #paired
   =====
      Rank r = cards[index1].rank;
      Suit s = cards[index1].suit;
   =====
      Rank r = cards[index1].suit;
      Suit s = cards[index1].rank;                         #paired
   =====
      cards[index1] = cards[index2]; 
   =====
      cards[index2] = cards[index1];                         #paired
   =====
      cards[index2].rank = r;
      cards[index2].suit = s;
   }

Now that we've written both ``randomInt`` and ``swapCards``, we can write the ``Deck`` member function
``shuffle`` which shuffles the deck of cards. Take a look at the active code below. Write  your implementation
of ``shuffle`` in the commented region.

.. activecode:: thirteenfive 
   :language: cpp

   #include <iostream>
   #include <string>
   #include <vector>
   using namespace std;

   enum Suit { CLUBS, DIAMONDS, HEARTS, SPADES };

   enum Rank { ACE=1, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE,
   TEN, JACK, QUEEN, KING };

   int randomInt (int low, int high);

   struct Card {
     Rank rank;
     Suit suit;
     Card ();
     Card (Suit s, Rank r);
     void print () const;
   };

   struct Deck {
     vector<Card> cards;
     Deck ();
     void print () const;
     void swapCards (int index1, int index2);
     void shuffleDeck ();
   };

   void Deck::shuffleDeck () {
      // Follow the pseudocode from above and use ``randomInt`` and 
      // ``swapCards`` to write the ``shuffle`` member function. 
      // If done correctly, a shuffled deck of cards should output.
   }

   int main() {
     Deck deck;
     deck.shuffleDeck ();
     deck.print ();
   }

   ====
   Card::Card () {
     suit = SPADES;  rank = ACE;
   }

   Card::Card (Suit s, Rank r) {
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

   Deck::Deck ()
   {
     vector<Card> temp (52);
     cards = temp;

     int i = 0;
     for (Suit suit = CLUBS; suit <= SPADES; suit = Suit(suit+1)) {
       for (Rank rank = ACE; rank <= KING; rank = Rank(rank+1)) {
         cards[i].suit = suit;
         cards[i].rank = rank;
         i++;
       }
     }
   }

   void Deck::print () const {
     for (size_t i = 0; i < cards.size(); i++) {
       cards[i].print ();
     }
   }

   int randomInt (int low, int high) {
      int x = random ();
      int y = x % (high - low + 1) + low; 
      return y;
   }

   void Deck::swapCards (int index1, int index2) {
      Rank r = cards[index1].rank;
      Suit s = cards[index1].suit;
      cards[index1] = cards[index2]; 
      cards[index2].rank = r;
      cards[index2].suit = s;
   }