##An Elephant Never Forgets

But I sure do.  Who can keep track of what remotes are attached to which repos - not me!

That's why I've created a handy alias script that runs this handy code:

```
lsof -Pi | grep LISTEN
```

The result should be the full url of the repo to which your folder is attached, if any.

Enjoy.
