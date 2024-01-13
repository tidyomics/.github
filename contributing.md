# Contributing to `tidyomics`

## Making contributions to existing tidyomics packages

1. Check the [open challenges page](https://github.com/orgs/tidyomics/projects/1), 
   or ask one of the community members about adding a new open
   challenge
2. Reach out to a package developer, either through a GitHub Issue, or
   on the Bioconductor community Slack, `#tidiness_in_bioc` channel
3. Discuss building a pull request, or developing a stand-alone
   package, with current members of the 
   [tidyomics development team](https://github.com/orgs/tidyomics/people)

Alternatively, you may have an idea for a new package to cover an area
not covered by existing packages. You can also reach out to discuss
with any of the members on Slack or our GitHub project space.

## Brief overview of what makes a tidyomics package

The goal of the tidyomics packages is not to re-implement tidy or
Bioconductor functionality, nor to create new classes to replace
Bioconductor classes. All of the tidyomics packages leverage existing
functions and classes, and simply provide an interface (an API)
between tidy verbs and Bioconductor objects.

An example is *tidySummarizedExperiment*, which does not re-implement
or change the class of SummarizedExperiment objects, but instead
provides a *tibble* abstraction of the object, which can be
manipulated as if the SummarizedExperiment were in a tidy format. The
underlying SummarizedExperiment maintains its class (unless there is a
summarization operation for example) and can be operated on with
existing Bioconductor methods as usual.

## Tidyomics in scripts vs in package development

We are planning to develop more tutorials and instructional material
on deciding between using tidyomics in scripts vs using tidyomics
throughout package code. One consideration is compute speed, where
certain matrix operations have highly optimized functions, e.g. the
operations available in `matrixStats`. For repetitive tasks within the
source code of a Bioconductor package, it may make more sense to use
`rowMeans` or the like, rather than, say,
`group_by(row) |> summarize(mean = mean(counts))`. 

Typically in scripts, readability and extensibility is much more
important than the speed of individual operations. In addition, for
most analyses, the speed of tidyomics is equivalent to base
R/Bioconductor (see tidyomics paper for speed comparisons).
 
Note that a tidyomics package need not make use of pipes or
non-standard evaluation in its own source code, while it certainly
would make use of these paradigms in its vignettes and examples. Feel
free to post to the `#tidiness_in_bioc` channel on the Bioconductor
community Slack if you want more guidance on this point.
