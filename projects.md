---
layout: page
title: Projects
permalink: /projects/
---
These are the abstracts of selected projects that I have undertaken recently.


## Classifying Quora Question-Pair Similarity 
###(Group Project, Georgia Tech)
Classifying if two questions are redundant plays an important role for websites that offer a question-answer service, such as Quora, Stack Exchange, Piazza, and general forums. Quora’s dataset, released January 25th, 2017, consists of binarily labelled question pairs, depending on whether they are effectively asking the same question. 

Question similarity classification is a problem of distinguishing semantic similarity between two short texts. Beginning with word embeddings ([word2vec by Mikolov](https://arxiv.org/abs/1301.3781)), my tasks were to obtain sentence embeddings that would be representative of each question. I experimented with taking the sum of the word vectors, after scaling each word vector its with term frequency inverse document frequency (tf-idf). I also augmented parts-of-speech tags and named-entity-recognition tags counts to the sentence vectors, generated from the [Stanford NLP toolkit](https://stanfordnlp.github.io/CoreNLP/). Finally, I tried augmenting path similarity distance as measured by [WordNet](https://wordnet.princeton.edu) between groups of similar word types (noun-noun, verb-verb, adjective-adjective).

All code was done in Python for this project.


## Numerical State Estimation of Operating Condition of Power System 
###(Individual Project, Georgia Tech)



## Danielson-Lanczos 2D FFT algorithm with MPI and PThreads 
###(Individual Project, Georgia Tech)

