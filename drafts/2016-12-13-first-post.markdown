---
layout: post
title:  "Developing Sentence Embeddings on Quora's Question Pairs"
date:   2017-05-12 18:00:00 +0800
categories: nlp
---
The Quora question-pair dataset challenge was released in January 2017, with the intent of eliminiating question redundancies. In essence, the problem is of quantifying semantic similarity between two short texts. This posed a new challenge to the research community because question lengths are by nature short, compared to sentence classification which has more words for discrimination.

Directly representing words in a vector space (word embeddings) have gained interest with Mikolov et al.'s development of word2vec. In a well trained word2vec model, related words are close to each other in the vector space. For example, the vector for the words “king” and “queen”, both having a sense of royalty, would be close.

However, forming a sentence vector from word vectors that faithfully maintains the semantic meaning of the text poses the main challenge. One could average all the word vectors in a sentence, however, this loses word order [3] and places equal emphasis on all words. Removing stop-words may not be effective as well, given that the text is short and context may be lost. Boom et. al [4] reported that scaling the word vectors with tf-idf 2 weights, which assigns each word relative importance, yielded promising results for short text.

Code:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

