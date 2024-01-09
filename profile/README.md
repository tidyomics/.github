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

* [Key Tidyomics Packages](#key-tidyomics-packages) and their documentation
* [Tutorials](#tutorials)
* [Join the Conversation](#join-the-conversation)
* [Get Involved](#get-involved)

## Key Tidyomics Packages

* tidybulk
    - test
* tidySummarizedExperiment
    - test
* tidySingleCellExperiment
    - test
* tidySeurat
    - test
* tidySpatialExperiment
    - test
* tidytof
    - test
* plyranges
    - test
* nullranges
    - test

## Tutorials

* Working with genomic range data: [Tidy ranges tutorial](https://tidyomics.github.io/tidy-ranges-tutorial/)
* Working with single cell data: [Tidy single-cell analyses workshop](https://tidyomics.github.io/tidyomicsWorkshopBioc2023/articles/tidyGenomicsTranscriptomics.html)
* Working with bulk RNA-seq: [Comparison of tidybulk with Bioconductor packages](https://stemangiola.github.io/tidybulk/articles/comparison_with_base_R.html)
* Working with Seurat objects: [Overview of the tidyseurat package](https://stemangiola.github.io/tidyseurat/articles/introduction.html)
* Working with cytometry data: [Overview of the tidytof package](https://keyes-timothy.github.io/tidytof/articles/tidytof.html)
* ...more to come!

For more description on the transcriptomics side of tidyomics, see:

* [Tidy transcriptomics manifesto](https://tidyomics.github.io/tidyomicsBlog/post/2021-07-07-tidy-transcriptomics-manifesto/)

## Join the Conversation

We value community feedback and collaboration. Join the ongoing
discussion and contribute to the evolution of the tidyomics
ecosystem.

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
