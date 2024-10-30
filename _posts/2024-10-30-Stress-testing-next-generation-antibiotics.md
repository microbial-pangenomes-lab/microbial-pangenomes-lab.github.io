---
title: Stress testing next-generation antibiotics 
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

_We have [just posted a new preprint describing some work we did in the area of
in-vitro laboratory evolution and next generation antibiotics](https://www.biorxiv.org/content/10.1101/2024.10.29.620885v1)! Here's a quick explainer
about what we (former postdoc [Adam]({{ site.url }}/2024/04/26/One-submission-and-one-farewell/), with help from
[Hien]({{ site.url }}/members/#hvuthu), and in collaboration with
[Jörg Vogel's group at the HIRI](https://www.helmholtz-hiri.de/en/research/organisation/people/person/prof-joerg-vogel/))_

By now, the general public is likely aware of the risks posed by infections from bugs that are
resistant to antibiotics. Whether we could surely argue if the widely circulated estimates
of [current](https://www.johnlees.me/posts/did-1-27m-people-die-from-amr-in-2019/) and
[future](https://journals.plos.org/plosmedicine/article?id=10.1371/journal.pmed.1002184) deaths caused by antimicrobial resistance are overblown, one thing is
certain: whenever a new antibiotic is introduced, [resistance will very quickly follow](https://journals.asm.org/doi/10.1128/mBio.01966-21).
Could there be a way to outpace evolution?

<img class="img-fluid" src="{{ site.url }}/static/img/news/20241030_abx.jpg" alt="Figure 1 from 10.1128/mBio.01966-21 demonstrating that resistance to antibiotics has always been discovered soon after they have been introduced">

A possible solution to this "arms race" is to develop an antibiotic
that can be quickly and easily updated to target resistant bugs.
An emerging solution is the development of so called antisense oligos (ASOs), which are
a short string of nucleotides (the "building blocks" of DNA) designed to 
very specifically block
key genes in the target bacteria.
Given their "lego" like nature, these ASOs are very easy to design, and more importantly
to be updated if the target sequence changes to escape the ASO's lethal effect.
An easy to understand parallel can be made with [covid mRNA vaccines](https://berthub.eu/articles/posts/reverse-engineering-source-code-of-the-biontech-pfizer-vaccine/), which are also based
on a (longer) string of nucleotides, and which
have been quickly updated as new variants have emerged.

But, as it is very frequently the case in biology, how organisms will adapt to
a new challenge is very difficult to predict
(["in the most carefully constructed experiment under the most carefully controlled conditions, the organism will do whatever it damn well pleases"](https://blog.codinghorror.com/the-organism-will-do-what-it-damn-well-pleases/)).
We therefore set to collect data using a realistic set of antimicrobial ASOs (for which we are using the new proposed term ["asobiotics"](https://www.helmholtz-hiri.de/en/newsroom/news/detail/news/focus-on-precision-antibacterials/))
and four nasty bacterial pathogens.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20241030_aso.jpg" alt="Figure 1a from our preprint showing the strains and asobiotics used, as well as the laboratory evolution protocol">

Given that an asobiotic needs a cell delivery component to reach the inside of a bacterial cell to exert its effect,
we hypothesized that we would see two classes of adaptive mutations being induced after treatment: one shutting the cell down
from the entry of the asobiotic, and one changing the target DNA sequence so that even if the asobiotic entered the cell
it would not have been able to bother its growth.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20241030_scheme.jpg" alt="A cartoon depicting the two kinds of mutations we expected to see and their impact on asobiotic resistance">

We indeed observed the two classes of mutations appearing (and the second class of mutations had never been reported before),
which confirms that in general bacteria
are very good at escaping whichever treatment we throw at them. But interestingly, which of the two kinds of
mutations would appear was heavily dependent on the nature of the cell delivery mechanism.
Given that cell delivery is harder to update than the "lego" like part, we propose that
particular care should be given to the choice of a delivery mechanism for which resistance
is induced at the lowest possible frequency. By following this simple advice and continuing in
improving this new class of antibiotics we are hoping to be able to eventually be able
to keep up with the evolution of antimicrobial resistance.
