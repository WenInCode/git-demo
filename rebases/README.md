## Rebase
> Reapply commits on top of another base tip

That pretty much sums up what rebasing is. Taking your branches commits and putting them after the tip of the target branch. The [git documentation]() on it provides a really great description.

> All changes made by commits in the current branch but that are not in <upstream> are saved to a temporary area...
> The current branch is reset to <upstream>, or <newbase> if the --onto option was supplied...
> The commits that were previously saved into the temporary area are then reapplied to the current branch, one by one, in order...

There are a few things I like about rebasing:

- There are no merge commits
- It's easy to edit and squash commits (really can clean up a branch)
- Once a feature is ready you can squash it into a feature commit

That last one is common in most of the open source that I have seen or taken part in. However, you lose the atomicity of your commits so it is important that the decision to do so is discussed ahead of time.

There are a few important things to remember when rebasing. The most important being that the history is being re-written. I think it's a good practice to *only rebase when you need to*. Just because your branch is out of date with the branch your pointing at doesn't mean you should rebase right away. I suggest only rebasing for the following reasons (flexible):

- You *need* new changes that are on the branch you are pointing at
- You are ready for final qa/testing
- You need to actually change where the base of the branch points to

### Dealing with conflicts
> In case of conflict, git rebase will stop at the first problematic commit and leave conflict markers in the tree. You can use git diff to locate the markers (<<<<<<) and make edits to resolve the conflict. For each file you edit, you need to tell Git that the conflict has been resolved, typically this would be done with
>
> `git add <filename>`
>
> After resolving the conflict manually and updating the index with the desired resolution, you can continue the rebasing process with
>
> `git rebase --continue`
>
> Alternatively, you can undo the git rebase with
>
> `git rebase --abort`
>
> Another option is to bypass the commit that caused the merge failure with
>
> `git rebase --skip`

### Rebasing to get the latest changes
![git rebase](https://dl2.pushbulletusercontent.com/rAzkHPuBJnBALbiiOCvQhVrnPG2KTUsn/git-rebase.PNG)

### Rebasing to fix/squash commits
git-rebase also has a really great `--interactive` (`-i`) mode that lets you do all sorts of tweaks to your commits for the rebase.

```bash
 pick bbb8a39 Class update and SG-1 import                                                        
 f f3c661c SG-1 import of latest version of branch                   

 # Rebase 52e4096..f3c661c onto 52e4096 (2 command(s))                                                          
 #                                                          
 # Commands:                                                          
 # p, pick = use commit                                                         
 # r, reword = use commit, but edit the commit message                                                          
 # e, edit = use commit, but stop for amending                                                          
 # s, squash = use commit, but meld into previous commit                                               
 # f, fixup = like "squash", but discard this commit's log message                                                          
 # x, exec = run command (the rest of the line) using shell                                                      
 # d, drop = remove commit                                                          
 #                                                          
 # These lines can be re-ordered; they are executed from top to bottom.                                                         
 #                                                      
 # If you remove a line here THAT COMMIT WILL BE LOST.                                                          
 #                                                           
 # wever, if you remove everything, the rebase will be aborted.                                                         
 #
 # Note that empty commits are commented out
```
I use this mostly for rewording commits and squashing related commits into one cleaner commit. As mentioned above, this is also often used to squash all the commits into a single feature commit when PRs are approved.

### When the branch you are based off rebases
This works the same as rebasing off the branch you are currently pointed at.
`git rebase <remote>/<branchyourbasingoff>` you can optionally add the branch you want to rebase at the end.
