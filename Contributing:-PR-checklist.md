Commit
------
For each commit be sure that:

  - [x] You used your real name and email to commit

  - [x] The commit is [atomic](http://www.freshconsulting.com/atomic-commits/):
    - Commit each fix or task as a separate change
    - Only commit when a block of work is complete (or commit and squash
      afterwards)
    - Layer changes, e.g. first make a separate commit formatting the code or
      refactoring, then commit the actual logic change. This way, the latter
      commit contains the only minimal diff, which is to be reviewed

  - [x] That is, the commit isn't mixing:
    - ... whitespace changes or code formatting with functional code changes
    - ... large refactorings with logic changes
    - ... two unrelated functional changes

  - [x] The commit log message follows **[the agreements](https://github.com/embox/embox/wiki/Contributing:-Git-commit-message-agreements)**

Open a new Pull Request
-----------------------
Before publishing the branch and proposing a new Pull Request, please check that:

  - [x] None of the commits introduce whitespace errors
    - Rebase with `--whitespace=fix` to ensure that; see the
      [[cheatsheet](https://github.com/embox/embox/wiki/Contributing:-Git-cheatsheet#fix-whitespace-errors)]

  - [x] Your branch is up-to-date with the upstream; fetch and rebase to
    catch-up recent changes from `upstream/master` [[cheatsheet](https://github.com/embox/embox/wiki/Contributing:-Git-cheatsheet#linearize-the-branch-and-catch-up-recent-changes-from-the-upstream)]

  - [x] There are no merge commits, e.g. you didn't accidentally `pull` without
    `--rebase` [[cheatsheet](https://github.com/embox/embox/wiki/Contributing:-Git-cheatsheet#linearize-the-branch-and-catch-up-recent-changes-from-the-upstream)]

  - [x] There are no "oops" or fixup commits; don't forget to 
    squash them [[cheatsheet](https://github.com/embox/embox/wiki/Contributing:-Git-cheatsheet#squash-commits-into-a-single-one)]

  - (ideally) The whole set of commits is bisectable, i.e. the code
    builds and runs fine after applying each commit one by one
    - Run `git rebase upstream/master -i --exec make` to check that

Everything's OK? Now create the PR:

  - Provide the title and the description
    - Follow [commit message agreements](https://github.com/embox/embox/wiki/Contributing:-Git-commit-message-agreements) as a rule of thumb

Integrate feedback
------------------

  - Do not rebase already published changes and force-push **until review is
    over**
    - Push `fixup!` commits instead [[cheatsheet](https://github.com/embox/embox/wiki/Contributing:-Git-cheatsheet#option-b-commit---fixup-followed-by-rebase---autosquash)], then rebase one last time once getting LGTM from maintainers :shipit:

  - [x] For maintainers: Travis CI has finishes building the PR
    - Don't merge until receiving the green mark, even if you believe
      everything's OK. No need to hurry.
