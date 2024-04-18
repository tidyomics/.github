## Get Started

**tidyomics** is an open project to develop and integrate software and
documentation to enable a
[tidy data](https://vita.had.co.nz/papers/tidy-data.pdf)
analysis framework for omics data objects.
tidyomics enables the use of familiar 
[tidyverse](https://dplyr.tidyverse.org/) verbs
(`select`, `filter`, `mutate`, etc.) to manipulate
rich data objects in the 
[Bioconductor](https://bioconductor.org) ecosystem.
Importantly, the data objects are not modified, but tidyomics provides
a tidy *interface* to work on the native objects, leveraging existing
Bioconductor classes and algorithms.

**tidyomics** is a set of R packages by an international group of
developers.

**tidyomics** allows for code such as the following:

```{r}
single_cell_data |>
  filter(Phase == "G1") |>
  ggplot(aes(UMAP_1, UMAP_2, color=score)) + 
  geom_point()
```

(filter single cells in G1 phase and plot UMAP coordinates)

or

```{r}
chip_seq_peaks |>
  filter(FDR < 0.01) |>
  join_overlap_inner(promoters) |>
  group_by(promoter_type) |>
  summarize(ave_score = mean(score))
```

(compute average score by the type of promoter overlap for significant peaks)

## Installer

Core tidyomics packages can be installed and loaded with the
*tidyomics* package. See the following URL for details and
instructions:

https://github.com/tidyomics/tidyomics

---

Below find links to:

* [Key Tidyomics Packages](#key-tidyomics-packages)
* [Comparison to base R](#comparison-to-base-r)
* [Tutorials](#tutorials)
* [News](#news)
* [Talks](#talks)
* [Tidyomics paper](#tidyomics-paper)
* [Getting Help](#getting-help)
* [Get Involved](#get-involved)

## Key Tidyomics Packages

| Package | Intro | GitHub | Description |
|---|---|---|---|
| [tidybulk](https://stemangiola.github.io/tidybulk/) | [Vignette](https://stemangiola.github.io/tidybulk/articles/introduction.html) | [GitHub](https://github.com/stemangiola/tidybulk/) | Tidy bulk RNA-seq data analysis |
| [tidySummarizedExperiment](https://stemangiola.github.io/tidySummarizedExperiment/) | [Vignette](https://stemangiola.github.io/tidySummarizedExperiment/articles/introduction.html) | [GitHub](https://github.com/stemangiola/tidySummarizedExperiment) | Tidy manipulation of SummarizedExperiment objects |
| [tidySingleCellExperiment](https://stemangiola.github.io/tidySingleCellExperiment) | [Vignette](https://stemangiola.github.io/tidySingleCellExperiment/articles/introduction.html) | [GitHub](https://github.com/stemangiola/tidySingleCellExperiment) | Tidy manipulation of SingleCellExperiment objects |
| [tidySeurat](https://stemangiola.github.io/tidyseurat/) | [Vignette](https://stemangiola.github.io/tidyseurat/articles/introduction.html) | [GitHub](https://github.com/stemangiola/tidyseurat) | Tidy manipulation of Seurat objects |
| [tidySpatialExperiment](https://william-hutchison.github.io/tidySpatialExperiment/) | [Vignette](https://william-hutchison.github.io/tidySpatialExperiment/articles/overview.html) | [GitHub](https://github.com/william-hutchison/tidySpatialExperiment) | Tidy manipulation of SpatialExperiment objects |
| [tidytof](https://keyes-timothy.github.io/tidytof) | [Vignette]() | [GitHub](https://github.com/keyes-timothy/tidytof) | Tidy manipulation of high-dimensional cytometry data |
| [plyranges](https://tidyomics.github.io/plyranges/) | [Vignette](https://tidyomics.github.io/plyranges/articles/an-introduction.html) | [GitHub](https://github.com/tidyomics/plyranges) | Tidy manipulation of genomics ranges |
| [plyinteractions](https://tidyomics.github.io/plyinteractions/) | [Vignette](https://tidyomics.github.io/plyinteractions/articles/plyinteractions.html) | [GitHub](https://github.com/tidyomics/plyinteractions) | Tidy manipulation of genomic interactions |
| [nullranges](https://nullranges.github.io/nullranges/) | [Vignette](https://nullranges.github.io/nullranges/articles/nullranges.html) | [GitHub](https://github.com/nullranges/nullranges/) | Generation of null genomic range sets | 

Consult each package homepage for a description of recent changes.

Note that many of these packages have more than one vignette, which
you can find by navigating the package main page.

## Comparison to base R

As the tidyomics packages offer an interface to underlying
R/Bioconductor function evaluations, operations carried out in
tidyomics can also be performed with base R/Bioconductor. The benefit
from the tidyomics approach is often in readability, interpretability,
and extensability of code, gained through elimination of temporary
variables, square bracket indexing (`[...,...]`) and control code
(e.g. `for`, `if`/`else`, `apply`/`sapply`, etc.).

For example, a filtering and grouping operation on a
SummarizedExperiment `data` in tidyomics would look like:

```{r}
data |>
  filter(score > 0) |>
  group_by(gene_class) |>
  summarize(mean_count = mean(counts))
```

In comparison, we can obtain the same with base R/Bioconductor, but
with more variables and some control code: 

```{r}
subdata <- data[rowData(data)$score > 0,]
gene_classes <- levels(rowData(subdata)$gene_class)
mean_count <- numeric(length(gene_classes))
for (i in seq_along(gene_classes)) {
  tmp_idx <- rowData(subdata)$gene_class == gene_classes[i]
  mean_count[i] <- mean(assay(subdata, "counts")[tmp_idx,])
}
```

This can be improved a bit if you know some more base R
functions. Here is a base R alternative making use of `subset` and
`aggregate`, h/t Martin Morgan:

```{r}
subdata <- subset(data, score > 0)
aggregate(
  as.vector(assay(subdata)),
  list(rep(rowData(subdata)$gene_class, ncol(subdata))),
  mean
)
```

Even still, the tidyomics version above (`filter`, `group_by`,
`summarize`) is likely the easiest to read and extend if the analyst
wants to do additional operations, and is the easiest to directly pipe
into a plot or a printed table.

For exploring this example, you can define `data` as follows:

```{r}
set.seed(5)
data <- SummarizedExperiment(
  assay=list(counts =
    matrix(rnorm(100),10,10, 
    dimnames=list(letters[1:10],letters[1:10]))
  ), 
  rowData = DataFrame(
    score=rnorm(10), 
    gene_class=factor(rep(1:3,c(3,3,4)))
  )
)
```

## Tutorials

* BioC workshop covering single cell transcriptomics and genomics: [Tidy single-cell analyses](https://tidyomics.github.io/tidyomicsWorkshopBioc2023/articles/tidyGenomicsTranscriptomics.html)
* Online book covering tidy manipulation of GRanges and more: [Tidy ranges tutorial](https://tidyomics.github.io/tidy-ranges-tutorial/)
* Quarto lecture notes introducing the concepts of tidyomics for expression and ranges: [Tidy intro talk](https://tidyomics.github.io/tidy-intro-talk)
* Short tutorial showing overlaps of GWAS SNPs with scATAC-seq peaks [T1D GWAS SNPs and CD4+ peaks](https://htmlpreview.github.io/?https://github.com/mikelove/cd4-overlaps/blob/main/CATlas/analysis.html)
* A workflow showing RNA-seq and ATAC-seq integration with plyranges: [Fluent genomics workflow](https://sa-lee.github.io/fluentGenomics/articles/fluentGenomics.html)
* More to come...

## News

* [Tidyomics blog](https://tidyomics.github.io/tidyomicsBlog/)

## Talks

* [Tidy enrichment analysis with plyranges and nullranges](https://github.com/tidyomics/tidy-genomics-talk/blob/main/tidy-enrichment.pdf)
* [Tidy analysis of genomic data](https://github.com/tidyomics/tidy-genomics-talk/blob/main/tidy-genomics-talk.pdf)

## Tidyomics paper

* [The tidyomics ecosystem: Enhancing omic data analyses](https://www.biorxiv.org/content/10.1101/2023.09.10.557072v2)

## Getting Help

We value community feedback and collaboration, and are happy to help
you get started. Join the ongoing discussion, or you can ask specific
questions about code on the support site.

* Join our Slack Channel,
  [#tidiness_in_bioc](https://slack.bioconductor.org) 
  for general discussion or pointers
* For specific coding help you can reach out on the 
  [Bioconductor support site](https://support.bioconductor.org) 

## Get Involved

<img src="tidyomics_community.png" alt="diagram of tidyomics community" align="right" width="350"/>

The tidyomics organization is open to new members and contributions;
it is an effort of 
[many developers](https://github.com/orgs/tidyomics/people) 
in the Bioconductor community and beyond.

* See our [tidyomics open challenges](https://github.com/orgs/tidyomics/projects/1)
  project to see what we are currently working on
* Issues tagged with 
  [good first issue](https://github.com/orgs/tidyomics/projects/1/views/1?filterQuery=good+first+issue)
  are those that developers think would be good for a new developer to
  start working on
* Read over our [Guidelines for contributing](contributing.md)
* Read over our [Code of Conduct](CODE_OF_CONDUCT.md)
* As with new users, for new developers please consider joining our
  Slack Channel,
  [#tidiness_in_bioc](https://slack.bioconductor.org).
  Most of the tidyomics developers are active there and we are happy
  to talk through updates, PRs, or give guidance on your development
  of a new package in this space.
