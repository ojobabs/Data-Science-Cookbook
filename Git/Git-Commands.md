> Written with [StackEdit](https://stackedit.io/).

### Git global setup

```bash
git config --global user.name "Marcos"
git config --global user.email "marcos_aguilerakeyser@newyorklife.com"
```

### Create a new repository

```bash
git clone git@nylgit.newyorklife.com:CDSA/cross-sell-up-sell-leads-from-agent-bob.git
cd cross-sell-up-sell-leads-from-agent-bob
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```
### Existing folder or Git repository

```bash
cd existing_folder
git init
git remote add origin git@nylgit.newyorklife.com:CDSA/cross-sell-up-sell-leads-from-agent-bob.git
git add .
git commit
git push -u origin master
```

### Remove directory from remote repository

```bash
git rm -r --cached node_modules
git commit -m 'Remove the now ignored directory node_modules'
git push origin master
```
[Reference](https://gist.github.com/sabarasaba/3080590)

### [Git's rejected push error](https://blog.plover.com/prog/git-ff-error.html)

When the following error arise after using `git push origin master`:


```
! [rejected]        master -> master (fetch first)  
    error: failed to push some refs to '../remote/'  
    hint: Updates were rejected because the remote contains work that you do  
    hint: not have locally. This is usually caused by another repository pushing  
    hint: to the same ref. You may want to first integrate the remote changes  
    hint: (e.g., 'git pull ...') before pushing again.  
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.  
```
The steps to follow are:

First: git fetch origin master using:

```
git fetch origin master
```

Second: Rewrite the local changes:

```
git rebase origin/master
```

Third: Try the push again:

```
git push origin master
```

### Remove a file from a  Git repository

If the file is on the local repository use `git_rm`:

```
git rm file.txt
git commit -m "Remove file1.txt"
```

But if you want to remove the file only from the remote Git repository and not remover it from the filesystem, use:

```
git rm --cached file1.txt
git commit -m "remove file1.txt"
```
And to push changes to remote repo:

```
git push origin master
```
[Reference](https://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo/28772827)

###  git init

This initializes a new Git repository, and you'll notice that it creates a `.git` folder so that you can start your project (this is hidden by default on Unix-based and Windows operating systems).

### git clone

The other situation you might find yourself in is working on an existing project and needing to create a local repository. This can be done with the `git clone` command. You specify a URL with a protocol (such as https:// or git://) and Git fetches all of the information for that repository before putting it in a folder for that project. It also constructs a working copy from the latest commit on master so that you can begin working on the files immediately.

### git add



----

### Creates a working repository using Git

```bash

```

### How to stop tracking and ignore changes to a file in Git - Create a `.gitignore` file
First create a `.gitignore` file:
```bash
project $ touch .gitignore
```
Then add the name of the file or files you want to ignore:
```bash
project $ echo ".remote-sync.jason" > .gitignore
```
Now Git stops tracking the file `.remote-sync.jason`. The `.gitignore` file is also ignored.

If you want to ignore all files with an specific extension, for example, `.txt` files, just use:
```bash
project $ echo "*.txt" > .gitignore
```
You can also ignore all files with the same path on the title, for example, all files starting by `video.`:
```bash
project $ echo "*.txt video.*" > .gitignore
```
Or just video on their titles:
```bash
project $ echo "*.txt video*" > .gitignore
```
In order to ignore folders:
```bash
project $ echo "*.txt Temp/" > .gitignore
```
The `/` signify that `Temp` is a directory. Adding a * ignores all files in that directory:
```bash
project $ echo "*.txt Temp/*" > .gitignore
```
If you want to ignore all Temp folders within the folder:
```bash
project $ echo "*.txt */Temp/*" > .gitignore
```
[Reference](https://www.google.com/search?q=how+to+use+gitignore&rlz=1C1GGRV_enUS765US765&oq=how+to+use+gitignore&aqs=chrome.0.0l6.6549j0j9&sourceid=chrome&ie=UTF-8#kpvalbx=1
)

### How can I determine the URL that a local Git repository was originally cloned from?
If you want only the remote URL, or referential integrity has been broken:
```bash
git config --get remote.origin.url
```
This is the output:
```bash
https://gitlab.com/magkey/test_project.git
```
If you require full output or referential integrity is intact:
```bash
git remote show origin
```
When using `git clone` (from GitHub, or any source repository for that matter) the default name for the source of the clone is "origin". Using `git remote show` will display the information about this remote name. The first few lines should show:
```bash
* remote origin
  Fetch URL: https://gitlab.com/magkey/test_project.git
  Push  URL: https://gitlab.com/magkey/test_project.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':

    master pushes to master (up to date)
```
[Reference](https://stackoverflow.com/questions/4089430/how-can-i-determine-the-url-that-a-local-git-repository-was-originally-cloned-fr)

### Create a new branch

```git
# See a list of current branches in the repo
git branch

# Create a new branch called BRANCH_NAMEgit branch BRANCH_NAME
git branch BRANCH_NAME

# Switch to the BRANCH_NAME branch
git checkout BRANCH_NAME
```


### [Git log to get commits only for a specific branch](https://stackoverflow.com/questions/14848274/git-log-to-get-commits-only-for-a-specific-branch)

From what it sounds like you should be using `cherry`:

```git
$ git cherry -v master traditional
```
Example:
```git
t93kqi0@IAG-MAGUI-KQ10 MINGW64 ~/Documents/Projects/Agent-Screening (traditional)
$ git cherry -v master traditional
+ 8be0467d1597af1b26ef371c23cac74415f77b30 Add code\binning_efd.py to apply equally frequency discretization to train, test and validation data. The data have been created for 3 and 6 bins.
+ 12b990690912f11ae18cdb9bdc1f37caa9820079 Add documents\analysis-traditional-economentric-approach-v01.xls with the variables inlcuded in the traditional approach.
+ 8e6723af883136261914acdcd36c3145edc4c463 Add code\pipeline-01.py with the corresponding data
+ 3439e2de2a2a98caf7c3afc525552062ec774b3e Add code\pipeline-01.py with the corresponding data
+ 80e80a3b78ad9fff8ff7082e2e5a863c4d8de271 Add code\pipeline-03.py and all corresponding data
+ 796f882c018b5a218d00c50de8cd24f4961b125d Add code\pipeline-03.py and all corresponding data
+ 0d423c6deeb87f28c41f6e1639ccfe3b69adfbaf Add code\pipeline-05.py with remaining and corresponding data
```
This would show all of the commits which are contained within  _traditional_, but NOT in  _master_. If you leave off the last option (_traditional_), it will compare the current branch instead.

You are ALWAYS comparing your branch to another branch, so know your branches and then choose which one to compare to.

The log is listed in chronological order. 

Another way using:

```git
$ git log --graph traditional
```
Example:
```git
t93kqi0@IAG-MAGUI-KQ10 MINGW64 ~/Documents/Projects/Agent-Screening (traditional)
$ git log --graph traditional
* commit 0d423c6deeb87f28c41f6e1639ccfe3b69adfbaf (HEAD -> traditional, origin/traditional)
| Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| Date:   Sun Sep 15 17:52:13 2019 -0400
|
|     Add code\pipeline-05.py with remaining and corresponding data
|
*   commit 1fc98a3ce47fd56020a4b9d620d43b06ea8ebfd8
|\  Merge: 796f882 80e80a3

| | Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| | Date:   Sun Sep 15 17:49:13 2019 -0400
| |
| |     Merge branch 'traditional' of nylgit.newyorklife.com:CDSA/Agent-Screening into traditional
| |
| * commit 80e80a3b78ad9fff8ff7082e2e5a863c4d8de271
| | Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| | Date:   Sun Sep 15 17:47:07 2019 -0400
| |
| |     Add code\pipeline-03.py and all corresponding data
| |
* | commit 796f882c018b5a218d00c50de8cd24f4961b125d
|/  Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
|   Date:   Sun Sep 15 17:48:44 2019 -0400
|
|       Add code\pipeline-03.py and all corresponding data
|
*   commit 618382c12aa72867c2694aa3f56ae08c2c45ba9e
* *   commit 618382c12aa72867c2694aa3f56ae08c2c45ba9e
|\  Merge: 3439e2d 8e6723a
| | Author: Marcos <marcos_aguilerakeyser@newyorklife.com>

| | Date:   Sun Sep 15 17:45:59 2019 -0400
| |
| |     Merge branch 'traditional' of nylgit.newyorklife.com:CDSA/Agent-Screening into traditional
| |
| * commit 8e6723af883136261914acdcd36c3145edc4c463
| | Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| | Date:   Sun Sep 15 17:40:02 2019 -0400
| |
| |     Add code\pipeline-01.py with the corresponding data
| |
* | commit 3439e2de2a2a98caf7c3afc525552062ec774b3e
|/  Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
|   Date:   Sun Sep 15 17:40:47 2019 -0400
|
|       Add code\pipeline-01.py with the corresponding data
|
* commit 12b990690912f11ae18cdb9bdc1f37caa9820079
| Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| Date:   Sun Sep 15 17:38:40 2019 -0400
|
|     Add documents\analysis-traditional-economentric-approach-v01.xls with the variables inlcuded in the traditional approach.
|
* commit 8be0467d1597af1b26ef371c23cac74415f77b30
| Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| Date:   Wed Sep 11 10:17:23 2019 -0400
|
|     Add code\binning_efd.py to apply equally frequency discretization to train, test and validation data. The data have been created for 3 and 6 bins.
|
* commit 3be7aa49aa51a0314a2efd059167bf7befe6cf41 (origin/master, master)
* | Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
| Date:   Mon Sep 9 14:30:54 2019 -0400
|
|     Update code\binning_decision_trees_data_2.py and master_validate\bootstrapped_validation_Binned.csv Updated code to include the binned version fo the validation dataset for model assesment.
|
* commit 75684932b31b3aba7d5494f8e37ad9cc8e113393
| Author: Marcos <marcos_aguilerakeyser@newyorklife.com>
```










<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM4ODg4MzUyMywxMDI4NzMwNDk4LC0xMD
E3NjgzNDkzLDE3MzYxMDQwNjgsMjAxOTI3OTM4NiwyMDE5Mjc5
Mzg2LDE2MDE4MTY5NzEsLTEzMDIxNTI2NTAsLTE5MjU3MDg0Nj
AsLTEwNTEzMjU3NDcsMjA0MDI2NzYwOSwyNDI2ODk3MzNdfQ==

-->