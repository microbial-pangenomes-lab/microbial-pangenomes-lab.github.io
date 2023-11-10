---
title: Multiple haystacks are better than one
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

Just a couple of days ago [we have published a research article](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.001129) describing
[panfeed](https://github.com/microbial-pangenomes-lab/panfeed), a software tool
to aid bacterial GWAS studies. This effort was
led by [Hannes]({{ site.url }}/members/#hsommer), with the help of [Dilfuza]({{ site.url }}/members/#ddjamalova)
during peer review.

As everyone in the field of genomics has heard _ad nauseam_, we now have an abundance of
genome sequences available; when that is combined with phenotypic measurements the obvious
question is then "which gene is responsible for this phenotype?". Statistical genetics (_i.e._
genome-wide association studies, GWAS) would be one way to answer that question, or rather
the more correct one "which genetic variant is associated, and hopefully causal, for the
variation in phenotype, across this collection of genomes?".

When asking this question in the context of bacterial genomes, the term "genetic variant"
can take a number of meanings, going from "classical" short variants such
as SNPs/InDels, to entire operons being transferred horizontally and even [genes changing
their arrangement](https://gtonkinhill.github.io/panaroo/#/post/sv). One clever way to
encode all these variant types is to use a _k_-mer, which is a DNA "word" of length _k_
([typically 31](https://threadreaderapp.com/thread/1488348684169404418.html)).

While this solution allows one to collapse different genetic variant types into a unified
data structure, it generates two problems: one of ambiguity and one of interpretability.
These are the problems that we aim to ameliorate (hopefully solve for most people!) with panfeed.
Let's go over both problems then.

Greatly simplyfing, one way to generate _k_-mers from a set of genomes is to take the input genomes
and put them into a blender that chops them into _k_-mers. The output can be then seen as a big haystack
from which we have to find the proverbial needle (the causal variants). The problem is that some genes
(which in bacterial genomes are pretty much the main unit of molecular function) will share some _k_-mers,
which will then implicate unrelated genes with the focal phenotype (as well as subtly modifying the presence/absence patterns
of those shared _k_-mers, affecting the association results themselves). That's the ambiguity problem that needs to be solved;
using data from 21 bacterial species' genomes we indeed show how on average 3% of _k_-mers are duplicated across genes
and how 13% of genes have at least one _k_-mer shared with at least another gene.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20231109_figure_2.jpg" alt="Plot with the proportion of duplicated k-mers across 21 pangenomes">

The problem of interpretability also stems from all genetic variants being in a big haystack: once you have found your needle,
how do you figure out 1) which gene it might belong to, and 2) which variant type it encodes?
You can surely map the _k_-mers back to the input genomes, but you would lack the local context, meaning which other
genetic variants are present in that genomic location across all the genomes in the sample.

We address both problems by leveraging the assumption that genes are the unit of function in bacterial genomes and what
most people will use to interpret results. So basically instead of having a single haystack, we generate many (tens of thousands in fact!)
smaller ones and search for a needle in each of them. To be more specific, we use the gene cluster definitions given by tools
such as [panaroo](https://gtonkinhill.github.io/panaroo/#/) and [ggCaller](https://ggcaller.readthedocs.io/en/latest/)
and extract _k_-mers and their presence/absence patterns from each gene cluster separately.
This means that a _k_-mer that is duplicated across gene clusters is allowed to have a different presence/absence pattern for each gene,
thus reducing false gene leads.
Interpretation is improved by linking _k_-mers and their source gene directly, as well as showing the local context of the associated variants,
which can optionally include promoter regions, as shown below.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20231109_figure_4.jpg" alt="An example of panfeeds visualization to improve interpretability">

panfeed is available as a conda package in [bioconda](https://anaconda.org/bioconda/panfeed) (`mamba create -c bioconda -n panfeed panfeed`),
as a [pypi package](https://pypi.org/project/panfeed/) (`python3 -m pip install panfeed`),
and its [source code and issue tracker can be accessed in our lab's github](https://github.com/microbial-pangenomes-lab/panfeed). Happy needle search!
