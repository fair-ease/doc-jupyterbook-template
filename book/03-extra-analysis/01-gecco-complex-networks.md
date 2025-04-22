---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# GECCO analysis over time (EXAMPLE)

This is far from perfect example, but the point being that that treating the EMO-BON samplings as *complex networks*, ie. graphs provides advantages on how to compare the results over time and space.

Every sequencing event is represented as a graph. Graphs can be constructed on both *taxonomy* [1](https://doi.org/10.1093/bib/bbaa005) and *functional* tables. Depending on the question at hand, different graphs represent the sequencing result [rK communities](https://www.nature.com/articles/s41598-021-03018-z).

Here I create graphs from the secondary analysis (GECCO) runs to identify *Biosynthetic Gene Clusters* (BGCs).

::::{note} Pilot demos allow to submit and receive GECCO jobs run on Galaxy. If interested, start [here](https://github.com/emo-bon/momics-demos?tab=readme-ov-file#wf3-biosynthetic-gene-clusters-bgcs)
:class: dropdown

## Setup

I ran GECCO locally on the assembled contigs from the metaGOflow for one single station (Ria Formosa). 16 total sequencing analyses in batch 1 and batch 2 are distributed into *replicates*, *soft sediment* and *water column samplings* and *3 collection dates*, which results in overall limited time series of maximum 3 time-points, but sufices for demonstration purposes.

```bash
gecco -v run --genome XXX.fa
```

GECCO version 0.9.10, default parameters.

## Loading 

