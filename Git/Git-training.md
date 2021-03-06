


> Written with [StackEdit](https://stackedit.io/).

# Git for Data Scientists

## Basic Workflow

### What is version control?

A  **version control system**  is a tool that manages changes made to the files and directories in a project. Many version control systems exist; this lesson focuses on one called Git, which is used by many of the data science tools covered in our other lessons. Its strengths are:

-   Nothing that is saved to Git is ever lost, so you can always go back to see which results were generated by which versions of your programs.
    
-   Git automatically notifies you when your work conflicts with someone else's, so it's harder (but not impossible) to accidentally overwrite work.
    
-   Git can synchronize work done by different people on different machines, so it scales as your team does.
    

Version control isn't just for software: books, papers, parameter sets, and anything that changes over time or needs to be shared can and should be stored and shared using something like Git.

### Where does Git store information?

Each of your Git projects has two parts: the files and directories that you create and edit directly, and the extra information that Git records about the project's history. The combination of these two things is called a  **repository**.

Git stores all of its extra information in a directory called  `.git`  located in the root directory of the repository. Git expects this information to be laid out in a very precise way, so you should never edit or delete anything in  `.git`.

---

Suppose your home directory `/home/repl` contains a repository called `dental`, which has a sub-directory called `data`. Where is information about the history of the files in `/home/repl/dental/data`stored?

  Answers
- [ ]  `/home/repl/.git`
- [X] `/home/repl/dental/.git`
- [ ] `/home/repl/dental/data/.git`
- [ ] None of the above.

### How can I check the state of a repository?

When you are using Git, you will frequently want to check the  **status**  of your repository. To do this, run the command  `git status`, which displays a list of the files that have been modified since the last time changes were saved.

---
You have been put in the `dental`repository. Use `git status` to discover which file(s) have been changed since the last save. Which file(s) are listed?

##### Possible Answers

- [ ]   `data/summer.csv`.
    
-   [X] `report.txt`.
    
-   [ ] Neither of the above.
    
-   [ ] Both of the above.

### How can I tell what I have changed?

Git has a  **staging area**  in which it stores files with changes you want to save that haven't been saved yet. Putting files in the staging area is like putting things in a box, while  **committing**  those changes is like putting that box in the mail: you can add more things to the box or take things out as often as you want, but once you put it in the mail, you can't make further changes.

![](https://s3.amazonaws.com/assets.datacamp.com/production/course_5355/datasets/staging-area.png)

`git status` shows you which files are in this staging area, and which files have changes that haven't yet been put there. In order to compare the file as it currently is to what you last saved, you can use `git diff filename`. `git diff` without any filenames will show you all the changes in your repository, while `git diff directory` will show you the changes to the files in some directory.

---

You have been put in the `dental`repository. Use `git diff` to see what changes have been made to the files.

```git
$ git diff
diff --git a/data/northern.csvb/data/northern.csv
index 5eb7a96..5a2a259 100644
--- a/data/northern.csv
+++ b/data/northern.csv
@@ -22,3 +22,4 @@ Date,Tooth
 2017-08-13,incisor
 2017-08-13,wisdom
 2017-09-07,molar
+2017-11-01,bicuspid
```
### What is in a diff?

A  **diff**  is a formatted display of the differences between two sets of files. Git displays diffs like this:

```git
diff --git a/report.txt b/report.txt
index e713b17..4c0742a 100644
--- a/report.txt
+++ b/report.txt
@@ -1,4 +1,4 @@
-# Seasonal Dental Surgeries 2017-18
+# Seasonal Dental Surgeries (2017) 2017-18
```

This shows:

-   The command used to produce the output (in this case,  `diff --git`). In it,  `a`  and  `b`are placeholders meaning "the first version" and "the second version".
-   An index line showing keys into Git's internal database of changes. We will explore these in the next chapter.
-   `--- a/report.txt`  and  `+++ b/report.txt`, which indicate that lines being  _removed_ are prefixed with  `-`, while lines being added are prefixed with  `+`.
-   A line starting with  `@@`  that tells where the changes are being made. The pairs of numbers are  `start line,number of lines changed`. Here, the diff output shows that 4 lines from line 1 are being removed and replaced with new lines.
-   A line-by-line listing of the changes with  `-`  showing deletions and  `+`  showing additions. (We have also configured Git to show deletions in red and additions in green.) Lines that  _haven't_  changed are sometimes shown before and after the ones that have in order to give context; when they appear, they  _don't_  have either  `+`  or  `-`in front of them.

Desktop programming tools like  [RStudio](https://www.rstudio.com/)  can turn diffs like this into a more readable side-by-side display of changes; you can also use standalone tools like  [DiffMerge](https://sourcegear.com/diffmerge/)  or  [WinMerge](http://winmerge.org/).

---

You have been put in the  `dental`repository. Use  `git diff data/northern.csv`  to look at the changes to that file. How many lines have been changed?

```git
$ cd dental
$ git diff data/northern.csv
diff --git 
a/data/northern.csv
b/data/northern.csv
index 5eb7a96..5a2a259 100644
--- a/data/northern.csv
+++ b/data/northern.csv
@@ -22,3 +22,4 @@ Date,Tooth
 2017-08-13,incisor
 2017-08-13,wisdom
 2017-09-07,molar
+2017-11-01,bicuspid
```

##### Possible Answers

-  [ ] None.
    
-   [X] 1.
    
-   [ ] 2.
    
-   [ ] 20.

### What's the first step in saving changes?

You commit changes to a Git repository in two steps:

1.  Add one or more files to the staging area.
2.  Commit everything in the staging area.

To add a file to the staging area, use  `git add filename`.

---

You have been put in the `dental`repository. Use `git add` to add the file `report.txt` to the staging area.

```git
$ cd dental
$ git add report.txt
```

Use another Git command to check the repository's status.

Let's see what happens before and after using `git add`:
```git
$ cd dental
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   report.txt

no changes added to commit (use "git add" and/or "git commit -a")
$ git add report.txt
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   report.txt
```

### How can I tell what's going to be committed?

To compare the state of your files with those in the staging area, you can use  `git diff -r HEAD`. The  `-r`  flag means "compare to a particular revision", and  `HEAD`  is a shortcut meaning "the most recent commit".

You can restrict the results to a single file or directory using  `git diff -r HEAD path/to/file`, where the path to the file is relative to where you are (for example, the path from the root directory of the repository).

We will explore other uses of  `-r`  and  `HEAD`  in the next chapter.

---

You have been put in the `dental`repository, where `data/northern.csv` has been added to the staging area. Use `git diff` with `-r` and an argument to see how files differ from the last saved revision.

```git
$ git diff -r HEAD
diff --git a/data/eastern.csv b/data/eastern.csv
index b3c1688..85053c3 100644
--- a/data/eastern.csv
+++ b/data/eastern.csv
@@ -23,3 +23,4 @@ Date,Tooth
 2017-08-02,canine
 2017-08-03,bicuspid
 2017-08-04,canine
+2017-11-02,molar
diff --git a/data/northern.csv b/data/northern.csv
index 5eb7a96..5a2a259 100644
--- a/data/northern.csv
+++ b/data/northern.csv
@@ -22,3 +22,4 @@ Date,Tooth
 2017-08-13,incisor
 2017-08-13,wisdom
 2017-09-07,molar
+2017-11-01,bicuspid
```
Use a single Git command to view the changes in the file that has been staged (and _only_ that file).

```git
$ git diff -r HEAD data/northern.csv
diff --git a/data/northern.csv b/data/northern.csv
index 5eb7a96..5a2a259 100644
--- a/data/northern.csv
+++ b/data/northern.csv
@@ -22,3 +22,4 @@ Date,Tooth
 2017-08-13,incisor
 2017-08-13,wisdom
 2017-09-07,molar
+2017-11-01,bicuspid
```

`data/eastern.csv`  hasn't been added to the staging area yet. Use a Git command to do this now.

```git
$ git add data/eastern.csv
```

### Interlude: how can I edit a file?

Unix has a bewildering variety of text editors. In this course, we will sometimes use a very simple one called Nano. If you type  `nano filename`, it will open  `filename`  for editing (or create it if it doesn't already exist). You can then move around with the arrow keys, delete characters with the backspace key, and so on. You can also do a few other operations with control-key combinations:

-   Ctrl-K: delete a line.
-   Ctrl-U: un-delete a line.
-   Ctrl-O: save the file ('O' stands for 'output').
-   Ctrl-X: exit the editor.

---

Run  `nano names.txt`  to edit a new file in your home directory and enter the following four lines:

```
Lovelace
Hopper
Johnson
Wilson
```

To save what you have written, type Ctrl-O to write the file out, then Enter to confirm the filename, then Ctrl-X and Enter to exit the editor.

### How do I commit changes?

To save the changes in the staging area, you use the command  `git commit`. It always saves everything that is in the staging area as one unit: as you will see later, when you want to undo changes to a project, you undo all of a commit or none of it.

When you commit changes, Git requires you to enter a  **log message**. This serves the same purpose as a comment in a program: it tells the next person to examine the repository why you made a change.

By default, Git launches a text editor to let you write this message. To keep things simple, you can use  `-m "some message in quotes"`  on the command line to enter a single-line message like this:

```
git commit -m "Program appears to have become self-aware."

```

If you accidentally mistype a commit message, you can change it using the  `--amend`  flag.

```
git commit --amend - m "new message"
``` 
---

You have been put in the `dental`repository, and `report.txt` has been added to the staging area. Use a Git command to check the status of the repository.

```git
$ cd dental
$ git add report.txt
$ git status
On branch master
Changes to be committed:  (use "git reset HEAD <file>..." to unstage)

        modified:   report.txt

```

Commit the changes in the staging area with the message "Adding a reference."

```git
$ git commit -m "Adding a reference."
```

### How can I view a repository's history?

The command  `git log`  is used to view the  **log**  of the project's history. Log entries are shown most recent first, and look like this:

```
commit 0430705487381195993bac9c21512ccfb511056d
Author: Rep Loop <repl@datacamp.com>
Date:   Wed Sep 20 13:42:26 2017 +0000

    Added year to report title.

```

The  `commit`  line displays a unique ID for the commit called a  **hash**; we will explore these further in the next chapter. The other lines tell you who made the change, when, and what log message they wrote for the change.

When you run  `git log`, Git automatically uses a pager to show one screen of output at a time. Press the space bar to go down a page or the 'q' key to quit.

----------

You are in the directory  `dental`, which is a Git repository. Use a single Git command to view the repository's history. What is the message on the very first entry in the log (which is displayed last)?

```git
$ git logcommit 610de9192eb50716c2447622bc36d19873f54554
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000
    Added year to report title.

commit 90959a632eed76570dc8fd9c448d48e1abf1174d
Author: Rep Loop <repl@datacamp.com>Date:   Mon Jul 15 17:11:48 2019 +0000
    Adding fresh data for western region.commit b001be7b2c9ecc538d1390dfc2f038b682d33d17
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for southern and western regions.
commit ebaf5c1169621398e713346fc508e1388dfe220e
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

commit 610de9192eb50716c2447622bc36d19873f54554
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000
    Added year to report title.

commit 90959a632eed76570dc8fd9c448d48e1abf1174d
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for western region.
commit b001be7b2c9ecc538d1390dfc2f038b682d33d17
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000
    Adding fresh data for southern and western reg
ions.
commit ebaf5c1169621398e713346fc508e1388dfe220e
Author: Rep Loop <repl@datacamp.com>Date:   Mon Jul 15 17:11:48 2019 +0000

    Fixed bug and regenerated results.
    1. bin/teeth was selecting column 1 instead of
 column 2: fixed.    2. Regenerated dependent results.

commit 9e1367c2539dde990fef44aecd80318b7b02d2b6
Author: Rep Loop <repl@datacamp.com>
:
```

##### Possible Answers

- [X]  "Added summary report file."
    
-   [ ] "Added seasonal CSV data files"
    
-   [ ] "Fixed bug and regenerated results."
    
-   [ ] "Added reminder to cite funding sources."

### How can I view a specific file's history?

A project's entire log can be overwhelming, so it's often useful to inspect only the changes to particular files or directories. You can do this using  `git log path`, where  `path`  is the path to a specific file or directory. The log for a file shows changes made to that file; the log for a directory shows when files were added or deleted in that directory, rather than when the contents of the directory's files were changed.

----------

You have been put in the  `dental`  repository. Use  `git log`  to display only the changes made to  `data/southern.csv`. How many have there been?

```git
$ git log data/southern.csv
commit b001be7b2c9ecc538d1390dfc2f038b682d33d17
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for southern and western regions.

commit 2712f6668534f5dfd942ada335cadc5ce22b62df
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Added seasonal CSV data files
```

##### Possible Answers

-   [ ] 0.
    
-   [ ] 1.
    
-   [X] 2.
    
-   [ ] 3.

### How do I write a better log message?

Writing a one-line log message with  `git commit -m "message"`is good enough for very small changes, but your collaborators (including your future self) will appreciate more information. If you run  `git commit`_without_  `-m "message"`, Git launches a text editor with a template like this:

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Your branch is up-to-date with 'origin/master'.
#
# Changes to be committed:
#       modified:   skynet.R
#

```

The lines starting with  `#`  are comments, and won't be saved. (They are there to remind you what you are supposed to do and what files you have changed.) Your message should go at the top, and may be as long and as detailed as you want.

---

You have been put in the `dental`repository, and `report.txt` has been added to the staging area. The changes to `report.txt` have already been staged. Use `git commit`  _without_  `-m` to commit the changes. The Nano editor will open up. Write a meaningful message and use Ctrl+O and Ctrl+X to save and leave the editor.


### How does Git store information?

You may wonder what information is stored by each commit that you make. Git uses a three-level structure for this.

1.  A  **commit**  contains metadata such as the author, the commit message, and the time the commit happened. In the diagram below, the most recent commit is at the bottom (`feed0098`), and vertical arrows point up towards the previous ("parent") commits.
2.  Each commit also has a  **tree**, which tracks the names and locations in the repository when that commit happened. In the oldest (top) commit, there were two files tracked by the repository.
3.  For each of the files listed in the tree, there is a  **blob**. This contains a compressed snapshot of the contents of the file when the commit happened. (Blob is short for  _binary large object_, which is a SQL database term for "may contain data of any kind".) In the middle commit,  `report.md`  and  `draft.md`  were changed, so the blobs are shown next to that commit.  `data/northern.csv`  didn't change in that commit, so the tree links to the blob from the previous commit. Reusing blobs between commits help make common operations fast and minimizes storage space.

![](https://s3.amazonaws.com/assets.datacamp.com/production/course_5355/datasets/commit-tree-blob.png)

Looking at the diagram, which files changed in the most recent commit to this repository?

##### Possible Answers

- [X]  `data/northern.csv`
    
-  [ ] `report.md`
    
-  [ ] `draft.md`

### What is a hash?

Every commit to a repository has a unique identifier called a  **hash**  (since it is generated by running the changes through a pseudo-random number generator called a  **hash function**). This hash is normally written as a 40-character hexadecimal string like  `7c35a3ce607a14953f070f0f83b5d74c2296ef93`, but most of the time, you only have to give Git the first 6 or 8 characters in order to identify the commit you mean.

Hashes are what enable Git to share data efficiently between repositories. If two files are the same, their hashes are guaranteed to be the same. Similarly, if two commits contain the same files and have the same ancestors, their hashes will be the same as well. Git can therefore tell what information needs to be saved where by comparing hashes rather than comparing entire files.

----------

Use  `cd`  to go into the  `dental`  directory and then run  `git log`. What are the first four characters of the hash of the most recent commit?

```git
$ cd dental
$ git log
commit 610de9192eb50716c2447622bc36d19873f54554
Author: Rep Loop <repl@datacamp.com>Date:   Mon Jul 15 17:11:48 2019 +0000

    Added year to report title.

commit 90959a632eed76570dc8fd9c448d48e1abf1174d
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for western region.

commit b001be7b2c9ecc538d1390dfc2f038b682d33d17
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for southern and western regions.

commit ebaf5c1169621398e713346fc508e1388dfe220e
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Fixed bug and regenerated results.
:
```
##### Possible Answers

-   [ ] bedc
    
-   [ ] 2e1b
    
-   [ ] 2e95
    
-   [x] None of the above

### How can I view a specific commit?

To view the details of a specific commit, you use the command  `git show`  with the first few characters of the commit's hash. For example, the command  `git show 0da2f7`  produces this:

```
commit 0da2f7ad11664ca9ed933c1ccd1f3cd24d481e42
Author: Rep Loop <repl@datacamp.com>
Date:   Wed Sep 5 15:39:18 2018 +0000

    Added year to report title.

diff --git a/report.txt b/report.txt
index e713b17..4c0742a 100644
--- a/report.txt
+++ b/report.txt
@@ -1,4 +1,4 @@
-# Seasonal Dental Surgeries 2017-18
+# Seasonal Dental Surgeries (2017) 2017-18

 TODO: write executive summary.

```

The first part is the same as the log entry shown by  `git log`. The second part shows the changes; as with  `git diff`, lines that the change removed are prefixed with  `-`, while lines that it added are prefixed with  `+`.

----------

You have been put in the  `dental`  directory. Use  `git log`  to see the hashes of recent commits, and then  `git show`  with the first few digits of a hash to look at the most recent commit. How many files did it change?

Reminder: press the space bar to page down through  `git log`'s output and  `q`  to quit the paged display.
```git
$ git show 610de9192
commit 610de9192eb50716c2447622bc36d19873f54554
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Added year to report title.

diff --git a/report.txt b/report.txt
index e713b17..4c0742a 100644
--- a/report.txt
+++ b/report.txt
@@ -1,4 +1,4 @@
-# Seasonal Dental Surgeries 2017-18
+# Seasonal Dental Surgeries (2017) 2017-18

 TODO: write executive summary.

```

##### Possible Answers

-  [ ] None.
    
-   [X] 1.
    
-   [ ] 2.
    
-   [ ] 4.
    
Submit Answer

### What is Git's equivalent of a relative path?

A hash is like an absolute path: it identifies a specific commit. Another way to identify a commit is to use the equivalent of a relative path. The special label  `HEAD`, which we saw in the previous chapter, always refers to the most recent commit. The label  `HEAD~1`  then refers to the commit before it, while  `HEAD~2`  refers to the commit before that, and so on.

Note that the symbol between  `HEAD`  and the number is a tilde  `~`,  _not_  a minus sign  `-`, and that there cannot be spaces before or after the tilde.

----------

You are in the  `dental`  repository. Using a single Git command, show the commit made just before the most recent one. Which of the following files did it change?
```git
$ git show HEAD~1
commit 90959a632eed76570dc8fd9c448d48e1abf1174d
Author: Rep Loop <repl@datacamp.com>
Date:   Mon Jul 15 17:11:48 2019 +0000

    Adding fresh data for western region.

diff --git a/data/western.csv b/data/western.csv
index f6d6374..f7c4509 100644
--- a/data/western.csv
+++ b/data/western.csv
@@ -27,3 +27,6 @@ Date,Tooth
 2017-10-05,molar
 2017-10-06,incisor
 2017-10-07,incisor
+2017-10-15,molar
+2017-10-17,bicuspid
+2017-10-18,bicuspid
```
##### Possible Answers

-  [ ] `report.txt`.
    
-   [X] `data/western.csv`.
    
-   [ ] Both of the above.
    
-   [ ] Neither of the above.

### How can I see who changed what in a file?

`git log`  displays the overall history of a project or file, but Git can give even more information: the command  `git annotate file`  shows who made the last change to each line of a file and when. For example, the first three lines of output from  `git annotate report.txt`  look something like this:

```
04307054        (  Rep Loop     2017-09-20 13:42:26 +0000       1)# Seasonal Dental Surgeries (2017) 2017-18
5e6f92b6        (  Rep Loop     2017-09-20 13:42:26 +0000       2)
5e6f92b6        (  Rep Loop     2017-09-20 13:42:26 +0000       3)TODO: write executive summary.

```

Each line contains five things, with two to four in parentheses.

1.  The first eight digits of the hash,  `04307054`.
2.  The author,  `Rep Loop`.
3.  The time of the commit,  `2017-09-20 13:42:26 +0000`.
4.  The line number,  `1`.
5.  The contents of the line,  `# Seasonal Dental Surgeries (2017) 2017-18`.

----------

You are in the  `dental`  repository. Use a single command to see the changes to  `report.txt`. How many different sets of changes have been made to this file (i.e., how many different hashes show up in the first column of the output)?

```git
$ git annotate report.txt
610de919        (  Rep Loop     2019-07-15 17:11:48 +0000       1)# Seasonal Dental Surgeries (2017) 2017-18
472e96ae        (  Rep Loop     2019-07-15 17:11:48 +0000       2)
472e96ae        (  Rep Loop     2019-07-15 17:11:48 +0000       3)TODO: write executive summary.
472e96ae        (  Rep Loop     2019-07-15 17:11:48 +0000       4)
472e96ae        (  Rep Loop     2019-07-15 17:11:48 +0000       5)TODO: include link to raw data.
9e15b9ea        (  Rep Loop     2019-07-15 17:11:48 +0000       6)
9e15b9ea        (  Rep Loop     2019-07-15 17:11:48 +0000       7)TODO: remember to cite funding sources!
```
##### Possible Answers

-   [ ] 1.
    
-   [X] 3.
    
-   [ ] 4.
    
-   [ ] 7.
    

Submit Answer

### How can I see what changed between two commits?

`git show`  with a commit ID shows the changes made  _in_  a particular commit. To see the changes  _between_  two commits, you can use  `git diff ID1..ID2`, where  `ID1`  and  `ID2`  identify the two commits you're interested in, and the connector  `..`is a pair of dots. For example,  `git diff abc123..def456`  shows the differences between the commits  `abc123`  and  `def456`, while  `git diff HEAD~1..HEAD~3`  shows the differences between the state of the repository one commit in the past and its state three commits in the past.

----------

You are in the  `dental`  repository. Use  `git diff`  to view the differences between its current state and its state two commits previously. Which of the following files have changed?

```git
$ cd dental
$ git diff HEAD..HEAD~2
diff --git a/data/western.csv b/data/western.csv
index f7c4509..f6d6374 100644
--- a/data/western.csv
+++ b/data/western.csv
@@ -27,6 +27,3 @@ Date,Tooth
 2017-10-05,molar
 2017-10-06,incisor
 2017-10-07,incisor
-2017-10-15,molar
-2017-10-17,bicuspid
-2017-10-18,bicuspid
diff --git a/report.txt b/report.txt
index 4c0742a..e713b17 100644
--- a/report.txt
+++ b/report.txt
@@ -1,4 +1,4 @@
-# Seasonal Dental Surgeries (2017) 2017-18
+# Seasonal Dental Surgeries 2017-18

 TODO: write executive summary.

```
##### Possible Answers

-   [ ] `data/western.csv`.
    
-   [ ] `report.txt`.
    
-   [ ] `data/southern.csv`.
    
-   [X] `report.txt`  and  `data/western.csv`.
    
-   [ ] `report.txt`  and  `data/southern.csv`.

### How do I add new files?

Git does not track files by default. Instead, it waits until you have used  `git add`  at least once before it starts paying attention to a file.

In the diagram you saw at the start of the chapter, the untracked files won't have a blob, and won't be listed in a tree.

The untracked files won't benefit from version control, so to make sure you don't miss anything,  `git status`  will always tell you about files that are in your repository but aren't (yet) being tracked.

---

You are in the `dental` repository. Use `git status` to find the files that aren't yet being tracked.

```git
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        sources.txt

nothing added to commit but untracked files present (use "git add" to track)
```
Use `git add` to add the new file to the staging area.
```git
$ git add sources.txt
```
Use `git commit` to save the staged files with the message "Starting to track data sources."
```git
$ git commit -m "Starting to track data sources"
[master b1d072a] Starting to track data sources
 1 file changed, 1 insertion(+)
 create mode 100644 sources.txt
```

### How do I tell Git to ignore certain files?

Data analysis often produces temporary or intermediate files that you don't want to save. You can tell it to stop paying attention to files you don't care about by creating a file in the root directory of your repository called  `.gitignore`  and storing a list of  **wildcard**  patterns that specify the files you don't want Git to pay attention to. For example, if  `.gitignore`  contains:

```
build
*.mpl
```

then Git will ignore any file or directory called  `build`  (and, if it's a directory, anything in it), as well as any file whose name ends in  `.mpl`.

----------

Which of the following files would  _not_  be ignored by a  `.gitignore`  that contained the lines:

```
pdf
*.pyc
backup
```
##### Possible Answers

-  [X] `report.pdf`
-  [ ]  `bin/analyze.pyc`
-   [ ] `backup/northern.csv`
-   [ ] None of the above.

### How can I remove unwanted files?

Git can help you clean up files that you have told it you don't want. The command  `git clean -n`  will show you a list of files that are in the repository, but whose history Git is not currently tracking. A similar command  `git clean -f`  will then delete those files.

_Use this command carefully:_  `git clean`  only works on untracked files, so by definition, their history has not been saved. If you delete them with  `git clean -f`, they're gone for good.

---
You are in the `dental` repository. Use `git status` to see the status of your repo.
```git
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        backup.log

nothing added to commit but untracked files present (use "git add" to track)
```
`backup.log` appears to be an untracked file and it's one we don't need. Let's get rid of it. Use `git clean` with the appropriate flag to remove unwanted files.
```git
$ git clean -f
Removing backup.log
```
List the files in your directory. `backup.log` should no longer be there!
```git
$ ls
bin  data  report.txt  results
```
### How can I see how Git is configured?

Like most complex pieces of software, Git allows you to change its default settings. To see what the settings are, you can use the command  `git config --list`  with one of three additional options:

-   `--system`: settings for every user on this computer.
-   `--global`: settings for every one of your projects.
-   `--local`: settings for one specific project.

Each level overrides the one above it, so  **local settings**  (per-project) take precedence over  **global settings**  (per-user), which in turn take precedence over  **system settings**  (for all users on the computer).

----------

You are in the  `dental`  repository. How many local configuration values are set in for this repository?

```git
$ git config --list --local
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```
##### Possible Answers

-   [ ] None.
    
-   [ ] 3.
    
-   [X] 4.
    
-   [ ] 7.

>Correct! Config settings are useful for storing your name and email address (to identify you in commit logs), choosing your favorite text editor and diff view tools, and customizing things just how you like them.

### How can I change my Git configuration?

Most of Git's settings should be left as they are. However, there are two you should set on every computer you use: your name and your email address. These are recorded in the log every time you commit a change, and are often used to identify the authors of a project's content in order to give credit (or assign blame, depending on the circumstances).

To change a configuration value for all of your projects on a particular computer, run the command:

```
git config --global setting.name setting.value
```

with the setting's name and value in the appropriate places. The keys that identify your name and email address are  `user.name`  and  `user.email`  respectively.

---
Change the email address (`user.email`) configured for the current user for _all_ projects to `rep.loop@datacamp.com`.

```git
$ git config  --global user.email rep.loop@datacamp.com
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNzk0MTMwMzUsLTEyNzIzMzYwMDcsLT
ExMTM4MDcwOCwxNjM0ODM3MjIyLDIwNDc2Njc5MjMsODIzOTMz
MDIxLDE5NjA0MDA4MjAsMTI1NzAzMTE4LC0yMTg3ODU5OSwxMD
k3NzMyOTU3LC00OTA4MjE3OTEsNTIwMjM1NTEwLC02MDk3NDQz
NDgsMTg2NDExNzc2OCwxNDYwODQ5MzkyLDU4NzEwODEzNCw5OD
kyNjI0MjgsLTExNzYwNjc2NjMsMTU1OTg4OTkwLDEzOTEyMTc4
NzJdfQ==
-->