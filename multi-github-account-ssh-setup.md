Inevitably you will find yourself in need of accessing multiple GitHub accounts, like when you start working for a [kickass company](https://github.com/Allied-Steel-Buildings) as I did.  The thought occurred to me, why not automate this process with a simple alias that can be run from the command line so that we need not ever have to re-research and read through dry and often overly opinionated user-generated walk-throughs.


# One line command
Here is the final line of code we will ultimately be running to accomplish this goal.
Note that you will need to replace my username with your own (obs).

```
git goattachnewgithub
```

Beautiful, isn't it?

# Let's get started
Switching between accounts require two things:

1. Changeing the `ssh` key,
2. And changeing the git `user.email` setting.

## Generate ssh keys

First things first, you'll need to generate as many keys as the number of accounts you have. Just specify a different email and name for every key:
