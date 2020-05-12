Shuffling and dealing
---------------------

In Section `1.6 <#shuffle>`__ I wrote pseudocode for a shuffling
algorithm. Assuming that we have a function called ``shuffleDeck`` that
takes a deck as an argument and shuffles it, we can create and shuffle a
deck:

::

     Deck deck;               // create a standard 52-card deck
     deck.shuffle ();         // shuffle it

Then, to deal out several hands, we can use ``subdeck``:

::

     Deck hand1 = deck.subdeck (0, 4);
     Deck hand2 = deck.subdeck (5, 9);
     Deck pack = deck.subdeck (10, 51);

This code puts the first 5 cards in one hand, the next 5 cards in the
other, and the rest into the pack.

When you thought about dealing, did you think we should give out one
card at a time to each player in the round-robin style that is common in
real card games? I thought about it, but then realized that it is
unnecessary for a computer program. The round-robin convention is
intended to mitigate imperfect shuffling and make it more difficult for
the dealer to cheat. Neither of these is an issue for a computer.

This example is a useful reminder of one of the dangers of engineering
metaphors: sometimes we impose restrictions on computers that are
unnecessary, or expect capabilities that are lacking, because we
unthinkingly extend a metaphor past its breaking point. Beware of
misleading analogies.