


> Written with [StackEdit](https://stackedit.io/).

# Working Collaboratively with Branches

To be a successful member of a data science team, you will need to be able to effectively collaborate with others. While this is true for nearly any practice, an additional challenge for collaborative data science is working on shared code for the same project. Many of the techniques for supporting collaborative coding involve writing clear, well-documented code that can be read, understood, and modified by others. But you will also need to be able to effectively _integrate_ your code with code written by others, avoiding any “copy-and-pasting” work for collaboration. The best way to do this is to use a version control system. Indeed, one of the biggest benefits of `git` is its ability to support **collaboration** (working with other people). In this chapter, you will expand your version control skills to maintain different versions of the same code base using `git`’s **branching model**, and familiarize yourself with two different models for collaborative development.

1. TRACKING DIFFERENT VERSIONS OF CODE WITH BRANCHES 

To work effectively with others, you need to understand how  `git`  supports nonlinear development on a project through branches. A  **branch**  in  `git`  is a way of labeling a  _sequence of commits_. You can create labeled commit sequences (branches) that exist side by side within the same project, allowing you to effectively have different “lines” of development occurring in parallel and diverging from each other. That is, you can use  `git`  to track multiple different, diverging versions of your code, allowing you to work on multiple versions at the same time.

At this point you know how to use  `git`  when you are working on a single branch (called  `master`) using a  _linear sequence_  of commits. As an example,  Figure.1  illustrates a series of commits for a sample project history. Each one of these commits—identified by its  **hash**  (e.g.,  `e6cfd89`  in short form)—follows sequentially from the previous commit. Each commit builds directly on the other; you would move back and forth through the history in a straight line. This linear sequence represents a workflow using a  _single line of development_. Having a single line of development is a great start for a work process, as it allows you to track changes and revert to earlier versions of your work.

[fig01]

**Figure 1**: A diagram of a linear sequence of commits alongside a log of the commit history as shown in the terminal. This project has a single history of commits (i.e., _branch_), each represented by a six-character _commit hash_. The `HEAD`—most recent commit—is on the `master` branch.

In addition to supporting single development lines, `git` supports a _nonlinear model_ in which you “branch off” from a particular line of development to create new concurrent change histories. You can think of these as “alternate timelines,” which are used for developing different features or fixing bugs. For example, suppose you want to develop a new visualization for your project, but you’re unsure if it will look good and be incorporated. You don’t want to pollute the primary line of development (the “main work”) with experimental code, so instead you _branch off_ from the line of development to work on this code at the same time as the rest of the core work. You are able to commit iterative changes to both the experimental visualization branch and the main development line, as shown in Figure 2. If you eventually decide that the code from the experimental branch is worth keeping, you can easily _merge_ it back into the main development line as if it were created there from the start!

[fig02]
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4MjczNjU4NCwtMTQ4NDI1MzM5MiwyMD
gyNTA3NzU4XX0=
-->