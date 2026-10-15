---
title: A (glowing) family in a bottle
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

We have [just posted a new preprint, describing the development of an experimental system to study horizontal gene transfer (HGT) of antimicrobial resistance (AMR) in the lab](https://www.biorxiv.org/content/10.64898/2026.10.13.758845v1).
This work was led almost completely by [Hien]({{ site.url }}/members/#hvuthu), with some help from colleagues in [our department](https://twincore.de/people/dr-camille-andrieu), from the [Max Planck Institute for Terrestrial Microbiology and Center for Synthetic Microbiology](https://www.mpi-marburg.mpg.de/1492924/LeanidLaganenka), and [from my *alma mater* (the University of Florence)](https://www.bio.unifi.it/p162.html).

*In-vitro* laboratory evolution has proven to be a valuable tool to investigate how AMR emerges and which genes are involved.
The vast majority of studies have however focused on isolated "individuals" (*i.e.* single strains), which can only evolve
resistance through spontaneous mutations. This is in sharp contrast with what happens in the wild; most bacteria don't live in isolation,
but have a rather busy social life, sometimes even living in a "happy family" with each member benefitting from each other.
As part of this social life sometimes genetic material, including AMR genes, can be exchanged between individuals.
In order to better understand this process of HGT, we wanted to develop an experimental system that recapitulated
a "family" of bacteria, growing happily together and surviving antibiotic treatment by sharing AMR genes.

Armed with just a high-level plan I gave her, Hien got very busy and essentially single-handedly built both the "happy family"
and the "home" in which it could live. We decided to use genetic engineering to build a bacterial community (called TriComm) composed
of the same base strain (*E. coli* BW25113), each with a metabolic "Achilles heel" that made it dependent on the other members to
survive. In order to be able to distinguish each member of TriComm, we introduced a fluorescent marker in the two most important
family members. We then used [the Chi.Bio culturing device](https://chi.bio/) as TriComm's "home"; thanks to its detectors, we could follow the ups and downs
of the glowing family members in real time (with one measurement every minute!) and for extended periods of time (more than 40 days!).
We then planned to try to break the family apart by adding antibiotics, and equipping the weakest member of the family
with an AMR genes housed in a conjugative (*i.e.* transferrable) plasmid.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20261015_tricomm.png" alt="A schematic of the TriComm bacterial community and the plasmids we used">

As we expected, TriComm alone could not stand the antibiotic treatment, and quickly fell apart. But when we equipped it
with a mobilazible AMR gene, the family was able to carry along as if nothing had happened. Using a plasmid that was not able to
move between family members, we confirmed the old adage that "sharing is caring": TriComm's survival was predictated on every family
member to get its own cpy of the AMR gene.

Our experiments imply that targeting HGT could be a viable strategy to fight AMR; we teamed up with [my old colleagues
from the University of Florence](https://www.bio.unifi.it/p162.html) to develop a mathematical model with which we could explore changing drug pressure
and targeting the ability to share AMR genes, without having to run humdreds of experiments. The model suggests
that modulating the ability to share AMR genes could lead to breaking up the family, and thus potentially preventing
further spread of AMR genes. 

There's (much!) more to discover in the preprint and the accompanying code repositories ([1](https://github.com/microbial-pangenomes-lab/2026_tricomm)
and [2](https://github.com/microbial-pangenomes-lab/2026_tricomm_sequencing)),
so please dig in! But first, enjoy the photo of our glowing happy family, drawn by Hien herself.

<img class="img-fluid" src="{{ site.url }}/static/img/news/20261015_plates.jpg" alt="A photo of glowing agar art depicting TriComm">
