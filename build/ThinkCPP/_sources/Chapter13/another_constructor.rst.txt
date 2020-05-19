Another constructor
-------------------

Now that we have a ``Deck`` object, it would be useful to initialize the
cards in it. From the previous chapter we have a function called
``buildDeck`` that we could use (with a few adaptations), but it might
be more natural to write a second ``Deck`` constructor.

::

   Deck::Deck ()
   {
     apvector<Card> temp (52);
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

Notice how similar this function is to ``buildDeck``, except that we had
to change the syntax to make it a constructor. Now we can create a
standard 52-card deck with the simple declaration ``Deck deck;``

The active code below prints out the cards in a deck using the loop from the previous section.

.. activecode:: thirteenthree 
   :language: cpp

   #include <iostream>
   #include <string>
   #include <vector>
   using namespace std;

   enum Suit { CLUBS, DIAMONDS, HEARTS, SPADES };

   enum Rank { ACE=1, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE,
   TEN, JACK, QUEEN, KING };

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
   };

   int main() {
     Deck deck;
     for (int i = 0; i<52; i++) {
       deck.cards[i].print();
     }
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

.. mchoice:: question13_4_1
   :answer_a: True
   :answer_b: False
   :correct: a
   :feedback_a: Correct! The for loops in the Deck constructor initialize each card to its proper value.
   :feedback_b: Incorrect! Are the cards printed out correctly?

   Based on your observations from the active code above, the cards in ``deck`` are initialized to the correct
   suits and ranks of a standard deck of 52 cards.
