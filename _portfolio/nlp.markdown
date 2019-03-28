---
layout: post
title: Natural Language Processing
description: quora questions
img: 
---

# **Quora Questions** [[Code]](https://github.com/lefthandwriter/QuoraQuestionPairs)

Term group project, ECE6254 Statistical Machine Learning.

Classifying if two questions are redundant plays an important role for websites that offer a question-answer service, such as Quora, Stack Exchange, Piazza, and general forums. Quora’s dataset, released January 25th, 2017, consists of binarily labelled question pairs, depending on whether they are effectively asking the same question. 

Question similarity classification is a problem of distinguishing semantic similarity between two short texts. Beginning with word embeddings ([word2vec by Mikolov](https://arxiv.org/abs/1301.3781)), my tasks were to obtain sentence embeddings that would be representative of each question. I experimented with taking the sum of the word vectors, after scaling each word vector its with term frequency inverse document frequency (tf-idf). I also augmented parts-of-speech tags and named-entity-recognition tags counts to the sentence vectors, generated from the [Stanford NLP toolkit](https://stanfordnlp.github.io/CoreNLP/). Finally, I tried augmenting path similarity distance as measured by [WordNet](https://wordnet.princeton.edu) between groups of similar word types (noun-noun, verb-verb, adjective-adjective).

