Glossary
--------

encode:
   To represent one set of values using another set of values, by
   constructing a mapping between them.

abstract parameter:
   A set of parameters that act together as a single parameter.

.. [1]
   ``apvector``\ \ s are a little different from ``apstring``\ \ s in
   this regard. The file ``apvector.cpp`` contains a template that
   allows the compiler to create vectors of various kinds. The first
   time you use a vector of integers, the compiler generates code to
   support that kind of vector. If you use a vector of
   ``apstring``\ \ s, the compiler generates different code to handle
   that kind of vector. As a result, it is usually sufficient to include
   the header file ``apvector.h``; you do not have to compile
   ``apvector.cpp`` at all! Unfortunately, if you do, you are likely to
   get a long stream of error messages. I hope this footnote helps you
   avoid an unpleasant surprise, but the details in your development
   environment may differ.
