### Welcome to this Git tutorial!

This tutorial will introduce you to a very popular branching strategy, [scaled trunk-based development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development). This is a simple branching strategy with a main source of truth, the `master` branch, and many short-lived "feature" branches.

The idea is that, when you want to make a change to your code base, you do so on a small, dedicated "feature" branch. You push that branch up to your remote repository, open up a pull request for peer review, merge it into `master`, and then delete it. Then, to do another piece of work, you `pull` the latest version of `master`, and create another "feature" branch.

###### Note: You can copy and paste the commands into your terminal, omitting the `$`. The `$` is simply used to imply that this is a command run on the terminal, since many terminals use `$` to signify where you can begin typing a command.

### Set Up

If you have not used git and GitHub before, you may need to sign up for a GitHub account. Follow [these instructions](https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration) to get set up.

# Instructions:

1. Clone this repository:

```
$ git clone https://github.com/marlenabowen/learning_git.git
```

2. Change your current directory to the repository:

```
$ cd learning_git
```

3. To list the contents of the repository, you can run `$ls -a`

3. To read the contents of the files in the repository, run:

```
$ cat hello_erin.txt
$ cat hello_david.txt
```

4. Create a new git branch:

```
$ git checkout -b hello_marlena
```
###### A note about branch names: feature branch names should reflect the change they introduce to the code base. They should start with a verb, like "adds", for example `adds-mailing-feature`

5. Create a new file:

```
$ touch hello_marlena.txt
```

6. Open the file in your preferred text editor:

```
$ open hello_marlena.txt
```

7. Add some content to the file and save it

8. Run `$ git status` to see the untracked file

9. Run `$ git diff` to see the changes

9. Run `$ git add .` to include the file

10. Run `$ git status` to see the uncomitted changes

11. Run `$ git commit -m "adds hello_marlena.txt"` to commit the change

###### A note about commit messages: like feature branches, commit messages should describe the change they introduce, and usually start with a verb, for example "Adds zipcode to user"

12. You can run `$ git diff --cached` to see the changes again, to verify them before pushing them up to the remote repository

12. Run `$ git push --set-upstream origin hello_marlena` to push the local branch to GitHub (remote)

13. Open a pull request on GitHub and request a review

14. Once reviewed, merge the branch into `master`

15. Delete the remote branch on GitHub

16. `$ git checkout master`

17. `$ git pull`

## Additional Commands:

#### Getting the latest changes

`$ git pull` helps make sure you have the latest changes from the remote branch on your local copy of the branch

#### See a branch's history

To see a list of commits to a branch, run `$ git log`

#### Deleting old branches

It's good practice to delete old local branches.

`$ git branch` will show you the names of all branches you have locally. To delete one, run `$ git branch -D <branch name>`

## Advanced Commands:

#### Rebasing

[Rebasing](https://help.github.com/en/github/using-git/about-git-rebase) is common and important when working on a feature branch for more than a day, while other developers on your team are checking code into `master`. I recommend rebasing your feature branch every day that you are working on it, and before merging it into master.

```
$ git checkout master
$ git pull
$ git checkout <feature branch name>
$ git fetch origin master
$ git rebase master
```

You may have merge conflicts, if someone has committed a change to `master` in a file that you have also changed on your branch. See [this article](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line) on resolving merge conflicts.

#### Amending a commit

You may realize, after pushing a commit, that you need to make a very small change like fixing a typo. Rather than creating another commit just for that typo, you may want to simply amend your previous commit. To add a change to a previous commit, after checking in the change with `$ git add .`, you can run:

```
$ git commit --amend
```

This will open your commit message in vim. To exit, enter `:wq!`

#### Force pushing

After doing something like amending or resetting a commit, you will have to force push those changes to `master`. You can do so via `$ git push -f`.

#### Resetting a commit

Sometimes, you may want to reset a commit or a number of commits. I like to do this when my branch is ready to merge, so that I don't merge a whole bunch of commits into `master`. For example, I may have made small, incremental commits to my feature branch that will not be useful in `master`'s history. Instead, I can reset my commits like this:

```
$ git reset --soft HEAD~<number of commits to reset>
$ git add .
$ git commit -m "Message that makes more sense for master's history"
$ git push -f
```

## Additional Resources

* [https://git-scm.com](https://git-scm.com)
* [https://trunkbaseddevelopment.com](https://trunkbaseddevelopment.com)
