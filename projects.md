---
layout: default
---

# Project Portfolio

## Audio Sample to FM Synthesis Predictor

### Personal project, October 2022 - Present

See detailed description [here](./sample2genesis.html).

#### Objective

* Given an audio sample, use (convolutional) neural networks to predict the YM2612 synthesizer chip registers (settings) needed to replicate the sound (or a close approximation of it).

#### Progress
* Preprocessed audio sample data taken from Sega Genesis audio output by analyzing spectra, identifying the samples’ fundamental frequencies, and applying dimension reduction techniques to the raw audio sample data.
* Trained neural network models on the spectra, reduced audio data, and YM2612 synthesizer chip registers.

#### Latest update

(March 3, 2023) I have tested 7 out of 8 convolutional neural network models, and will test the last one tonight (it has the largest training set, so I saved it for last). See the above link for details.

## Bloomberg Challenge

### TAMU Datathon, October 2022

#### Objective

Contestants were provided 5 tanh-embeddings, each corresponding to a news article (no other clues given). Also, a set of ~1,000 articles with their corresponding embeddings were provided.

* Part 1: Determine the subjects of the articles corresponding to the 5 embeddings.
* Part 2: Build a general article classifier for the embeddings (sports vs. politics vs. travel, etc.).

#### What Was Done
* Used a TF-IDF vector to count and reweigh the frequencies of all words in the provided news articles.
* Used a _k_-nearest neighbor model with a cosine metric to determine the nearest neighbors to each of the 5 embeddings.

#### Latest update

(October 17, 2022) I have returned to this project, and am working on a custom classifier, which is essentially Bayesian classification with Gaussian mixtures to allow for a wider variety of cluster shapes.

## TAMU Institute of Data Science Competition

### April 2022

#### Objective

* To conduct a data-driven study that describes and visualizes Texas A&M University's research output in ways that illuminate the patterns of collaboration across disciplines and can help TAMU communicate the significance and impact of that research.
* Present these findings to a panel of judges as if they were university leaders, state representatives, the public, etc.

See the competition [website](https://tamids.tamu.edu/2022/01/23/2022-dscomp-call/) for more information on the objective.

My team and I have a [website](https://arpan-pal.github.io/ds_comp_22/index.html) showcasing this project. I also have a fork of our GitHub repository for anyone interested. We were named a Finalist and won the category of "Best Use of External Data".

As the four of us were mathematics graduate students, we focused our efforts on the interdisciplinary research of the TAMU Mathematics Department.

#### What Was Done
* Extracted metadata from TAMU Libraries for research articles from authors in the TAMU Mathematics, Statistics, and Computer Science departments.
* Developed a Python script to clean collected data by cross-referencing with Cornell’s arXiv database, since this database kept track of specific subfield, while TAMU Libraries did not. On the other hand, arXiv only keeps track of _current_ affiliation, not affiliation at the time of publishing each article (TAMU Libraries, of course, does).
* Produced visualizations (using VosViewer) of data on recent collaborative research output between these departments.
* Identified emerging sub-fields of mathematics in interdepartmental applications and proposed future collaborations.

[back](./)
