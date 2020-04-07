A more complicated example
--------------------------

Although the process of transforming functions into member functions is
mechanical, there are some oddities. For example, ``after`` operates on
two ``Time`` structures, not just one, and we can’t make both of them
implicit. Instead, we have to invoke the function on one of them and
pass the other as an argument.

Inside the function, we can refer to one of the them implicitly, but to
access the instance variables of the other we continue to use dot
notation.

::

   bool Time::after (const Time& time2) const {
     if (hour > time2.hour) return true;
     if (hour < time2.hour) return false;

     if (minute > time2.minute) return true;
     if (minute < time2.minute) return false;

     if (second > time2.second) return true;
     return false;
   }

To invoke this function:

::

     if (doneTime.after (currentTime)) {
       cout << "The bread will be done after it starts." << endl;
     }

You can almost read the invocation like English: “If the done-time is
after the current-time, then...”
