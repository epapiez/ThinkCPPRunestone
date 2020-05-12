The ``Set`` data structure
--------------------------

A data structure is a container for grouping a collection of data into a
single object. We have seen some examples already, including
``apstring``\ s, which are collections of characters, and
``apvector``\ s which are collections on any type.

An ordered set is a collection of items with two defining properties:

Ordering:
   The elements of the set have indices associated with them. We can use
   these indices to identify elements of the set.

Uniqueness:
   No element appears in the set more than once. If you try to add an
   element to a set, and it already exists, there is no effect.

In addition, our implementation of an ordered set will have the
following property:

Arbitrary size:
   As we add elements to the set, it expands to make room for new
   elements.

Both ``apstring``\ s and ``apvector``\ s have an ordering; every element
has an index we can use to identify it. Both none of the data structures
we have seen so far have the properties of uniqueness or arbitrary size.

To achieve uniqueness, we have to write an ``add`` function that
searches the set to see if it already exists. To make the set expand as
elements are added, we can take advantage of the ``resize`` function on
``apvector``\ s.

Here is the beginning of a class definition for a ``Set``.

::

   class Set {
   private:
     apvector<apstring> elements;
     int numElements;

   public:
     Set (int n);

     int getNumElements () const;
     apstring getElement (int i) const;
     int find (const apstring& s) const;
     int add (const apstring& s);
   };

   Set::Set (int n)
   {
     apvector<apstring> temp (n);
     elements = temp;
     numElements = 0;
   }

The instance variables are an ``apvector`` of strings and an integer
that keeps track of how many elements there are in the set. Keep in mind
that the number of elements in the set, ``numElements``, is not the same
thing as the size of the ``apvector``. Usually it will be smaller.

The ``Set`` constructor takes a single parameter, which is the initial
size of the ``apvector``. The initial number of elements is always zero.

``getNumElements`` and ``getElement`` are accessor functions for the
instance variables, which are private. ``numElements`` is a read-only
variable, so we provide a ``get`` function but not a ``set`` function.

::

   int Set::getNumElements () const
   {
     return numElements;
   }

Why do we have to prevent client programs from changing
``getNumElements``? What are the invariants for this type, and how could
a client program break an invariant. As we look at the rest of the
``Set`` member function, see if you can convince yourself that they all
maintain the invariants.

When we use the ``[]`` operator to access the ``apvector``, it checks to
make sure the index is greater than or equal to zero and less than the
length of the ``apvector``. To access the elements of a set, though, we
need to check a stronger condition. The index has to be less than the
number of elements, which might be smaller than the length of the
``apvector``.

::

   apstring Set::getElement (int i) const
   {
     if (i < numElements) {
       return elements[i];
     } else {
       cout << "Set index out of range." << endl;
       exit (1);
     }
   }

If ``getElement`` gets an index that is out of range, it prints an error
message (not the most useful message, I admit), and exits.

The interesting functions are ``find`` and ``add``. By now, the pattern
for traversing and searching should be old hat:

::

   int Set::find (const apstring& s) const
   {
     for (int i=0; i<numElements; i++) {
       if (elements[i] == s) return i;
     }
     return -1;
   }

So that leaves us with ``add``. Often the return type for something like
``add`` would be void, but in this case it might be useful to make it
return the index of the element.

::

   int Set::add (const apstring& s)
   {
     // if the element is already in the set, return its index
     int index = find (s);
     if (index != -1) return index;

     // if the apvector is full, double its size
     if (numElements == elements.length()) {
       elements.resize (elements.length() * 2);
     }

     // add the new elements and return its index
     index = numElements;
     elements[index] = s;
     numElements++;
     return index;
   }

The tricky thing here is that ``numElements`` is used in two ways. It is
the number of elements in the set, of course, but it is also the index
of the next element to be added.

It takes a minute to convince yourself that that works, but consider
this: when the number of elements is zero, the index of the next element
is 0. When the number of elements is equal to the length of the
``apvector``, that means that the vector is full, and we have to
allocate more space (using ``resize``) before we can add the new
element.

Here is a state diagram showing a ``Set`` object that initially contains
space for 2 elements.

Now we can use the ``Set`` class to keep track of the cities we find in
the file. In ``main`` we create the ``Set`` with an initial size of 2:

::

     Set cities (2);

Then in ``processLine`` we add both cities to the ``Set`` and store the
index that gets returned.

::

     int index1 = cities.add (city1);
     int index2 = cities.add (city2);

I modified ``processLine`` to take the ``cities`` object as a second
parameter.
