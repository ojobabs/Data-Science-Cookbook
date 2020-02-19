> Written with [StackEdit](https://stackedit.io/).

# Some Atom Resources

## Interesting packages

- [Finally, an IDE that does both Python and R well (Atom)](https://jstaf.github.io/2018/03/25/atom-ide.html). I used this article to install Python and R on my MacBook Pro. It works.
- [Using anaconda environment in Atom](https://stackoverflow.com/questions/43207427/using-anaconda-environment-in-atom)
- [How to uninstall Atom Windows (Step-by-step guide with screenshots)]([https://windowsreport.com/uninstall-atom-windows/](https://windowsreport.com/uninstall-atom-windows/))
The following YouTube video is fantastic. This is maybe the best reference for setting up a simple Python environment for Atom:
- [Setting up a Python Development Environment in Atom](https://www.youtube.com/watch?v=DjEuROpsvp4)
> The above training video mentions the following packages: **script**, **autocomplete_pytyon**, **file-icons**, **python-autopep8**,  First you need to install`pip install autopep8` on Anaconda and **linter-flake8**, here you need also `pip install flake8`. 

Other resources I used for the above steps:

- [atom-ide-r](https://github.com/REditorSupport/atom-ide-r)
- [Atom gitlab-integration package]()
- [Hydrogen](https://nteract.gitbooks.io/hydrogen/content/)
- [Hydrogen Reference](https://nteract.gitbooks.io/hydrogen/)
- [Hydrogen: Interactive computing in Atom](https://blog.nteract.io/hydrogen-interactive-computing-in-atom-89d291bcc4dd)
- [Cell Magic for Ipyhton](https://ipython.readthedocs.io/en/stable/interactive/magics.html)
- [Use Atom + Hydrogen!](https://acarril.github.io/posts/atom-hydrogen)
- [Atom gitlab-integration package](https://atom.io/packages/gitlab-integration)
- [# Question: How can one execute R code with hydrogen?](https://github.com/nteract/hydrogen/issues/881)
- [r-languageserver](https://anaconda.org/gwerbin/r-languageserver)
- [IDE-R package](https://atom.io/packages/ide-r)
- [languageserver](https://github.com/REditorSupport/languageserver)
- [knitr](https://github.com/yihui/knitr) I had to install this too
- I used Jupyter Lab to install `install.packages("languageserver")` and `install.packages('knitr', dependencies = TRUE)`. 
- [IDE-R package](https://atom.io/packages/ide-r)
- [R markdown](https://rmarkdown.rstudio.com/lesson-1.html)
- I installed `install.packages("rmarkdown")` using Jupyter Lab. I don't know if I really need this.
- [The current state of R support in Atom](https://haroldpimentel.wordpress.com/2016/11/28/the-current-state-of-r-support-in-atom/)
- [git-plus](https://atom.io/packages/git-plus)
- 

Issue about rendering Latex or Katex on Ipython on GitLab:

- https://gitlab.com/gitlab-org/gitlab-ce/issues/47350
- https://gitlab.com/magkey/test_project/blob/master/test_notebook.ipynb
- https://gitlab.com/gitlab-org/gitlab-ce/issues/37536
- https://stackoverflow.com/questions/11256433/how-to-show-math-equations-in-general-githubs-markdownnot-githubs-blog?rq=1


### Mermaid flowcharts with Atom

Packages:

- language-mermaid
- atom-merma
- markdown-preview-enhanced

With the above packages you can:
1. Write mermaid code in an `.mm` extension file. By using the language-mermaid package you can highlight the code. An by using the atom-mermaid package, you can render the content of the `.mm` file.
2. You can just write mermaid code in a markdown document. by using:


```mermaid
graph TD
``'


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxOTQ5MDMyMSwtMTQyODI3MTcxLC01OT
M3MzY2MTYsMjgzNzU2NjY2LDk1NzcwNTYyMiwtMTIzMzEyMTQ3
NywtMjcxODUxNTkzLC0xNjc4NjY4NDRdfQ==
-->