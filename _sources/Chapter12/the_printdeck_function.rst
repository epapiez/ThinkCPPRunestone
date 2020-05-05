.. _printdeck:

The ``printDeck`` function
--------------------------

Whenever you are working with vectors, it is convenient to have a
function that prints the contents of the vector. We have seen the
pattern for traversing a vector several times, so the following function
should be familiar:

::

   void printDeck (const apvector<Card>& deck) {
     for (int i = 0; i < deck.length(); i++) {
       deck[i].print ();
     }
   }

By now it should come as no surprise that we can compose the syntax for
vector access with the syntax for invoking a function.

Since ``deck`` has type ``apvector<Card>``, an element of ``deck`` has
type ``Card``. Therefore, it is legal to invoke ``print`` on
``deck[i]``.