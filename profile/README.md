## Get Started

The main idea is to allow biologists to use familiar 
[tidyverse](https://dplyr.tidyverse.org/)
commands with rich biological datasets in the 
[Bioconductor](https://bioconductor.org)
ecosystem and beyond. 
This means being able to do things like:

```{r}
single_cell_data |>
  filter(Phase == "G1") |>
  ggplot(aes(UMAP_1, UMAP_2, color=score)) + 
  geom_point()
```

or

```{r}
chip_seq_peaks |>
  filter(FDR < 0.01) |>
  group_by(promoter_overlap) |>
  summarize(ave_score = mean(score))
```

While Bioconductor objects are not all natively in
[tidy data](https://vita.had.co.nz/papers/tidy-data.pdf)
formar, `tidyomics` packages provide interfaces that allow users to
operate on them as if they were, in a way that the original
Bioconductor objects and methods are preserved.

To get more examples of what `tidyomics` means, and what packages are
involved, here are some getting started material and tutorials:

* [Tidy transcriptomics manifesto](https://tidyomics.github.io/tidyomicsBlog/post/2021-07-07-tidy-transcriptomics-manifesto/)
* [Tidy ranges tutorial](https://tidyomics.github.io/tidy-ranges-tutorial/)
* ...

You might also check out recent workshops:

* [Tidy genomic and transcriptomic single-cell analyses at BioC2023](https://tidyomics.github.io/tidyomicsWorkshopBioc2023/articles/tidyGenomicsTranscriptomics.html)
* ...

## Join the Conversation

We value community feedback and collaboration. Join the ongoing
discussion and contribute to the evolution of the `tidyomics`
ecosystem.

[Join our Slack Channel - #tidiness_in_bioc](https://slack.bioconductor.org)

## Looking to get involved? 

* See our [tidyomics open challenges](https://github.com/orgs/tidyomics/projects/1)
  project to see what we are currently working on
* [Guidelines for contributing](contributing.md)
* [Code of Conduct](CODE_OF_CONDUCT.md)
