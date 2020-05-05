Decks and subdecks
------------------

Looking at the interface to ``findBisect``

::

   int findBisect (const Card& card, const apvector<Card>& deck,
           int low, int high) {

it might make sense to treat three of the parameters, ``deck``, ``low``
and ``high``, as a single parameter that specifies a **subdeck**.

This kind of thing is quite common, and I sometimes think of it as an
**abstract parameter**. What I mean by “abstract,” is something that is
not literally part of the program text, but which describes the function
of the program at a higher level.

For example, when you call a function and pass a vector and the bounds
``low`` and ``high``, there is nothing that prevents the called function
from accessing parts of the vector that are out of bounds. So you are
not literally sending a subset of the deck; you are really sending the
whole deck. But as long as the recipient plays by the rules, it makes
sense to think of it, abstractly, as a subdeck.

There is one other example of this kind of abstraction that you might
have noticed in Section `[objectops] <#objectops>`__, when I referred to
an “empty” data structure. The reason I put “empty” in quotation marks
was to suggest that it is not literally accurate. All variables have
values all the time. When you create them, they are given default
values. So there is no such thing as an empty object.

But if the program guarantees that the current value of a variable is
never read before it is written, then the current value is irrelevant.
Abstractly, it makes sense to think of such a variable as “empty.”

This kind of thinking, in which a program comes to take on meaning
beyond what is literally encoded, is a very important part of thinking
like a computer scientist. Sometimes, the word “abstract” gets used so
often and in so many contexts that it is hard to interpret.
Nevertheless, abstraction is a central idea in computer science (as well
as many other fields).

A more general definition of “abstraction” is “The process of modeling a
complex system with a simplified description in order to suppress
unnecessary details while capturing relevant behavior.”