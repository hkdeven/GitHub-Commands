# Kill Your Server

Or whatever else you have running.  I'm constantly having this issue with React applications.  Luckily there commands are easy:

```
git config --get remote.origin.url
```

Hold tight, this could take sometime depending on what you have running.
When completed, you should see something like this:

```
Adobe\x20  421 deven   13u  IPv4 0x9738127491d67b7b      0t0  TCP localhost:15292 (LISTEN)
node       439 deven   15u  IPv4 0x9738127491c7dd6b      0t0  TCP localhost:50000 (LISTEN)
node      2108 deven   16u  IPv6 0x973812748bcbab6b      0t0  TCP *:3000 (LISTEN)
```

Take the numeric ID from the second column of the event you wish to terminate and inject it into the command prompt below.  For our scenario we want to kill the first node server that is running on localhost:50000.

```
kill -9 439
```

We can verify that the process has been terminated by running the first command above.

Enjoy.
