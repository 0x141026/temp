git checkout

EXAMPLES

​    \1. The following sequence checks out the master branch, reverts the .....

​      Makefile to two revisions back, deletes hello.c by mistake, and

​      gets it back from the index.



​        $ git checkout master       (1)

​        $ git checkout master~2 Makefile (2)

​        $ rm -f hello.c

​        $ git checkout hello.c      (3)





​      \1. switch branch

​      \2. take a file out of another commit

​      \3. restore hello.c from the index



​      If you want to check out all C source files out of the index, you

​      can say



​        $ git checkout -- '*.c'



​      Note the quotes around *.c. The file hello.c will also be checked

​      out, even though it is no longer in the working tree, because the

​      file globbing is used to match entries in the index (not in the

​      working tree by the shell).



​      If you have an unfortunate branch that is named hello.c, this step

​      would be confused as an instruction to switch to that branch. You

​      should instead write:

​		$ git checkout -- hello.c



​    \2. After working in the wrong branch, switching to the correct branch

​      would be done using:



​        $ git checkout mytopic



​      However, your "wrong" branch and correct mytopic branch may differ

​      in files that you have modified locally, in which case the above

​      checkout would fail like this:



​        $ git checkout mytopic

​        error: You have local changes to 'frotz'; not switching branches.



​      You can give the -m flag to the command, which would try a

​      three-way merge:



​        $ git checkout -m mytopic

​        Auto-merging frotz



​      After this three-way merge, the local modifications are not

​      registered in your index file, so git diff would show you what

​      changes you made since the tip of the new branch.



​    \3. When a merge conflict happens during switching branches with the -m

​      option, you would see something like this:



​        $ git checkout -m mytopic

​        Auto-merging frotz

​        ERROR: Merge conflict in frotz

​        fatal: merge program failed



At this point, git diff shows the changes cleanly merged as in the

​      previous example, as well as the changes in the conflicted files.

​      Edit and resolve the conflict and mark it resolved with git add as

​      usual:



​        $ edit frotz

​        $ git add frotz

---

git diff 

EXAMPLES

​    Various ways to check your working tree



​        $ git diff      (1)

​        $ git diff --cached  (2)

​        $ git diff HEAD    (3)



​      \1. Changes in the working tree not yet staged for the next commit.

​      \2. Changes between the index and your last commit; what you would

​      be committing if you run git commit without -a option.

​      \3. Changes in the working tree since your last commit; what you

​      would be committing if you run git commit -a



​    Comparing with arbitrary commits



​        $ git diff test      (1)

​        $ git diff HEAD -- ./test (2)

​        $ git diff HEAD^ HEAD   (3)



​      \1. Instead of using the tip of the current branch, compare with the

​      tip of "test" branch.

​      \2. Instead of comparing with the tip of "test" branch, compare with

​      the tip of the current branch, but limit the comparison to the file

​      "test".

​      \3. Compare the version before the last commit and the last commit.



​    Comparing branches



​        $ git diff topic master  (1)

​        $ git diff topic..master  (2)

​        $ git diff topic...master (3)



​      \1. Changes between the tips of the topic and the master branches.

​      \2. Same as above.

​      \3. Changes that occurred on the master branch since when the topic

​      branch was started off it.

Limiting the diff output



​        $ git diff --diff-filter=MRC      (1)

​        $ git diff --name-status        (2)

​        $ git diff arch/i386 include/asm-i386  (3)



​      \1. Show only modification, rename, and copy, but not addition or

​      deletion.

​      \2. Show only names and the nature of change, but not actual diff

​      output.

​      \3. Limit diff output to named subtrees.



​    Munging the diff output



​        $ git diff --find-copies-harder -B -C (1)

​        $ git diff -R             (2)



​      \1. Spend extra cycles to find renames, copies and complete rewrites

​      (very expensive).

​      \2. Output diff in reverse.
