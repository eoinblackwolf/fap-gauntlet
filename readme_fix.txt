tl;dr just run exe/fg.exe or py/fg.py, right click, download manager.
readme_original.txt contains the original readme of the program.

The function (ChanThread.get_bump_time) that gets the time information from a thread's 
last post's time string (e.g. "09/13/11(Tue)23:51") to sort the threads in correct bump order was bugged.

Firstly, the python's time.strptime failed to fetch the weekday abbreviation (e.g. "Tue") for users with 
non-US time formats. I used a regex to remove the weekday abbreviation and fetched the info without it, 
since it wasn't really needed after all.

Secondly, threads with no posts caused the time string to be empty, and thus caused the
function to throw an exception. I fixed this by returning a date in 1970 (the unix epoch), which
effectively sends these threads to the very bottom. This is not a perfect strategy, but suffices as a 
heurestic.
One can edit line 14 of fg. py (BUMPTIME_EMPTY_VAL = time.gmtime(0)) for a different value. 
Namely, time.gmtime() returns the currect time and sends threads to the front instead.

This fix is not made by the original author of Fap Gauntlet. I just saw a challenge and decided to act
on it, perhaps helping the fellow NEET. I'm not a good programmer, someone with more talent could 
easily better my fixes (and in far less time it took for me).

- Anon