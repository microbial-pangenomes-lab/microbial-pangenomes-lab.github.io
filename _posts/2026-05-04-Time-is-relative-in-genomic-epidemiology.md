---
title: Time is relative in genomic epidemiology
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

We have [just posted a new preprint, describing our work on improving how to detect bacterial transmission in hospitals using genomics](https://www.medrxiv.org/content/10.64898/2026.04.27.26351816v1).
This effort was led by [Judit]({{ site.url }}/members/#jburgaya), who worked in collaboration with colleagues from
[Hannover Medical School](https://www.mh-hannover.de/) and [Copenhagen University Hospital-Rigshospitalet](https://www.rigshospitalet.dk/),
to use a large (~30k genomes!) bacterial genomics dataset that our collaborator [Susanne Häußler](https://www.helmholtz-hzi.de/personen/prof-dr-susanne-haeussler/)
has put together over the years.

Bacterial infections are a much too common "perk" for patients being hospitalized, and it's the job of
epidemiologists to identify the transmission routes for these pathogens. Often this problem boils down
to a relatively simple question: is this particular pair of bacterial samples related to each other? Genomics, used to
read all the millions of letters in the bug's DNA, provides the highest possible resolution
to answer this question. But how to choose the number of genetic differences ("SNPs") that separate related (i.e. the same bug moving between patients) from unrelated samples?

The standard practice in the field has relied on a fixed SNPs threshold (e.g. 20), which generally works, but has two problems:
it's rather arbitrary, but most importantly it does not take into account the impact of time. Since every time a bacterial cell
duplicates there is a chance that errors (i.e. SNPs) are introduced, then samples that are farther apart in time can
be expected to have more SNPs separating them. But how can we calibrate such a "SNPs accumulation clock"?
Judit had the brilliant intuition that in the dataset we had ~50 patients that had been sampled multiple times (~20!) over their hospital
stay. She could then calibrate our empirical clock within the same dataset we would use the clock for.
We hope that this approach will be taken up by genomic epidemiologists in their daily practice.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20260504_clock.jpg" alt="Schematic representation of how we calibrated a mutation accumulation clock">

Once we had used our calibrated clocks to identify transmitting bugs, we wanted to know if we could identify genetic
characteristics that could differentiate them from non-transmitting ones. We used two approaches to answer this question,
one using lists of known genes, and one looking at the whole ["haystack"]({{ site.url }}/2023/11/09/Multiple-haystacks-are-beter-than-one/).
Even though we could identify many genes and genetic variants associated with the ability to transmit between patients,
we failed to use them to predict which samples were part of a transmission chain in a held-out dataset. This suggests
that patient and environment factors might dominate the probability of bacterial transmission. Measuring and including
these factors in future analysis may then lead to a system that is better for predictions. 

<img class="img-fluid" src="{{ site.url }}/static/img/news/20260504_genes.jpg" alt="Differences in virulence and resistance scores between bacterial pathogens">

There's more to discover in the preprint and the [accompanying code repository](https://github.com/jburgaya/2025_genomics_transmission),
so please dig in!
