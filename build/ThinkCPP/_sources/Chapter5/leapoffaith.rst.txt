Leap of faith
-------------

Following the flow of execution is one way to read programs, but as you
saw in the previous section, it can quickly become labarynthine. An
alternative is what I call the “leap of faith.” When you come to a
function call, instead of following the flow of execution, you *assume*
that the function works correctly and returns the appropriate value.

In fact, you are already practicing this leap of faith when you use
built-in functions. When you call ''cos'' or ''exp'', you don’t examine the
implementations of those functions. You just assume that they work,
because the people who wrote the built-in libraries were good
programmers.

Well, the same is true when you call one of your own functions. For
example, in Section \ `8 <#bool>`__ we wrote a function called
''isSingleDigit'' that determines whether a number is between 0 and 9. Once
we have convinced ourselves that this function is correct—by testing and
examination of the code—we can use the function without ever looking at
the code again.

The same is true of recursive programs. When you get to the recursive
call, instead of following the flow of execution, you should *assume*
that the recursive call works (yields the correct result), and then ask
yourself, “Assuming that I can find the factorial of :math:`n-1`, can I
compute the factorial of :math:`n`?” In this case, it is clear that you
can, by multiplying by :math:`n`.

Of course, it is a bit strange to assume that the function works
correctly when you have not even finished writing it, but that’s why
it’s called a leap of faith!
