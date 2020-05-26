Sorting
-------

Now that we have messed up the deck, we need a way to put it back in
order. Ironically, there is an algorithm for sorting that is very
similar to the algorithm for shuffling.

Again, we are going to traverse the deck and at each location choose
another card and swap. The only difference is that this time instead of
choosing the other card at random, we are going to find the lowest card
remaining in the deck.

By “remaining in the deck,” I mean cards that are at or to the right of
the index ``i``.

::

     for (size_t i=0; i<cards.size(); i++) {
       // find the lowest card at or to the right of i
       // swap the ith card and the lowest card
     }

Again, the pseudocode helps with the design of the **helper functions**.
In this case we can use ``swapCards`` again, so we only need one new
one, called ``findLowestCard``, that takes an index where it should start 
looking in the vector of cards.

This process, using pseudocode to figure out what helper functions are
needed, is sometimes called **top-down design**, in contrast to the
bottom-up design I discussed in Section `[counting] <#counting>`__.

Once again, I am going to leave the implementation up to the reader.

.. activecode:: thirteenseven 
   :language: cpp

   Try writing the ``findLowestCard`` function in the commented section
   of the active code below. Once you're done with ``findLowestCard``,
   try using it along with ``swapCards`` to implement the ``Deck`` member 
   function ``sortDeck``. If done correctly, the program should output a 
   sorted deck of cards. If you get stuck, you can reveal the extra problems 
   at the end for help. 
   ~~~~
   #include <iostream>
   #include <string>
   #include <vector>
   #include <cstdlib>
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
     bool isGreater (const Card& c2) const;
   };

   struct Deck {
     vector<Card> cards;
     Deck ();
     void print () const;
     void swapCards (int index1, int index2);
     int findLowestCard (int index);
     void shuffleDeck ();
     void sortDeck ();
   };

   int Deck::findLowestCard (int index) {
     // ``findLowestCard`` should search through the vector of cards  
     // starting at index and return the index of the smallest card.
     // Delete the return 0 and write your implementation here.
     return 0;
   }

   void Deck::sortDeck () {
     // Follow the pseudocode from above and use ``findLowestCard`` and 
     // ``swapCards`` to write the ``sort`` member function. 
     // Write your implementation here.
   }

   int main() {
     Deck deck;
     deck.shuffleDeck ();
     deck.sortDeck ();
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

   bool Card::isGreater (const Card& c2) const {
      if (suit > c2.suit) return true;
      if (suit < c2.suit) return false;
      if (rank > c2.rank) return true;
      if (rank < c2.rank) return false;
      return false;
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
      srand (time(NULL));
      int x = random ();
      int y = x % (high - low + 1) + low; 
      return y;
   }

   void Deck::swapCards (int index1, int index2) {
      Card temp = cards[index1];
      cards[index1] = cards[index2]; 
      cards[index2] = temp;
   }

   void Deck::shuffleDeck () {
     for (size_t i = 0; i < cards.size(); i++) {
       int x = randomInt (i, cards.size() - 1);
       swapCards (i, x);
     }
   }

   
.. reveal:: 13_7_1
   :showtitle: Reveal Problem
   :hidetitle: Hide Problem

   .. parsonsprob:: question13_7_1
      :numbered: left
      :adaptive:
   
      Let's write the code for the ``findLowestCard`` function. ``findLowestCard``
      should take an index as a parameter and return an int.
      -----
      int Deck::findLowestCard (int index) {
      =====
      void Deck::findLowestCard (int index) {                         #paired
      =====
         int min = index;
      =====
         for (size_t i = index; i < cards.size(); ++i) { 
      =====
         for (size_t i = 0; i < cards.size(); ++i) {                         #paired 
      =====
            if (cards[min].isGreater(cards[i])) { 
      =====
            if (cards[i].isGreater(cards[min])) {                         #paired 
      =====
             min = i;
            }
         }
      =====
         return min;
      }
      =====
         return cards[min];                         #paired
      }

.. reveal:: 13_7_2
   :showtitle: Reveal Problem
   :hidetitle: Hide Problem

   .. parsonsprob:: question13_7_2
      :numbered: left
      :adaptive:
   
      Let's write the code for the ``sortDeck`` function. We'll use ``findLowestCard``
      and ``swapCards`` in our implementation of ``sortDeck``.
      -----
      void Deck::sortDeck () {
      =====
      Deck::sortDeck () {                         #paired
      =====
         for (size_t i = 0; i < cards.size(); i++) {
      =====
            int x = findLowestCard (i); 
      =====
            int x = findLowestCard (cards.size());                         #paired 
      =====
            swapCards (i, x);
         }
      }

