.. _find:

Searching
---------

The next function I want to write is ``find``, which searches through a
vector of ``Card``\ s to see whether it contains a certain card. It may
not be obvious why this function would be useful, but it gives me a
chance to demonstrate two ways to go searching for things, a ``linear``
search and a ``bisection`` search.

Linear search is the more obvious of the two; it involves traversing the
deck and comparing each card to the one we are looking for. If we find
it we return the index where the card appears. If it is not in the deck,
we return -1.

::

   int find (const Card& card, const apvector<Card>& deck) {
     for (int i = 0; i < deck.length(); i++) {
       if (equals (deck[i], card)) return i;
     }
     return -1;
   }

The loop here is exactly the same as the loop in ``printDeck``. In fact,
when I wrote the program, I copied it, which saved me from having to
write and debug it twice.

Inside the loop, we compare each element of the deck to ``card``. The
function returns as soon as it discovers the card, which means that we
do not have to traverse the entire deck if we find the card we are
looking for. If the loop terminates without finding the card, we know
the card is not in the deck and return ``-1``.

To test this function, I wrote the following:

::

     apvector<Card> deck = buildDeck ();

     int index = card.find (deck[17]);
     cout << "I found the card at index = " << index << endl;

The output of this code is

::

   I found the card at index = 17