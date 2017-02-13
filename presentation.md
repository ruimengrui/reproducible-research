---
title: Adopting open source practices for better science
output:
  xaringan::moon_reader
---

# Adopting open source practices for better science
Pierce Edmiston  
<pedmiston@wisc.edu>  
Lupyan Lab, [sapir.psych.wisc.edu](http://sapir.psych.wisc.edu/)  
[github.com/pedmiston](https://github.com/pedmiston)




---
# Outline

Open source practices that make for more reproducible science:

1. Version control
2. Dynamic documents
3. Building from source

Conclusion: It's worth it!

---
# Why I care about reproducible research

- [Open Science Collaboration. 2015. Estimating the reproducibility of psychological science. _Science_.](http://science.sciencemag.org/content/349/6251/aac4716)
- [Palmeri, K. 2016. Psychology is in crisis over whether it's in crisis. _WIRED_.](https://www.wired.com/2016/03/psychology-crisis-whether-crisis/)
- [Ioannidis, J. 2005. Why most published research findings are false. _PLOS Medicine_](http://dx.doi.org/10.1371/journal.pmed.0020124)

<aside class="notes">
</aside>

---
# Why open source is the answer

> My collaborators should be able to reproduce my research.  
> Anyone should be able to use and contribute to this project.

---
# 1. Version control

---
## Examples

<div class="figure">
<img src="presentation_files/figure-html/unnamed-chunk-2-1.png" alt="Version control in the wild." width="1152" />
<p class="caption">Version control in the wild.</p>
</div>

---
## Tools for climbing

<img src="presentation_files/figure-html/unnamed-chunk-3-1.png" width="672" />

---
## Pick your poison

- **git**
- mercurial
- subversion

<aside class="notes">
My requirements for choosing version control system are that it is **open source** and supports **distributed** collaboration and merge operations, which most modern VCSs do.
</aside>

---
## Forks and branches

<!--html_preserve--><div id="htmlwidget-831d45d03e34844f64c5" style="width:672px;height:200px;" class="grViz html-widget"></div>
<script type="application/json" data-for="htmlwidget-831d45d03e34844f64c5">{"x":{"diagram":"\ndigraph {\n  rankdir = LR;\n  node[label = \"\"];\n  m0 -> m1 -> m2 -> m3;\n  b0, b1[style = invis];\n  b0 -> b1 -> b2[style = invis];\n  b2 -> b3;\n  m1 -> b2[constraint = false];\n}","config":{"engine":"dot","options":null}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---
## Submodules

<aside class="notes">
One neat thing you can do with `git` (and likely other VCS but I don't know for sure) is link projects within other projects as "submodules". Version controlled projects are called "repos", and submodules are repos within repos.

Imagine I have two separate research projects, each with its own repo. Now I'm giving a presentation and I want to talk about results from both of those projects. Or I'm submitting some of the preliminary results from these research projects to a conference or journal. Rather than copying over the results from each research project into the new presentation, you could just include the research project as a submodule. This would basically link the research project at a particular time to the presentation being given or manuscript being submitted.
</aside>

    talk or pub/
    ├── research_project_1
    └── research_project_2

<aside class="notes">
I should warn you that submodules are a bit clunky and I don't think that most people in the open source community advocate too much for using them. But as a tool used carefully it allows for the formal linking of different kinds of repos.

Here's a different use-case for submodules, one that I don't think people are doing, but one that would be very interesting to see take off. Here the root project is a meta-analysis of many different research projects. Even if all the research projects contained was plain text data files of the results of the research project (and some accompanying documentation) this could be an extraordinarily effective way of facilitating meta-analytic analysis.
</aside>

    meta-analysis/
    ├── research_project_1
    ├── ...
    └── research_project_n

<aside class="notes">
The final use case is one that I actually use, and it's a case where a research project just gets really complicated and has multiple parts, and it helps to break off different parts to be their own submodules.
</aside>

    project/
    ├── *web-app*  -> also installed on web server
    ├── *psychopy* -> also installed on lab computers
    ├── *r-pkg*    -> installed by anyone who wants the data
    ├── conference
    └── journal

---
# Dynamic documents

---
## Don't Repeat Yourself (DRY)

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system (Hunt & Thomas, 1999, [_The pragmatic programmer_](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)).

---
## Literate programming (LP)

Knuth, Donald E. (1983). [Literate programming](https://en.wikipedia.org/wiki/Literate_programming).

* Intermingle prose and code for better understanding of the program.
* The explanation of a program does not need to resemble the program structure.

---
## Sphinx

Examples:

* Python standard library: [json](https://docs.python.org/3/library/json.html)
* Third party package: [requests](http://docs.python-requests.org/en/master/api/#requests.request)

---
## Knitr

Evergreen statistics:

Participants in condition A outperformed participants in condition B, `report_model_results(mod, param = "condition")`.

Reproducible plots:
    
&#96``{r, eval=FALSE, literal=TRUE}
plot(df)
&#96``

---
# Building from source