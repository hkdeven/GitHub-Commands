# Merging NTK

To merge another branch into your own you'll need to add the other branch as a remote:

```
git remote add otherrep uriToOtherRep
```

Fetch changes from that other branch:

```
git fetch otherrep
```

And then merge the branch from the remote repository into your current branch:

```
git merge otherrep/branchname
```

And you're done.  :white_check_mark:    
