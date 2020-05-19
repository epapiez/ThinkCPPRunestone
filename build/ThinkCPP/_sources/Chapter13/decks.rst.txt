Decks
-----

In the previous chapter, we worked with a vector of objects, but I also
mentioned that it is possible to have an object that contains a vector
as an instance variable. In this chapter I am going to create a new
object, called a ``Deck``, that contains a vector of ``Card``\ s.

The structure definition looks like this

::

   struct Deck {
     apvector<Card> cards;

     Deck (int n);
   };

   Deck::Deck (int size)
   {
     apvector<Card> temp (size);
     cards = temp;
   }

The name of the instance variable is ``cards`` to help distinguish the
``Deck`` object from the vector of ``Card``\ s that it contains.

For now there is only one constructor. It creates a local variable named
``temp``, which it initializes by invoking the constructor for the
``apvector`` class, passing the size as a parameter. Then it copies the
vector from ``temp`` into the instance variable ``cards``.

Now we can create a deck of cards like this:

::

     Deck deck (52);

Here is a state diagram showing what a ``Deck`` object looks like:

.. figure:: Images/13.3stackdiagram.png
   :scale: 35%
   :align: center
   :alt: image

The object named ``deck`` has a single instance variable named
``cards``, which is a vector of ``Card`` objects. To access the cards in
a deck we have to compose the syntax for accessing an instance variable
and the syntax for selecting an element from an array. For example, the
expression ``deck.cards[i]`` is the ith card in the deck, and
``deck.cards[i].suit`` is its suit. The following loop

::

     for (int i = 0; i<52; i++) {
       deck.cards[i].print();
     }

demonstrates how to traverse the deck and output each card.

.. fillintheblank:: question13_3_1

    How many cards are in ``deck`` if we make a Deck object like this: ``Deck deck (48)``?

    - :48: Correct!
      :.*: Incorrect! Try again.

.. mchoice:: question13_3_2
   :answer_a: True
   :answer_b: False
   :correct: b
   :feedback_a: Incorrect! Look at the values of ``suit`` and ``rank`` in the state diagram for each card.
   :feedback_b: Correct! We'll see how to initialize each card in a deck in the next section.

   Take a look at the state diagram above. When we create a deck of cards using ``Deck deck (52)``, 
   the cards will be initialized to the correct suits and ranks of a standard deck of 52 cards. 