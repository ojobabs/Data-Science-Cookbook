> Written with [StackEdit](https://stackedit.io/).

## Bash Commands

### [how do I add the 'tree' command to git-bash on Windows?](https://superuser.com/questions/531592/how-do-i-add-the-tree-command-to-git-bash-on-windows)

On the Atom or Git Bash consoles (that are using Bash) write:

```bash
$ cmd
```
To move to the `cmd` console within the Atom or Git Bash consoles.  The write:

```bash
tree
```
And the output is:
```bash
├───code
│   └───.ipynb_checkpoints
└───data
    └───csem71
```
Finally, to come back to the Atom / Git Bash consoles:
```bash
$ exit
```
> Note: the `tree`command is not part of [Chocolatey](https://chocolatey.org/). You can find the `tree` command as part of Bash but not in Chocolatey.  Of course, the tree command exist for `cmd`.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUzODUwMDA3OSwxMTg2MTQ5MDI3LC0xOT
Y5OTI4NDU5XX0=
-->