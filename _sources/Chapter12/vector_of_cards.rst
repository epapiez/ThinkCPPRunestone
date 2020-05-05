Vectors of cards
----------------

The reason I chose ``Cards`` as the objects for this chapter is that
there is an obvious use for a vector of cards—a deck. Here is some code
that creates a new deck of 52 cards:

::

     apvector<Card> deck (52);

Here is the state diagram for this object:

The three dots represent the 48 cards I didn’t feel like drawing. Keep
in mind that we haven’t initialized the instance variables of the cards
yet. In some environments, they will get initialized to zero, as shown
in the figure, but in others they could contain any possible value.

One way to initialize them would be to pass a ``Card`` as a second
argument to the constructor:

::

     Card aceOfSpades (3, 1);
     apvector<Card> deck (52, aceOfSpades);

This code builds a deck with 52 identical cards, like a special deck for
a magic trick. Of course, it makes more sense to build a deck with 52
different cards in it. To do that we use a nested loop.

The outer loop enumerates the suits, from 0 to 3. For each suit, the
inner loop enumerates the ranks, from 1 to 13. Since the outer loop
iterates 4 times, and the inner loop iterates 13 times, the total number
of times the body is executed is 52 (13 times 4).

::

     int i = 0;
     for (int suit = 0; suit <= 3; suit++) {
       for (int rank = 1; rank <= 13; rank++) {
         deck[i].suit = suit;
         deck[i].rank = rank;
         i++;
       }
     }

I used the variable ``i`` to keep track of where in the deck the next
card should go.

Notice that we can compose the syntax for selecting an element from an
array (the ``[]`` operator) with the syntax for selecting an instance
variable from an object (the dot operator). The expression
``deck[i].suit`` means “the suit of the ith card in the deck”.

As an exercise, encapsulate this deck-building code in a function called
``buildDeck`` that takes no parameters and that returns a
fully-populated vector of ``Card``\ s.