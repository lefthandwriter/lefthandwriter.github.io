---
layout: page
title: Projects
permalink: /projects/
---
These are the abstracts of selected projects that I have undertaken recently.

#
## Classifying Quora Question-Pair Similarity 
#### (Group Project, Georgia Tech)
Classifying if two questions are redundant plays an important role for websites that offer a question-answer service, such as Quora, Stack Exchange, Piazza, and general forums. Quora’s dataset, released January 25th, 2017, consists of binarily labelled question pairs, depending on whether they are effectively asking the same question. 

Question similarity classification is a problem of distinguishing semantic similarity between two short texts. Beginning with word embeddings ([word2vec by Mikolov](https://arxiv.org/abs/1301.3781)), my tasks were to obtain sentence embeddings that would be representative of each question. I experimented with taking the sum of the word vectors, after scaling each word vector its with term frequency inverse document frequency (tf-idf). I also augmented parts-of-speech tags and named-entity-recognition tags counts to the sentence vectors, generated from the [Stanford NLP toolkit](https://stanfordnlp.github.io/CoreNLP/). Finally, I tried augmenting path similarity distance as measured by [WordNet](https://wordnet.princeton.edu) between groups of similar word types (noun-noun, verb-verb, adjective-adjective).

All code was done in Python for this project.

#
## Hybrid State Estimation of Power System 
#### (Individual Project, Georgia Tech)
State estimation is a process of computing the minimum number of variables in order to obtain the current operating condition of the power system. The traditional power system consists of SCADA measurements that measure voltage and current magnitudes and real and reactive power flows. In this case, the state estimation problem is non-linear, requiring numerical computations.

In the past two decades, phasor measurement units (PMU) technology has been developed that can accurately measures the positive phase sequence voltage and current phasors. However, PMU technology is not yet ubiquitous in the power system. This creates a system that has a mixture of SCADA and PMU instruments, known as the hybrid state estimation problem.

Given a five bus substation system as a study, I used the approach of combining both SCADA and phasor measurements in one problem and computed the solution as a non-linear problem. This approach is based on the ["Supercalibrator" concept](http://ieeexplore.ieee.org/document/5589997/) by Prof Sakis Meliopoulos, where the states of an individual substation and interconnecting buses are computed locally to be sent to a central control station.

The accuracy was evaluated by taking the normalized residuals and chi-square test.

All code was done in MATLAB for this project.


#
## Drawing the Mandelbrot Set 
#### (Individual Project, Georgia Tech)
Using OpenGL and PThreads in C++, I drew the Mandelbrot Set, with a zoom + history feature and escape iteration of 8000.

<a href="http://www.youtube.com/watch?feature=player_embedded&v=JVzF5I_Xweo&t
" target="_blank"><img src="lefthandwriter.github.io/Mandelbrot.png" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>


#
## Danielson-Lanczos 2D FFT algorithm with MPI and PThreads 
#### (Individual Project, Georgia Tech)

