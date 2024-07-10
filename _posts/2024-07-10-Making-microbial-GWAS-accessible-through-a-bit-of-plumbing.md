---
title: Making microbial GWAS accessible through a bit of plumbing
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

We have [just published a research preprint](https://www.biorxiv.org/content/10.1101/2024.07.08.602456v1) describing
[microGWAS](https://github.com/microbial-pangenomes-lab/microGWAS), a software pipeline
to facilitate microbial GWAS studies. This effort was
led by [Judit]({{ site.url }}/members/#jburgaya), [Bamu]({{ site.url }}/members/#bfufordamaris), and [Jenny]({{ site.url }}/members/#jfiebig),
who worked as a team to make my old chaotic code a "production-ready" tool.
It was a real pleasure to see this communal effort take shape!

<img class="img-fluid" src="{{ site.url }}/static/img/pub/burgaya_damaris_fiebig_2024.png" alt="microGWAS logo">

[What we wrote last time]({{ site.url }}2023/11/09/Multiple-haystacks-are-beter-than-one/) we published a method related to microbial GWAS remains a good
simple primer on the subject:

> As everyone in the field of genomics has heard _ad nauseam_, we now have an abundance of
genome sequences available; when that is combined with phenotypic measurements the obvious
question is then "which gene is responsible for this phenotype?". Statistical genetics (_i.e._
genome-wide association studies, GWAS) would be one way to answer that question, or rather
the more correct one "which genetic variant is associated, and hopefully causal, for the
variation in phenotype, across this collection of genomes?".

The complex nature of microbial genetic variability means that in practice one has to use
a number of software tools to preprocess genomes prior to the actual statistical association analysis.
These tools have each a number of quirks and informal best practices, and very often one needs to write
a small script to connect the output of one tool to the input of the next one in the so-called
"software pipeline". On top of these diffilcuties, very rarely the "raw" output of the association
analysis provides the information that user needs. Most commonly a user would want to know: 1)
which genes are associated with a given phenotype, and 2) is there a biological process that is
overrepresented in the gene list?

These are the problems that our pipeline hopes to solve! We used the popular [Snakemake workflow
management system](https://snakemake.readthedocs.io/) to connect each individual step of the typical end-to-end microbial GWAS
analysis, including a number of downstream analyses to provide the users with an annotated gene list.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20240710_pipeline.jpg" alt="Schematic representation of the pipeline steps">

As you can see from the simplified scheme above, the pipeline carries out all of the work needed to go from annotated genome assemblies and 
a phenotype table to annotated results and diagnostic plots. We even leverage Snakemake's support for [conda](https://docs.conda.io/en/latest/) to automate
the cumbersome (and frankly irritating) process of installing and insulating individual tools.

As we want to make this pipeline sustainable in medium term, we have also added a small test dataset to speed up
the developing process; we hope that young and eager researchers in the microbial bioinformatics community
will be interested in contributing to maintain the pipeline and implement new features.

More information about the four (4!) sets of genetic variants that are used in five (5!) distinct associations tests
can be found in the [preprint](https://www.biorxiv.org/content/10.1101/2024.07.08.602456v1), as well as in [the online documentation](https://microgwas.readthedocs.io).
