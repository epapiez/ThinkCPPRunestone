Our own version of ``find``
---------------------------

If we are looking for a letter in a ``string``, we may not want to
start at the beginning of the string. One way to generalize the ``find``
function is to write a version that takes an additional parameter—the
index where we should start looking. Here is an implementation of this
function.

::

   int find (string s, char c, int i)
   {
     while (i<s.length()) {
       if (s[i] == c) return i;
       i = i + 1;
     }
     return -1;
   }

Instead of invoking this function on an ``string``, like the first
version of ``find``, we have to pass the ``string`` as the first
argument. The other arguments are the character we are looking for and
the index where we should start.

For example, below we are finding the number of 'e' characters in the "Shepard" part of "German Shepard using our function. Then we use the built-in find function to demonstrate how they work differently.

.. activecode:: seventen
  :language: cpp
  :caption: Our own find function


    #include <iostream>
    using namespace std;

    int find (string s, char c, int i)
    {
      int length = s.length();
      while (i < length) {
        if (s[i] == c) {
            return i;
          }
          i = i + 1;
        }
        return -1;
    }

    int main() {
      string dog = "German Shepard";
      int start_shepard = 7;
      cout << find(dog, 'e', start_shepard) << endl;
      cout << dog.find('e') << endl;
    }
