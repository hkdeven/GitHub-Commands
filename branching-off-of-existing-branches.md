# Branching from Existing Branches

At some point we will all do work on a feature that is in development.  The safest, cleanest workflow is obviously to create a branch from the current `development` branch.  This way, if or when you screw something up, no one in your team need be aware or affected by it.  And when everything is ready with your particular feature, you can simple merge into the `development` branch.

The process is very simple, but it's important to be particular.

First, create your branch off of the `development` branch:

```
$ git checkout -b myFeature development
```

When committing work:

```
$ git add .
$ git commit -am "Your commit message :smiley:"
$ git push origin myFeature
```

And finally, when ready to merge your feature into the `development` branch without fast forwarding:

```
$ git checkout development
$ git merge --no-ff myFeature
```

And there you have it.  :v:

For more about branching on branches, checkout [nvie.com/posts/a-successful-git-branching-model.][1]

[1]: http://nvie.com/posts/a-successful-git-branching-model/
