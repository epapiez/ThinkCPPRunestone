Programs with multiple functions
--------------------------------

When you look at a class definition that contains several functions, it
is tempting to read it from top to bottom, but that is likely to be
confusing, because that is not the **order of execution** of the
program.

Execution always begins at the first statement of main, regardless of
where it is in the program (often it is at the bottom). Statements are
executed one at a time, in order, until you reach a function call.
Function calls are like a detour in the flow of execution. Instead of
going to the next statement, you go to the first line of the called
function, execute all the statements there, and then come back and pick
up again where you left off.

That sounds simple enough, except that you have to remember that one
function can call another. Thus, while we are in the middle of main, we
might have to go off and execute the statements in threeLine. But while
we are executing threeLine, we get interrupted three times to go off and
execute newLine.

Fortunately, C++ is adept at keeping track of where it is, so each time
newLine completes, the program picks up where it left off in threeLine,
and eventually gets back to main so the program can terminate.

What’s the moral of this sordid tale? When you read a program, don’t
read from top to bottom. Instead, follow the flow of execution.
