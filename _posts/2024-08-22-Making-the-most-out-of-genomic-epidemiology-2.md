---
title: Making the most out of genomic epidemiology, one year on 
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

Believe it or not, exactly one year after [our preprint on predicting epistatic interactions in SARS-CoV-2](https://www.biorxiv.org/content/10.1101/2023.08.22.554253v1)
went online
we have [published a revised version in the journal Genome Biology](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-024-03355-y).
Talk about good timing!

[What we wrote one year ago]({{ site.url }}2023/08/23/Making-the-most-out-of-genomic-epidemiology/) is still a good primer on what epistatic interactions are
and why SARS-CoV-2 is a good test case for developing methods that are able to work
on large datasets.

What did we change with respect to the preprint? The main change is very obvious: we have six (6!) new authors,
which have contributed to run some experiments aimed at validating some of
the predicted interactions.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20240822_validation.jpg" alt="Figure 5 from the published paper with data from the experimental validations">

We decided to focus on interactions that had emerged after the March 2023 cutoff we had from the preprint,
as a way to have a relatively "blind" validation. Our colleagues from Twincore and HZI (with a special
mention to [Maureen](https://www.twincore.de/forschungsgruppen/institute/experimentelle-infektionsforschung/mitarbeiter/mitarbeiter-details/?tx_tcemployees_singleemployee%5Baction%5D=show&tx_tcemployees_singleemployee%5Bcontroller%5D=Employee&tx_tcemployees_singleemployee%5Bemployee%5D=526&cHash=c7dfb22d6bc2e53b04dbb65914c6257a) and [Henning](https://www.linkedin.com/in/henning-jacobsen-4052a9108/)!)
then built and tested pseudoviruses with the single and double mutations for their ability to infect
human cells and escape antibodies. We were able to validate all of our hand-picked interactions,
which is a good indication that our predictions are sound and that in theory the method we propose
could become part of the genomic epidemiology "arsenal".

Another addition of note is a visual representation of how our samples weighting method works,
which explains how we were able to identify the epistatic interaction that gave Omicron
its "super-powers" with as little as seven (7!) Omicron samples (the light orange dot below).

<img class="img-fluid" src="{{ site.url }}/static/img/news/20240822_weights.jpg" alt="Detail from supplementary figure 3 from the published paper demonstrating how the samples weighting strategy works">

Lastly, a couple of notes on the process of getting this paper published: given that the main author ([Gabriel](https://scholar.google.com/citations?user=2bfcQEgAAAAJ))
did not need to have this work published in the usual way for the benefit of his own career (he had already an offer for a graduate student position), we could experiment a bit more freely.
We decided to use [Review Commons](https://www.reviewcommons.org/) to solicit reviews in a journal-agnostic way. We got very stimulating comments
from two anonymous reviewers ([attached to the preprint](https://www.biorxiv.org/content/10.1101/2023.08.22.554253v1#review)); after we were done
replying to them we could pick where to submit the revised manuscript from a list of affiliated journals. I wish I could tell you which journals
are currently affiliated, but my google-fu came back empty-handed. I really liked the whole idea and process, and deciding which journal might be a good fit
after being done with the first round of peer review feels much easier. We are convinced that Genome Biology has the right readers for the main points
we tried to make. The only downside to the choice of journal would have been its steep [APC](https://en.wikipedia.org/wiki/Article_processing_charge) of 4290 Euros.
Luckily for us we did not have to directly cover this cost, as our institution participates in [Projekt DEAL](https://en.wikipedia.org/wiki/Project_DEAL), of which I only had a very vague idea about.
Not only did we use SARS-CoV-2 as a way to peek into the future of genomic epidemiology, but also in that of the research publishing system!
