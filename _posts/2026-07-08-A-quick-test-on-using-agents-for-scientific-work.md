---
title: A quick test on using agents for scientific work
author: Marco Galardini
short: mgalardini
layout: post
group: news
---

I guess this post is as good a place as any to announce that I recently got tenure. The reason why this post
starts with a humble (?) brag is that it is customary in Germany to give an inaugural lecture (*Antrittsvorlesung*)
upon tenure. These lectures tend to be less scientific in nature, and so I decided to reflect on where computational
microbiology would be heading into the future. Obviously, it was not possible for me not to include a mention of AI,
especially given the acceleration driven by coding agents since the fall of 2025. It ended up being a bit of a [gloomy
outlook for young people looking to study computational biology](https://simonwillison.net/2026/Feb/15/deep-blue/);
what was once a sure path to a stable (?) career
is now under threat of being quickly automated.
[Anthropic's BioMysteryBench benchmark](https://www.anthropic.com/research/Evaluating-Claude-For-Bioinformatics-With-BioMysteryBench)
has shown how AI agents can solve complex bioinformatics tasks, and I like to show
skeptics [the plots on ARC-AGI's website](https://arcprize.org/leaderboard), which not only report how many tasks
are solved by AI, but also at which
*cost*, which is obviously a fraction of that of a human, hence the gloomy end of my inaugural lecture.

Let's however imagine, as AI enthusiasts do, that AI-assisted work simply increases productivity without necessarily
removing a bioinformatician's job. How useful, costly, and safe is it to use AI agents for scientific work?
With this post I want to add a single data point to the discussion, and look in some more detail at various
implementation details that are specific to the German sensitivity to data protection (*Datenschutz*) and independence
from foreign companies ([broadly gestures at everything](https://i.kym-cdn.com/photos/images/original/001/877/982/0ed.png)).

## The task

I gave myself the task of collecting as many large bacterial datasets as possible that were used for GWAS/ML studies,
and in particular of focusing on those in which the genetic variants causal for a phenotype were experimentally validated.
The final output I wanted was a table with as many details as possible. A boring chore that seems perfect for an agent
to do. I therefore prepared [an initial set of 15 papers](https://github.com/microbial-pangenomes-lab/2026_literature_parsing/blob/main/Zotero/Zotero.bib)
(identified through the excellent [Google Scholar Labs tool](https://scholar.google.it/scholar_labs/search?hl=en)),
for two of which I had already [filled the table with some sensible fields](https://github.com/microbial-pangenomes-lab/2026_literature_parsing/blob/main/datasets.tsv).
The papers were provided as a Zotero export in PDF format. I wanted the agent first to fill the table with details found in the papers, and then to fetch and parse additional ones.

## The models and their harnesses

I wanted to test whether this relatively simple but open-ended task could be performed well by a set of AI models
ranging from the frontier to the "portable" (i.e. locally hosted) ones. I therefore chose the following,
in order of "size":

* `Claude Opus 4.8` (using an Anthropic personal Pro license)
* `glm-5.2` (via a pay-as-you-go OpenRouter API key)
* `qwen-3.5-397b-a17b` (via an [Academic Cloud](https://academiccloud.de/)/[GWDG API key](https://docs.hpc.gwdg.de/services/ai-services/saia/index.html), free, but capped at 2000 requests per day)
* `qwen-3.6-35b-a3b` at 4-bit quantization (running on our lab's workstation with two Nvidia 3090 GPUs)

The use of the first two models clearly comes with data and intellectual property protection issues, while with the other two
we can ensure that data does not leave Germany and is not stored and used for further training. 

In terms of providing a harness to these models to become actual agents (as per [the "official" definition](https://simonwillison.net/2025/Sep/18/agents/)), I used
[Claude Code](https://claude.com/product/claude-code) for Claude, and the [`pi` agent harness](https://pi.dev/)
for the other three, with two extensions [to talk to the Academic Cloud models](https://github.com/microbial-pangenomes-lab/pi-academiccloud) and
[to host the smaller model locally](https://github.com/mgalardini/pi-llamacpp).
To avoid any collateral damage to files outside the working directory, I also used
[a sandboxing script based on the `bwrap` tool.](https://github.com/microbial-pangenomes-lab/2026_agentic_coding/blob/main/pi/sandbox.sh)
Lastly, I provided two skills to all agents:
[to use the excellent `liteparse` tool to extract text from PDFs](https://github.com/microbial-pangenomes-lab/mipa-pi-skills/blob/main/skills/liteparse/SKILL.md) and
[to use `uv` to set up isolated Python environments](https://github.com/microbial-pangenomes-lab/mipa-pi-skills/blob/main/skills/uv/SKILL.md).

## The prompts

I started with this prompt to fill the table with details from the initial set of 15 papers:

> I want to complete the table in `datasets.tsv` so that the information about bacterial GWAS datasets contained in this repository is complete.
I am particularly interested in identifying which of these studies have an experimentally validated hit
(gene presence/absence, short variants, or other kinds of variants).
Parse the papers using `liteparse` as needed and fill any missing information in the table and add the missing entries.
If you need to go online to find the source data/code from each paper feel free to do so.
If you think more columns should be added to make the table more detailed please do so.
Also prepare a markdown file detailing the steps you have taken and any trouble you have faced.

Once that was done I asked the agents to fetch additional papers:

> Now try to add more entries to the table: query pubmed using their entrez API
(you can for instance use the Bio.Entrez module from Biopython, use `uv` to set the environment,
and use my email `XX.YY@twincore.de`, be careful not to exceed their quota).
Find relevant papers listing large bacterial GWAS datasets, focusing (but not exclusively) on those
with experimentally validated hits. Make a list of PMIDs,
I will then download them and provide them for parsing and completing the table.
Continue to document what you are doing. 

I then created a Zotero folder from the list of PubMed IDs provided by the agent, got the PDFs, and exported them
as a new Zotero folder. This was the last instruction given:

> I created a new Zotero folder called `XXX`. Complete the `datasets.tsv` file, adding a column to indicate that the new entries come from an AI-assisted search

## Hiccups and cost

All four agents completed the task in a reasonable amount of time (no more than an hour, excluding the time I spent clicking
around in the browser to fetch the PDFs Zotero could not automatically find). The only agent requiring intervention on my part
was the one using the Academic Cloud model provider, which got too busy and started hanging; I downgraded the model to
`qwen-3.5-122b-a10b` and could continue the task.

The only model for which I could measure inference costs directly was `glm-5.2`, which consumed $1.75 overall. I did not
reach the usage limit on either my Anthropic personal Pro account or in Academic Cloud, for which I used 94 requests over the 2000 daily limit.
The local agent likely increased the temperature in my office slightly, but luckily I was working from home that day.
There's a lot of hidden or subsidized costs in all four agents, but it's clear how this task was executed on the cheap.

## Results

More importantly, did the agent perform well? I was interested in comparing the way they filled out the table from the original
set of papers, but more importantly if they identified more datasets that I had originally missed.

The most interesting result is that none of the additional 80 papers was identified by all four agents; a single one (a PhD dissertation!) was
identified by three, and 13 by at least two agents. It is therefore also likely that running the same agent multiple times
would have given different results. A truly open-ended task.

Another interesting, or rather concerning, result is that `qwen-3.5-397b-a17b/122b-a10b` missed the `.bib` file in the Zotero export folder and filled the
table with hallucinated DOIs. This agent also had the weakest strategy to filter its own PubMed searches, including five papers that had nothing to 
do with bacteria. Hallucinations are still a thing, even in an agent loop.

Surprisingly, the smallest (and quantized!) model performed well, suggesting only eight new datasets, but with explicit filters to identify
bona-fide bacterial datasets with an actual experimental validation.

In the heavyweights league, the underdog `glm-5.2` differentiated itself from the incumbent by not using a binary classification
of whether a dataset had an experimentally validated hit, but added a third "partial" category to flag unclear examples.

## The aftermath

After running this experiment I had Claude further refine the four tables to remove the smaller studies, fix the obvious hallucinations, and harmonize
the columns. I then dumped the resulting table on poor [Alessio](https://www.microbial-pangenomes-lab.org/members/) for a round of manual curation.
The final result turned out to be quite useful for some work we are doing in the lab.

I can see how my own experience and preference in tools influenced the agents; I could have simply given a prompt with no initial set of papers,
no preferred tools (i.e. `liteparse` and `biopython`), and removed myself completely from the loop. I would imagine that an AI-native scientist
would have let the agent figure out which tools and strategy to use, likely leading to a different set of datasets,
but possibly making the identification of mistakes more difficult.

Despite the hallucinations and small sample size, this little experiment shows that agents can be useful for open-ended work,
provided that multiple agents are run and that a human stays in the loop to check for gross errors.
More importantly, locally hosted models seem to already be on par with their larger counterparts, at least when given a relatively narrow task.
This is a very exciting possibility, especially for people working on sensitive data or worried about depending on foreign entities.
The EU however still needs to produce more of its own open-weight models to be truly independent.
