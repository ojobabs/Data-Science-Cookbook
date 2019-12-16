


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

[Fig08]

Figure 20.8 A merge conflict as shown in Atom. You can select the version of the code you wish to keep by clicking one of the Use me buttons, or edit the code in the file directly.

To resolve a merge conflict, you need to take the following steps:

1.  Use  `git status`  to see which files have merge conflicts. Note that multiple files may have conflicts, and each file may have more than one conflict.
    
2.  Choose which version of the code to keep. You do this by editing the files (e.g., in RStudio or Atom). You can make these edits manually, though some IDEs (including Atom) provide buttons that let you directly choose a version of the code to keep (e.g., the “Use me” button in  [Figure 20.8](https://learning.oreilly.com/library/view/Programming+Skills+for+Data+Science:+Start+Writing+Code+to+Wrangle,+Analyze,+and+Visualize+Data+with+R,+First+Edition/9780135159071/ch20.xhtml#fig20_8)).
    
    Note that you can choose to keep the “original”  `HEAD`  version from the current branch, the “incoming” version from the other branch, or some combination thereof. Alternatively, you can replace the conflicting code with something new entirely! Think about what you want the “correct” version of the final code to be, and make it so. Remember to remove the  `<<<<<<<`  and  `=======`  and  `>>>>>>>`  characters; these are not legal code in any language.

> **Tip**
>When resolving a merge conflict, pretend that a cat walked across your keyboard and added a bunch of extra junk to your code. Your task is to fix your work and restore it to a clean, working state.  _Be sure to test your code to confirm that it continues to work after making these changes!_

3. Once you are confident that the conflicts are all resolved and everything works as it should, follow the instructions shown by `git status` to `add` and `commit` the change you made to the code to resolve the conflict:

```bash
# Check current status: have you edited all conflicting files?
git status

# Add and commit all updated files
git add .
git commit -m "Resolve merge conflict"
```
This will complete the merge! Use `git status` to check that everything is clean again.

> **Tip**
>If you want to “cancel” a merge with a conflict (e.g., you initiated a merge, but you don’t want to go through with it because of various conflicts), you can cancel the merge process with the  `**git merge --abort**`  command.

>**Remember**
>_Merge conflicts are expected_. You didn’t do something wrong if one occurs! Don’t worry about getting merge conflicts or try to avoid them: just resolve the conflict, fix the “bug” that has appeared, and move on with your life.

### 1.4. Merging from GitLab

When you  `push`  to and  `pull`  from GitLab, what you’re actually doing is merging your commits with the ones on GitLab! Because GitLab won’t know which version of your files to keep, you will need to resolve all merge conflicts on your machine. This plays out in two ways:

1.  You will  _not_  be able to  `push`  to GitLab if merging your commits  _into_  GitLab’s repo might cause a merge conflict.  `git`  will instead report an error, telling you that you need to  `pull`  changes first and make sure that your version is up to date. “Up to date” in this case means that you have downloaded and merged all the commits on your local machine, so there is no chance of divergent changes causing a merge conflict when you merge by pushing.
    
2.  Whenever you  `pull`  changes from GitLab, there may be a merge conflict. These are resolved in the exact same way as when merging local branches; that is, you need to edit the files to resolve the conflict, then  `add`  and  `commit`  the updated versions.

Thus, when working with GitLab (and especially with multiple people), you will need to perform the following steps to upload your changes:

1.  `pull`  (download) any changes you don’t have
    
2.  _Resolve_  any merge conflicts that occur
    
3.  `push`  (upload) your merged set of changes
    

Of course, because GitLab repositories are repos just like the ones on your local machine, they can have branches as well. You gain access to any  _remote_  branches when you  `clone`  a repo; you can see a list of them with  `git branch -a`  (using the “**a**ll” option).

If you create a new branch on your local machine, it is possible to push that branch to GitLab, creating a mirroring branch on the remote repo (which usually has the alias name  `origin`). You do this by specifying the branch in the  `git push`  command:

```bash
# Push the current branch to the BRANCH_NAME branch on the `origin`
# remote (GitLab)
git push origin BRANCH_NAME
```
where `BRANCH_NAME` is the name of the branch you are currently on (and thus want to push to GitLab). For example, you could push the `experiment` branch to GitLab with the following command:

```bash
# Make sure you are on the `experiment` branch
git checkout experiment

# Push the current branch to the `experiment` branch on GitLab
git push origin experiment
```

You often want to create an association between your local branch with the remote one on GitLab. You can establish this relationship by including the `-u` option in your push:
```bash
# Push to the BRANCH_NAME branch on origin, enabling remote tracking
# The -u creates an association between the local and remote branches
git push -u origin BRANCH_NAME
```
This causes your local branch to “track” the one on GitLab. Then when you run a command such as `git status`, it will tell you whether one repo has more commits than the other. Tracking will be remembered once set up, so you only need to use the `-u` option _once_. It is best to do this the first time you push a local branch to GitLab.

## 2. DEVELOPING PROJECTS USING FEATURE BRANCHES
The main benefit of branches is that they allow you (and others) to simultaneously work on different aspects of the code without disturbing the main code base. Such development is best organized by separating your work across different  **feature branches**—branches that are each dedicated to a different  **feature**  (capability or part) of the project. For example, you might have one branch called  `new-chart`  that focuses on adding a complex visualization, or another branch called  `experimental-analysis`  that tries a bold new approach to processing the data. Importantly, each branch is based on a feature of the project, not a particular person: a single developer could be working on multiple feature branches, and multiple developers could collaborate on a single feature branch (more on this later).

The goal when organizing projects into feature branches is that the  `master`  branch should always contain “**production-level**” code: valid, completely working code that you could deploy or publish (read: give to your boss or teacher) at a whim. All feature branches branch off of  `master`, and are allowed to contain temporary or even broken code (since they are still in development). This way there is always a “working” (if incomplete) copy of the code (`master`), and development can be kept  isolated and considered independent of the whole. Note that this organization is similar to how the earlier example uses an  `experiment`  branch.

Using feature branches works like this:

1. You decide to add a new feature to the project: a snazzy visualization. You create a new feature branch off of `master` to isolate this work:

```bash
# Make sure you are on the `master` branch
git checkout master

# Create and switch to a new feature branch (called `new-chart`)
git checkout -b new-chart
```
2. You then do your coding work while on this branch. Once you have completed some work, you would make a commit to add that progress:
```bash
# Add and commit changes to the current (`new-chart`) branch
git add .
git commit -m "Add progress on new vis feature"
```
3. Unfortunately, you may then realize that there is a bug in the `master` branch. To address this issue, you would switch back to the `master` branch, then create a _new branch_ to fix the bug:

```bash
# Switch from your `new-chart` branch back to `master`
git checkout master

# Create and switch to a new branch `bug-fix` to fix the bug
git checkout -b bug-fix
```
(You would fix a bug on a separate branch if it was complex or involved multiple commits, in order to work on the fix separate from your regular work).
4. After fixing the bug on the `bug-fix`  _branch_, you would `add` and `commit` those changes, then checkout the `master` branch to merge the fix back into `master`:
```bash
# Add and commit changes that fix the bug (on the `bug-fix` branch)
git add .
git commit -m "Fix the bug"

# Switch to the `master` branch
git checkout master

# Merge the changes from `bug-fix` into the current (`master`) branch
git merge bug-fix
```
Now that you have fixed the bug (and merged the changes into `master`), you can get back to developing the visualization (on the `new-chart` branch). When it is complete, you will `add` and `commit` those changes, then checkout the `master` branch to merge the visualization code back into `master`:
``` bash
# Switch back to the `new-chart` branch from the `master` branch
git checkout new-chart

# Work on the new chart...

# After doing some work, add and commit the changes
git add .
git commit -m "Finish new visualization"

# Switch back to the `master` branch
git checkout master

# Merge in changes from the `new-chart` branch
git merge new-chart
```
The use of feature branches helps isolate progress on different elements of a project, reducing the need for repeated merging (and the resultant conflicts) of half-finished features and creating an organized project history. Note that feature branches can be used as part of either the _centralized workflow_ (see Section 3) or the _forking workflow_ (see Section 4).

## 3. COLLABORATION USING THE CENTRALIZED WORKFLOW

This section describes a model for working with multiple collaborators on the same project, coordinating and sharing work through GitLab. In particular, it focuses on the  **centralized workflow,**1 in which all collaborators use a single repository on GitHub. This workflow can be extended to support the use of feature branches (in which each feature is developed on a different branch) as described in  Section 2 —the only additional change is that multiple people can work on each feature! Using the centralized workflow involves configuring a shared repository on GitHub, and managing changes across multiple contributors.

[1] **Atlassian: Centralized Workflow:**  [https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow)

### 3.1 Creating a Centralized Repository

The centralized workflow uses a single repository stored on GitLab—that is, every single member of the collaboration team will  `push`  and  `pull`  to the same GitLab repo. However, since each repository needs to be created under a particular account, a  _single member_  of the team will need to create that repository (e.g., by clicking the  _“New”_  button on the “Repositories” tab on the GitLab web portal).

To make sure everyone is able to  `push`  to the repository, whoever creates the repo will need to add the other team members as collaborators. They can do this under the  _“Settings”_  tab of the repo’s web portal page, as shown in Figure 9. (The creator will want to give all team members “write” access so they can  `push`  changes to the repo.)

Once everyone has been added to the GitLab repository, _each team member_ will need to `clone` the repository to their local machines to work on the code individually, as shown in Figure 10. Collaborators can then `push` any changes they make to the central repository, and `pull` any changes made by others.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0ODkwNTQ3NCwtMTY1NzE0MDYxMSwtMT
k4NjE1OTAxOSwxNTQyNTI3OTYzLC0xMDUxMDM4MTksLTE0ODQy
NTMzOTIsMjA4MjUwNzc1OF19
-->