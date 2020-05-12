Mergesort
---------

In Section `1.7 <#sorting>`__, we saw a simple sorting algorithm that
turns out not to be very efficient. In order to sort :math:`n` items, it
has to traverse the vector :math:`n` times, and each traversal takes an
amount of time that is proportional to :math:`n`. The total time,
therefore, is proportional to :math:`n^2`.

In this section I will sketch a more efficient algorithm called
**mergesort**. To sort :math:`n` items, mergesort takes time
proportional to :math:`n \log n`. That may not seem impressive, but as
:math:`n` gets big, the difference between :math:`n^2` and
:math:`n \log n` can be enormous. Try out a few values of :math:`n` and
see.

The basic idea behind mergesort is this: if you have two subdecks, each
of which has been sorted, it is easy (and fast) to merge them into a
single, sorted deck. Try this out with a deck of cards:

#. Form two subdecks with about 10 cards each and sort them so that when
   they are face up the lowest cards are on top. Place both decks face
   up in front of you.

#. Compare the top card from each deck and choose the lower one. Flip it
   over and add it to the merged deck.

#. Repeat step two until one of the decks is empty. Then take the
   remaining cards and add them to the merged deck.

The result should be a single sorted deck. Here’s what this looks like
in pseudocode:

::

     Deck merge (const Deck& d1, const Deck& d2) {
       // create a new deck big enough for all the cards
       Deck result (d1.cards.length() + d2.cards.length());

       // use the index i to keep track of where we are in
       // the first deck, and the index j for the second deck
       int i = 0;
       int j = 0;

       // the index k traverses the result deck
       for (int k = 0; k<result.cards.length(); k++) {

         // if d1 is empty, d2 wins; if d2 is empty, d1 wins;
         // otherwise, compare the two cards

         // add the winner to the new deck
       }
       return result;
     }

I chose to make ``merge`` a nonmember function because the two arguments
are symmetric.

The best way to test ``merge`` is to build and shuffle a deck, use
subdeck to form two (small) hands, and then use the sort routine from
the previous chapter to sort the two halves. Then you can pass the two
halves to ``merge`` to see if it works.

If you can get that working, try a simple implementation of
``mergeSort``:

::

   Deck Deck::mergeSort () const {
     // find the midpoint of the deck
     // divide the deck into two subdecks
     // sort the subdecks using sort
     // merge the two halves and return the result
   }

Notice that the current object is declared ``const`` because
``mergeSort`` does not modify it. Instead, it creates and returns a new
``Deck`` object.

If you get that version working, the real fun begins! The magical thing
about mergesort is that it is recursive. At the point where you sort the
subdecks, why should you invoke the old, slow version of ``sort``? Why
not invoke the spiffy new ``mergeSort`` you are in the process of
writing?

Not only is that a good idea, it is *necessary* in order to achieve the
performance advantage I promised. In order to make it work, though, you
have to add a base case so that it doesn’t recurse forever. A simple
base case is a subdeck with 0 or 1 cards. If ``mergesort`` receives such
a small subdeck, it can return it unmodified, since it is already
sorted.

The recursive version of ``mergesort`` should look something like this:

::

   Deck Deck::mergeSort (Deck deck) const {
     // if the deck is 0 or 1 cards, return it

     // find the midpoint of the deck
     // divide the deck into two subdecks
     // sort the subdecks using mergesort
     // merge the two halves and return the result
   }

As usual, there are two ways to think about recursive programs: you can
think through the entire flow of execution, or you can make the “leap of
faith.” I have deliberately constructed this example to encourage you to
make the leap of faith.

When you were using ``sort`` to sort the subdecks, you didn’t feel
compelled to follow the flow of execution, right? You just assumed that
the ``sort`` function would work because you already debugged it. Well,
all you did to make ``mergeSort`` recursive was replace one sort
algorithm with another. There is no reason to read the program
differently.

Well, actually you have to give some thought to getting the base case
right and making sure that you reach it eventually, but other than that,
writing the recursive version should be no problem. Good luck!