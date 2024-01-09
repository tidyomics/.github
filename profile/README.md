## Get Started

**tidyomics** is an open project to develop and integrate software and
documentation to enable a
[tidy data](https://vita.had.co.nz/papers/tidy-data.pdf)
analysis framework for omics data objects.
tidyomics allows use of familiar 
[tidyverse](https://dplyr.tidyverse.org/) verbs
(`select`, `filter`, `mutate`, etc.) to manipulate
rich data objects in the 
[Bioconductor](https://bioconductor.org) ecosystem.
Importantly, the data objects are not modified, but tidyomics provides
a tidy *interface* to work on the native objects, leveraging existing
Bioconductor classes and algorithms.

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
chip_seq_peaks %>%
  filter(FDR < 0.01) %>%
  mutate(n_olap = count_overlaps(., promoters),
         any_pro_olap = n_olap > 0) %>%
  group_by(any_pro_olap) %>%
  summarize(ave_score = mean(score))
```

(compute average score by promoter overlap for significant peaks)

---

Below find links to:

* [Key Tidyomics Packages](#key-tidyomics-packages)
* [Tutorials](#tutorials)
* [Getting Help](#getting-help)
* [Get Involved](#get-involved)

## Key Tidyomics Packages

| packages | intro | GitHub | description |
|---|---|---|---|
| [tidybulk](https://stemangiola.github.io/tidybulk/) | [vignette](https://stemangiola.github.io/tidybulk/articles/introduction.html) | [GitHub](https://github.com/stemangiola/tidybulk/) | bulk RNA-seq tasks |
| [tidySummarizedExperiment]() | [vignette]() | [GitHub]() | |
| [tidySingleCellExperiment]() | [vignette]() | [GitHub]() | |
| [tidySeurat]() | [vignette]() | [GitHub]() | |
| [tidySpatialExperiment]() | [vignette]() | [GitHub]() | |
| [tidytof]() | [vignette]() | [GitHub]() | |
| [plyranges](https://sa-lee.github.io/plyranges/) | [vignette](https://sa-lee.github.io/plyranges/articles/an-introduction.html) | [GitHub](https://github.com/sa-lee/plyranges) | manipulation of genomics ranges |
| [plyinteractions](https://tidyomics.github.io/plyinteractions/) | [vignette](https://tidyomics.github.io/plyinteractions/articles/plyinteractions.html) | [GitHub](https://github.com/tidyomics/plyinteractions) | manipulation of genomic interactions |
| [nullranges](https://nullranges.github.io/nullranges/) | [vignette](https://nullranges.github.io/nullranges/articles/nullranges.html) | [GitHub](https://github.com/nullranges/nullranges/) | generation of null genomic range sets | 

Note that many of these packages have more than one vignette, which
you can find by navigating the package main page.

## Tutorials

* Various genomic range manipulation tasks: [Tidy ranges tutorial](https://tidyomics.github.io/tidy-ranges-tutorial/)
* Single cell transcriptomics and genomics: [Tidy single-cell analyses](https://tidyomics.github.io/tidyomicsWorkshopBioc2023/articles/tidyGenomicsTranscriptomics.html)
* ...more to come!

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
