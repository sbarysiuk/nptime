Non-Pedantic Time
=================

Python's ``datetime`` module has many uses, but it has a difficulty:
you can't do any arithmetic with ``datetime.time``.  Only with
``datetime.datetime``.  Now, there are good reasons for this:  "What
time will it be, 24 hours from now" has a lot of corner cases,
including daylight savings time, leap seconds, historical timezone
changes, leap years, and so on. But sometimes you really *do* need the
simple case.  Sometimes the perfect is the enemy of the good.  And
that's why you have this module.  This module will allow you to
coccoon yourself in the comforting illusion that, in 24 hours, it will
be the same time as it is right now.

And what freedom this illusion gives you!  You can add a
``datetime.timedelta`` object to an ``nptime`` object, and it works!
It will cycle around 24 hours, like modular arithmetic.  You can ask
"what time comes 1 day and 36 minutes after 12:24 pm?" and it will let
you know: 1:00 pm. How lovely!

>>> from nptime import nptime
>>> from datetime import timedelta
>>> afternoon = nptime(12, 24) + timedelta(days=1, minutes=36)
>>> afternoon
nptime(13, 0)
>>> str(afternoon)
'13:00:00'

You can also ask "How long is it between 9:00 AM and 5:00 PM?  It sure
feels like a million years!"

>>> workday = nptime(hour=17) - nptime(hour=9)
>>> workday
datetime.timedelta(0, 28800)
>>> print workday
8:00:00

Nope, only 8 hours, how strange.  Anyway, please use this module.  It
will be convenient.  But don't use it when talking about concrete
time, time in a particular place, or anything like that.  In fact, it
doesn't even notice tzinfo objects right now.  Good luck.
