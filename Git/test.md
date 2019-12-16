


> Written with [StackEdit](https://stackedit.io/).

# Working Collaboratively with Branches

To be a successful member of a data science team, you will need to be able to effectively collaborate with others. While this is true for nearly any practice, an additional challenge for collaborative data science is working on shared code for the same project. Many of the techniques for supporting collaborative coding involve writing clear, well-documented code that can be read, understood, and modified by others. But you will also need to be able to effectively _integrate_ your code with code written by others, avoiding any “copy-and-pasting” work for collaboration. The best way to do this is to use a version control system. Indeed, one of the biggest benefits of `git` is its ability to support **collaboration** (working with other people). In this chapter, you will expand your version control skills to maintain different versions of the same code base using `git`’s **branching model**, and familiarize yourself with two different models for collaborative development.

## 1. TRACKING DIFFERENT VERSIONS OF CODE WITH BRANCHES 

To work effectively with others, you need to understand how  `git`  supports nonlinear development on a project through branches. A  **branch**  in  `git`  is a way of labeling a  _sequence of commits_. You can create labeled commit sequences (branches) that exist side by side within the same project, allowing you to effectively have different “lines” of development occurring in parallel and diverging from each other. That is, you can use  `git`  to track multiple different, diverging versions of your code, allowing you to work on multiple versions at the same time.

At this point you know how to use  `git`  when you are working on a single branch (called  `master`) using a  _linear sequence_  of commits. As an example,  Figure.1  illustrates a series of commits for a sample project history. Each one of these commits—identified by its  **hash**  (e.g.,  `e6cfd89`  in short form)—follows sequentially from the previous commit. Each commit builds directly on the other; you would move back and forth through the history in a straight line. This linear sequence represents a workflow using a  _single line of development_. Having a single line of development is a great start for a work process, as it allows you to track changes and revert to earlier versions of your work.

[fig01]

**Figure 1**: A diagram of a linear sequence of commits alongside a log of the commit history as shown in the terminal. This project has a single history of commits (i.e., _branch_), each represented by a six-character _commit hash_. The `HEAD`—most recent commit—is on the `master` branch.

In addition to supporting single development lines, `git` supports a _nonlinear model_ in which you “branch off” from a particular line of development to create new concurrent change histories. You can think of these as “alternate timelines,” which are used for developing different features or fixing bugs. For example, suppose you want to develop a new visualization for your project, but you’re unsure if it will look good and be incorporated. You don’t want to pollute the primary line of development (the “main work”) with experimental code, so instead you _branch off_ from the line of development to work on this code at the same time as the rest of the core work. You are able to commit iterative changes to both the experimental visualization branch and the main development line, as shown in Figure 2. If you eventually decide that the code from the experimental branch is worth keeping, you can easily _merge_ it back into the main development line as if it were created there from the start!

[fig02]

**Figure 2**: A sequence of commits spread across multiple branches, producing “alternate time-lines.” Commits switch between being added to each branch (timeline). The commits on the `bug-fix` branch (labeled G and H) are _merged_ into the `master` branch, becoming part of that history.

### 1.1. Working with Different Branches

All `git` repositories have at least one branch (line of development) where commits are made. By default, this branch is called `master`. You can view a list of current branches in the repo with the `**git branch**` command:

```bash
# See a list of current branches in the repo
git branch
```
The line printed with the asterisk (`*`) is the “current branch” you’re on. You can use the same `git branch` command to create a _new_ branch:
```bash
# Create a new branch called BRANCH_NAME
git branch BRANCH_NAME
```
This will create a new branch called `BRANCH_NAME` (replace `BRANCH_NAME` with whatever name you want; usually not in all caps). For example, you could create a branch called `experiment`:

```bash
# Create a new branch called `experiment`
git branch experiment
```
If you run `git branch` again, you will see that this _hasn’t actually changed what branch you’re on_. In fact, all you have done is create a new branch that _starts_ at the current commit!

To switch to a different branch, you use the `git checkout` command

```bash
# Switch to the BRANCH_NAME branch
git checkout BRANCH_NAME
```
For example, you can switch to the `experiment` branch with the following command:
```bash
# Switch to the `experiment` branch
git checkout experiment
```
_Checking out_ a branch doesn’t actually create a new commit! All it does is change the `HEAD` so that it now refers to the latest commit of the target branch (the alternate timeline). `**HEAD**` is just an alias for “the most recent commit on the current branch.” It lets you talk about the most recent commit generically, rather than needing to use a particular _commit hash_.

You can confirm that the branch has changed by running the `git branch` command and looking for the asterisk (`*`), as shown in Figure 3:

[fig03]

**Figure 3**: Using `git` commands on the command line to display the current branch (`git branch`), and create and checkout a new branch called `experiment` (`git checkout -b experiment`).

Alternatively (and more commonly), you can create _and_ checkout a branch in a single step using the `-b` option with `git checkout`:

```bash
# Create and switch to a branch called BRANCH_NAME
git checkout -b BRANCH_NAME
```
For example, to create and switch to a new branch called `experiment`, you would use the following command:

```bash
# Create and switch to a new branch called `experiment`
git checkout -b experiment
```
This effectively does a `git branch BRANCH_NAME` followed by a `git checkout BRANCH_NAME`. This is the recommended way of creating new branches.

Once you have checked out a particular branch, any new commits from that point on will occur in the “alternate timeline,” without disturbing any other line of development. New commits will be “attached” to the `HEAD` (the most recent commit on the _current_ branch), while all other branches (e.g., `master`) will stay the same. If you use `git checkout` again, you can switch back to the other branch. This process is illustrated in Figure 4:

[fig04]

**Figure 4**: Using `git` to commit to multiple branches. A hollow circle is used to represent where the next commit will be added to the history. Switching branches, as in figures (a), (d), and (f), will change the location of the `HEAD` (the commit that points to the hollow circle), while making new commits, as in figures (b), (c), and (e), will add new commits to the current branch.

Importantly, checking out a branch will “reset” the files and code in the repo to whatever they looked like when you made the last commit on that branch; the code from the other branches’ versions is stored in the repo’s `.git` database. You can switch back and forth between branches and watch your code change!

For example, Figure 5 demonstrates the following steps:

1.  `git status`: Check the status of your project. This confirms that the repo is on the  `master`  branch.
    
2.  `git checkout -b experiment`: Create and checkout a new branch,  `experiment`. This code will  _branch off_  of the  `master`  branch.
    
3.  Make an update to the file in a text editor (still on the  `experiment`  branch).
    
4.  `git commit -am "Update README"`: This will  `add`  and  `commit`  the changes (as a single command)! This commit is made  _only_  to the  `experiment`  branch; it exists in that timeline.
    
5.  `git checkout master`: Switch back to the  `master`  branch. The file switches to show the latest version of the  `master`  branch.
    
6.  `git checkout experiment`: Switch back to the  `experiment`  branch. The file switches to show the latest version of the  `experiment`  branch.

[fig05]

**Figure 5**: Switching branches allows you to work on multiple versions of the code simultaneously.

>**Caution**
>You can only check out a branch if the  _current working directory_  has no uncommitted changes. This means you will need to  `commit`  any changes to the current branch before you  `checkout`  another branch. If you want to “save” your changes but don’t want to commit to them, you can use git’s ability to temporarily  **stash**[a](https://learning.oreilly.com/library/view/Programming+Skills+for+Data+Science:+Start+Writing+Code+to+Wrangle,+Analyze,+and+Visualize+Data+with+R,+First+Edition/9780135159071/ch20.xhtml#ch20sbfn1a)  changes.
>[a](https://learning.oreilly.com/library/view/Programming+Skills+for+Data+Science:+Start+Writing+Code+to+Wrangle,+Analyze,+and+Visualize+Data+with+R,+First+Edition/9780135159071/ch20.xhtml#ch20sbfn1)[https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)

Finally, you can delete a branch using  `git branch -d BRANCH_NAME`. Note that this command will give you a warning if you might lose work; be sure to read the output message!

Taken together, these commands will allow you to develop different aspects of your project  _in parallel_. The next section discusses how to bring these lines of development together.

> **Tip**
>You can also use the  `git checkout BRANCH_NAME FILE_NAME`  command to checkout an individual file from a particular branch. This will load the file directly into the current working directory as a file change,  _replacing_  the current version of the file (`git`  will not merge the two versions of the file together)! This is identical to checking out a file from a past commit, just using a branch name instead of a commit hash.

### 1.2. Merging Branches

If you have changes (commits) spread across multiple branches, eventually you will want to combine those changes back into a single branch. This process is called **merging**: you “merge” the changes from one branch into another. You do this with the (surprise!) `**git merge**` command:

```bash
# Merge OTHER_BRANCH into the current branch
git merge OTHER_BRANCH
```
For example, you can merge the `experiment` branch into the `master` branch as follows:
```bash
# Make sure you are on the `master` branch
git checkout master

# Merge the `experiment` branch into the current (`master`) branch
git merge experiment
```
The `merge` command will (in effect) walk through each line of code in the two versions of the files, looking for any differences. Changes to each line of code in the _incoming_ branch will then be applied to the equivalent line in the current branch, so that the current version of the files contains all of the incoming changes. For example, if the `experiment` branch included a commit that added a new code statement to a file at line 5, changed the code statement at line 9, and deleted the code statement at line 13, then `git` would add the new line 5 to the file (pushing everything else down), change the code statement that was at line 9, and delete the code statement that was at line 13. `git` will automatically “stitch” together the two versions of the files so that the current version contains _all_ of the changes.

> **Tip**
>When merging, think about where you want the code to “end up”—that is the branch you want to checkout and merge into!

In effect, merging will take the commits from another branch and insert them into the history of the current branch. This is illustrated in Figure 6:

[fig06]

**Figure 6**: Merging an `experiment` branch into the `master` branch. The committed changes from the `experiment` branch (labeled C and D) are inserted into the `master` branch’s history, while also remaining present in the `experiment` branch.

Note that the `git merge` command will merge `OTHER_BRANCH` into the branch you are currently on. For example, if you want to take the changes from your `experiment` branch and merge them into your `master` branch, you will need to first `checkout` your `master` branch, and merge in the changes from the `experiment` branch.

> **Caution**
> If something goes wrong, don’t panic and close your command shell! Instead, take a breath and look up how to fix the problem you’ve encountered (e.g., how to exit  _vim_). As always, if you’re unsure why something isn’t working with git, use  `git status`  to check the current status and to determine which steps to do next.

If the two branches have not edited the same line of code, `git` will stitch the files together seamlessly and you can move forward with your development. Otherwise, you will have to resolve any _conflict_ that occurs as part of your merge.

### 1.3. Merge conflicts

If you perform a merge between two branches that have different commits that edit the _same lines of code_ the result will be a **merge conflict** (so called because the changes are in “conflict”), as demonstrated in Figure 7.

[fig07]

**Figure 7**: A merge conflict as shown in the command shell.

`git` is just a simple computer program, and has no way of knowing which version of the conflicting code it should keep—is the `master` version or the `experiment` version better? Since `git` can’t determine which version of the code to keep, it stops the merge in the middle and forces you to choose what code is correct _manually_.

To resolve the merge conflict, you will need to edit the files (code) to pick which version to keep. `git`  adds special characters (e.g., `<<<<<<<<`) to the files to indicate where it encountered a conflict (and thus where you need to make a decision about which code to keep), as shown in Figure 8.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NTUzNzQ1MCwtMTA1MTAzODE5LC0xND
g0MjUzMzkyLDIwODI1MDc3NThdfQ==
-->