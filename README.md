semaphoric - lightweight counting semaphore concurrency control using flock
===========================================================================

A utility to limit concurrency by running a command only if fewer than some
number of other commands (associated with an arbitrary id) are running.

The id defines the scope of the semaphore.
If id contains a / then it's treated as the directory to store the semaphores.
Otherwise they're stored in /tmp/semaphoric-$USER/.

Features:
- very lightweight (unlike gnu parallels sem utility)
- most callers block cheaply on file lock until ready
- only one process (the next-to-be-run) polls for a semaphore
- first-in-first-out queuing, no starvation or similar risks
- uses filehandle locks (not SysV semaphores) so is robust and stable
- returns the exit status of the command that was run

