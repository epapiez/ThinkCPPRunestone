Stack diagrams for recursive functions
--------------------------------------

In the previous chapter we used a stack diagram to represent the state
of a program during a function call. The same kind of diagram can make
it easier to interpret a recursive function.

Remember that every time a function gets called it creates a new
instance that contains the function’s local variables and parameters.

This figure shows a stack diagram for countdown, called with ``n = 3``:

.. figure:: Images/4.9stackdiagram.png
   :scale: 50%
   :align: center
   :alt: image



There is one instance of main and four instances of countdown, each with
a different value for the parameter ``n``. The bottom of the stack,
countdown with ``n=0`` is the base case. It does not make a recursive call,
so there are no more instances of countdown.

The instance of main is empty because main does not have any parameters
or local variables. As an exercise, draw a stack diagram for nLines,
invoked with the parameter n=4.

::

    shared_birthdays = {}
        shared_birthday_list = []
        for i in self.data_dict['DOB']:
            split_date = monday_and_day.split('/')
            month_and_day = split_date[0] + '/' + split_date[1]
            shared_birthdays[month_and_day] = shared_birthdays.get(month_and_day, 0) + 1

        for i in shared_birthdays[month_and_day]:
            if shared_birthdays.get(month_and_day) > 1:
                shared_birthday_list.append(shared_birthdays[month_and_day], shared_birthdays[i])

        shared_birthdays_list = sorted(shared_birthdays_list.items(), key=lambda x: x[1], reverse=True)
        return shared_birthdays_list
