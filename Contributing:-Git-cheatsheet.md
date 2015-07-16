There is a bunch of typical scenarios when you prepare your changes for the
review. We tried to put these together among with commands necessary to make
things done. Most of them are about *editing* the history by `git rebase` and
its derivatives.

It is always assumed that you're currently **on your branch**:

    git checkout my-branch

Also, some operations expect the working directory to be clean. You may
consider running `git stash` before and `git stash pop` after such ones.

### Linearize the branch and catch-up recent changes from the upstream

`git rebase` is designed to "replay" a set of commits on top of a new "base"
commit.

The following command replays your branch on top of `master`. As a bonus,
it removes merge commits, if any.

Affects the whole branch, including already published changes, if any:

    git rebase upstream/master

However, this command puts the branch on top of `upstream/master` of your
local clone, it won't check remotes for new commits. To catch-up these too,
you also need to fetch them too:

    git fetch upstream
    git rebase upstream/master

### Fix whitespace errors

On your local commits only:

    git rebase --whitespace=fix

  - This only works if the branch is tracking its remote counterpart

On the whole branch, including already published changes, if any:

    git rebase --whitespace=fix upstream/master

  - Also use for newly created local branches without remote tracking
    information

### Undo the last commit

This is what `git reset` for.

Bring you back to the exact state just before you've done `git commit`:

    git reset --soft HEAD^

  - This preserves the current working copy, as well as the stage

The same as the above, but also resets the stage, i.e. you'll need to `git add`
from the beginning:

    git reset HEAD^

However, it is often an overkill to use `git reset`. There are more convenient
commands in case you just want to edit a commit instead of throwing it away
completely.

### Amend the last commit

It sometimes happens, that you just miss something in your last commit: forgot
to add a line to some file, made a typo, need to "fix a bugfix", etc.

Often, there's no need to `reset` the whole commit and to redo it from scratch.

`git commit` has a handy `--amend` option for that that instead of creating a
new "oops" commit, add the changes to the last one pointed by `HEAD`:

    git commit --amend

  - This can also be used to fix the commit log message

### Amend a commit buried in the history

There are two options for doing that.

#### Option A: `edit` rebase and `commit --amend`

Since `git commit --amend` allows one to only edit *the last* commit, to amend
an arbitrary commit you "rewind" the history, stop at the commit you wish to
edit, amend it, and "resume".

This is basically what `git rebase --interactive` for:

    git rebase --interactive

Or, to include already published changes:

    git rebase --interactive upstream/master

This opens an editor with a "todo" list of yet unpublished commits. Find the
commit you wish to edit and change *`pick`* in front of it to *`edit`*. Save
and close the editor. You will be advised what to do next.

You can amend the commit now, with:

    git commit --amend

Once you are satisfied with your changes, run:

    git rebase --continue

In case you just want to edit the commit log message, there's more "light"
option for that: instead of *`edit`* use *`reword`*

#### Option B: `commit --fixup` followed by `rebase --autosquash`

If you don't want to interrupt your workflow to rebase, there's yet another
option.

Once you realize that some previous commit need amendment, you create a
so-called "fixup" commit with:

```sh
git commit --fixup "SHA"
```

Which basically only creates a commit with a special message starting with
*`fixup!`* followed by a subject of the target commit:

    fixup! A subject of the commit to fix

That is, you just create a *temporary* "oops" commit. But instead of naming it
like *`(oops) Forgot to add a foo.h file`* you write *`fixup! net: Add foo
driver`*. You may create multiple such commits and then run interactive
rebasing with an `--autosquash` flag:

    git rebase --interactive --autosquash

This will prepare a "todo" list with your fixup commits put where appropriate
and the action set to *`fixup`*. Just review the list, save and close the
editor.

Note: this may sometimes result in conflicts since a fixup commit is created on
top of a snapshot that may diverge from the target commit too much.

### Squash commits into a single one

If it happen that you made some "oops" or fixup commits, you may be asked to
combine them into a single atomic commit. To achieve this, use interactive
rebasing as described above:

    git rebase --interactive

And, to include already published changes:

    git rebase --interactive upstream/master

In the "todo" list put *`squash`* in front of commits that need to be merged
into the proper one:

    pick   cf5e2f4 net: Add support for ...
    squash b54da44 (oops) Missing header file
    squash acd54ef (minor) Fix code style
    squash fe29a8c sorry, remove trailing whitespaces

Once you save and close the editor, you'll be prompted to review the final
commit log message of the combined commit. Remove unnecessary lines and save.

    Successfully rebased and updated refs/heads/my-branch

Hint: you might also use *`fixup`* instead of *`squash`*. This would do the
same, but won't ask to review the commit message.
