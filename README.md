# git-demo
A small repo used for git demos

## Commits

![git stage flow](http://www.nullptr.me/images/git-lifecycle.png)

### Atomic Commits
It's important to keep your commits small and focused, with brief but meaningful commit messages. Doing this will make your coworkers and your life way easier. We have a [commit message guideline]() in our wiki. Main points are:

- Try to keep them clean. One commit - one feature.
- All tests should pass before making a commit.
- Ideally it should be possible to cleanly revert or cherry-pick individual commits.
- Commit messages should be written in the "imperative mood" (i.e. "Add a timers widget", not "Adding a timers widget" or "Added a timers widget")
- Make your commit messages useful

Following this guideline will make it easy to know what a single commit does without having to actually dive into code. Another important piece is that the commits should be atomic enough that it should be possible to cleanly cherry-pick or revert individual commits without side effects. 

### Staging Changes
There are several different ways to stage changes for a commit, and I am only going to *briefly* cover a few. Since our goal is to try and make our commits atomic, I think it is important to try and be specific when staging changes for a commit. Doing this often lends the question, "Does this piece really belong in this commit". You'll probably find that the best approach will be to use a combination of the following strategies depending on what your goal is.

#### Adding Changes by File
Often you'll want to commit all changes within a file, or maybe even add a file that is not already being tracked by git. One of the easiest ways to do this is `git add <filename>`

An alternative way is to use the interactive mode:
```bash
twendlan@Tylers-MBP-2 git-demo (commit-story) $ git add -i
           staged     unstaged path
  1:    unchanged        +6/-2 README.md

*** Commands ***
  1: status       2: update       3: revert       4: add untracked
  5: patch        6: diff         7: quit         8: help
What now> a
  1: commits.txt
  2: notcommits.txt
Add untracked>> 1
* 1: commits.txt
  2: notcommits.txt
Add untracked>> 
added one path

*** Commands ***
  1: status       2: update       3: revert       4: add untracked
  5: patch        6: diff         7: quit         8: help
What now> q
Bye.
```

#### Adding Changes by Hunk
Sometimes only certain changes within a file are important to a commit. One of the options at your disposal is to add changes by hunk (also known as `patch`). This can be done using `git add -p` which opens a similarly interactive cli. You can display the options by typing `?`

```bash
twendlan@Tylers-MBP-2 git-demo (commit-story) $ git add -p
diff --git a/README.md b/README.md
index 58af1aa..2a5590e 100644
--- a/README.md
+++ b/README.md
@@ -1,5 +1,9 @@
 # git-demo
 A small repo used for git demos
 
-## Sections
-- Commits
+## Commits
+### Atomic Commits
+### Adding changes by file
+### Adding changes by hunk
+### Adding changes by line
+
Stage this hunk [y,n,q,a,d,/,e,?]? ?
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
```

Patching can also be accessed via the interactive menu, shown above. An important thing to note is that you can only patch tracked files (at least to my knowledge).

#### Adding Changes by Line
Sometimes you need to get even more specific when staging changes. If you were to have made changes to a file but in one big hunk that can't easily be split by gits patch option, you could use the `-e` flag to go into `--edit` mode where you can select what to include line by line.
 
*Notes from git-scm docs*
> ## added content
> Added content is represented by lines beginning with "+". You can prevent staging any addition lines by deleting them.
> 
> ## removed content
> Removed content is represented by lines beginning with "-". You can prevent staging their removal by converting the "-" to a " " (space).
> 
> ## modified content
> Modified content is represented by "-" lines (removing the old content) followed by "+" lines (adding the replacement content). You can prevent staging the modification by converting "-" lines to " ", and removing "+" lines. Beware that modifying only half of the pair is likely to introduce confusing changes to the index.
 
