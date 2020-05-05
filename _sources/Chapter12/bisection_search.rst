Bisection search
----------------

If the cards in the deck are not in order, there is no way to search
that is faster than the linear search. We have to look at every card,
since otherwise there is no way to be certain the card we want is not
there.

But when you look for a word in a dictionary, you don’t search linearly
through every word. The reason is that the words are in alphabetical
order. As a result, you probably use an algorithm that is similar to a
bisection search:

#. Start in the middle somewhere.

#. Choose a word on the page and compare it to the word you are looking
   for.

#. If you found the word you are looking for, stop.

#. If the word you are looking for comes after the word on the page,
   flip to somewhere later in the dictionary and go to step 2.

#. If the word you are looking for comes before the word on the page,
   flip to somewhere earlier in the dictionary and go to step 2.

If you ever get to the point where there are two adjacent words on the
page and your word comes between them, you can conclude that your word
is not in the dictionary. The only alternative is that your word has
been misfiled somewhere, but that contradicts our assumption that the
words are in alphabetical order.

In the case of a deck of cards, if we know that the cards are in order,
we can write a version of ``find`` that is much faster. The best way to
write a bisection search is with a recursive function. That’s because
bisection is naturally recursive.

The trick is to write a function called ``findBisect`` that takes two
indices as parameters, ``low`` and ``high``, indicating the segment of
the vector that should be searched (including both ``low`` and
``high``).

#. To search the vector, choose an index between ``low`` and ``high``,
   and call it ``mid``. Compare the card at ``mid`` to the card you are
   looking for.

#. If you found it, stop.

#. If the card at ``mid`` is higher than your card, search in the range
   from ``low`` to ``mid-1``.

#. If the card at ``mid`` is lower than your card, search in the range
   from ``mid+1`` to ``high``.

Steps 3 and 4 look suspiciously like recursive invocations. Here’s what
this all looks like translated into C++:

::

   int findBisect (const Card& card, const apvector<Card>& deck,
                   int low, int high) {
     int mid = (high + low) / 2;

     // if we found the card, return its index
     if (equals (deck[mid], card)) return mid;

     // otherwise, compare the card to the middle card
     if (deck[mid].isGreater (card)) {
       // search the first half of the deck
       return findBisect (card, deck, low, mid-1);
     } else {
       // search the second half of the deck
       return findBisect (card, deck, mid+1, high);
     }
   }

Although this code contains the kernel of a bisection search, it is
still missing a piece. As it is currently written, if the card is not in
the deck, it will recurse forever. We need a way to detect this
condition and deal with it properly (by returning ``-1``).

The easiest way to tell that your card is not in the deck is if there
are *no* cards in the deck, which is the case if ``high`` is less than
``low``. Well, there are still cards in the deck, of course, but what I
mean is that there are no cards in the segment of the deck indicated by
``low`` and ``high``.

With that line added, the function works correctly:

::

   int findBisect (const Card& card, const apvector<Card>& deck,
                   int low, int high) {

     cout << low << ", " << high << endl;

     if (high < low) return -1;

     int mid = (high + low) / 2;

     if (equals (deck[mid], card)) return mid;

     if (deck[mid].isGreater (card)) {
       return findBisect (card, deck, low, mid-1);
     } else {
       return findBisect (card, deck, mid+1, high);
     }
   }

I added an output statement at the beginning so I could watch the
sequence of recursive calls and convince myself that it would eventually
reach the base case. I tried out the following code:

::

     cout << findBisect (deck, deck[23], 0, 51));

And got the following output:

::

   0, 51
   0, 24
   13, 24
   19, 24
   22, 24
   I found the card at index = 23

Then I made up a card that is not in the deck (the 15 of Diamonds), and
tried to find it. I got the following:

::

   0, 51
   0, 24
   13, 24
   13, 17
   13, 14
   13, 12
   I found the card at index = -1

These tests don’t prove that this program is correct. In fact, no amount
of testing can prove that a program is correct. On the other hand, by
looking at a few cases and examining the code, you might be able to
convince yourself.

The number of recursive calls is fairly small, typically 6 or 7. That
means we only had to call ``equals`` and ``isGreater`` 6 or 7 times,
compared to up to 52 times if we did a linear search. In general,
bisection is much faster than a linear search, especially for large
vectors.

Two common errors in recursive programs are forgetting to include a base
case and writing the recursive call so that the base case is never
reached. Either error will cause an infinite recursion, in which case
C++ will (eventually) generate a run-time error.