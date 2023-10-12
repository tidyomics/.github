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
chip_seq_peaks %>%
  filter(FDR < 0.01) %>%
  mutate(n_olap = count_overlaps(., promoters),
         any_pro_olap = n_olap > 1) %>%
  group_by(any_pro_olap) %>%
  summarize(ave_score = mean(score))
```

While Bioconductor objects are not all natively in
[tidy data](https://vita.had.co.nz/papers/tidy-data.pdf)
format, `tidyomics` packages provide interfaces that allow users to
operate on them as if they were, in a way that the original
Bioconductor objects and methods are preserved.

## Tutorials

* Working with genomic range data: [Tidy ranges tutorial](https://tidyomics.github.io/tidy-ranges-tutorial/)
* Working with single cell data: [Tidy single-cell analyses workshop](https://tidyomics.github.io/tidyomicsWorkshopBioc2023/articles/tidyGenomicsTranscriptomics.html)
* Working with bulk RNA-seq: [Comparison of tidybulk with Bioconductor packages](https://stemangiola.github.io/tidybulk/articles/comparison_with_base_R.html)
* Working with Seurat objects: [Overview of the tidyseurat package](https://stemangiola.github.io/tidyseurat/articles/introduction.html)
* ...more to come!

For more description on the transcriptomics side of tidyomics, see:

* [Tidy transcriptomics manifesto](https://tidyomics.github.io/tidyomicsBlog/post/2021-07-07-tidy-transcriptomics-manifesto/)

## Join the Conversation

We value community feedback and collaboration. Join the ongoing
discussion and contribute to the evolution of the `tidyomics`
ecosystem.

* Join our Slack Channel, [#tidiness_in_bioc](https://slack.bioconductor.org)
* For help you can reach out on the [Bioconductor support site](https://support.bioconductor.org)

## Looking to get involved? 

The `tidyomics` organization is open to contributions; it is an effort
of many developers in the Bioconductor community and beyond.

* See our [tidyomics open challenges](https://github.com/orgs/tidyomics/projects/1)
  project to see what we are currently working on
* [Guidelines for contributing](contributing.md)
* [Code of Conduct](CODE_OF_CONDUCT.md)
