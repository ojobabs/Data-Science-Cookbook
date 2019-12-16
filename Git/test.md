


> Written with [StackEdit](https://stackedit.io/).

# Working Collaboratively with Branches

To be a successful member of a data science team, you will need to be able to effectively collaborate with others. While this is true for nearly any practice, an additional challenge for collaborative data science is working on shared code for the same project. Many of the techniques for supporting collaborative coding involve writing clear, well-documented code that can be read, understood, and modified by others. But you will also need to be able to effectively _integrate_ your code with code written by others, avoiding any “copy-and-pasting” work for collaboration. The best way to do this is to use a version control system. Indeed, one of the biggest benefits of `git` is its ability to support **collaboration** (working with other people). In this chapter, you will expand your version control skills to maintain different versions of the same code base using `git`’s **branching model**, and familiarize yourself with two different models for collaborative development.

1. TRACKING DIFFERENT VERSIONS OF CODE WITH BRANCHES 

To work effectively with others, you need to understand how  `git`  supports nonlinear development on a project through branches. A  **branch**  in  `git`  is a way of labeling a  _sequence of commits_. You can create labeled commit sequences (branches) that exist side by side within the same project, allowing you to effectively have different “lines” of development occurring in parallel and diverging from each other. That is, you can use  `git`  to track multiple different, diverging versions of your code, allowing you to work on multiple versions at the same time.

[Chapter 3](https://learning.oreilly.com/library/view/Programming+Skills+for+Data+Science:+Start+Writing+Code+to+Wrangle,+Analyze,+and+Visualize+Data+with+R,+First+Edition/9780135159071/ch03.xhtml#ch03)  describes how to use  `git`  when you are working on a single branch (called  `master`) using a  _linear sequence_  of commits. As an example,  [Figure 20.1](https://learning.oreilly.com/library/view/Programming+Skills+for+Data+Science:+Start+Writing+Code+to+Wrangle,+Analyze,+and+Visualize+Data+with+R,+First+Edition/9780135159071/ch20.xhtml#fig20_1)  illustrates a series of commits for a sample project history. Each one of these commits—identified by its  **hash**  (e.g.,  `e6cfd89`  in short form)—follows sequentially from the previous commit. Each commit builds directly on the other; you would move back and forth through the history in a straight line. This linear sequence represents a workflow using a  _single line of development_. Having a single line of development is a great start for a work process, as it allows you to track changes and revert to earlier versions of your work.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA4MjUwNzc1OF19
-->