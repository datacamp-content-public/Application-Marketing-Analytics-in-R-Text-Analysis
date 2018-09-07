---
title: Insert title here
key: cc30cbf2c09acb54b3a8a5ad506e3f36

---
## Topic Modeling

```yaml
type: "TitleSlide"
key: "c47d0ba4dd"
```

`@lower_third`

name: Marc Dotson
title: Marketing Professor


`@script`
So far in this course, you have learned how to wrangle and visualize text. In particular, you’ve applied a tidy, bag-of-words approach to text analysis using the tidytext package. You’ve seen how the tidy text format of a long data frame with a single token per row has facilitated your use of dplyr, ggplot2, and other tidyverse packages to effectively wrangle and visualize text.

However, we often want to do more than just compute and visualize word frequencies. One of the most useful modeling approaches for text is topic modeling. While word frequencies suggest overall meaning, topic modeling is used to uncover the themes or topics being written about within a corpus. Identifying topics within a corpus is especially useful as the number of documents increases and any qualitative assessment of content becomes impractical.


---
## Clustering vs. Topic Modeling

```yaml
type: "TwoRows"
key: "920d6619dc"
```

`@part1`
Clustering
- Clusters are uncovered based on distance, which is continuous.
- Every object is assigned to a single cluster.
- Clusters are summarized based on averages.


`@part2`
Topic Modeling
- Topics are uncovered based on word frequency, which is discrete.
- Every document is a mixture (i.e., partial member) of every topic.
- Topics are summarized based on word probabilities.


`@script`
Because topic models uncover topics or groups of words that occur together, they are often confused with other unsupervised learning techniques, clustering in particular. It’s worth taking a moment to distinguish these two techniques.

Common clustering techniques like k-means and hierarchical clustering are identified based on distance between objects, which is an inherently continuous measure. Furthermore, each object being clustered is assigned to a single cluster. Finally, clusters are often summarized based on averages, which is another continuous measure.

Topic models identify topics based on word frequency, which is an inherently discrete measure. Furthermore, each object (in this case, a document within a corpus) is a mixture or partial member of every topic. Finally, topics are often summarized based on word probabilities.

To be clear, a topic model is the appropriate tool for modeling text based on the discrete nature of text and the more realistic property of characterizing every document as a mixture of topics.


---
## Create a Document Term Matrix

```yaml
type: "TwoRows"
key: "cdffc2d578"
```

`@part1`
- Let's use the most common topic model: latent Dirichlet allocation (LDA).
- The input for a topic model is not tidy data, it’s a document term matrix (DTM).
- Let’s “cast” our tidy data into a DTM.


`@part2`
``dtm_text <- tidy_text %>%
     anti_join(stop_words) %>%
     count(word, talk) %>%
     cast_dtm(talk, word, n)
``


`@script`
But enough of that – let’s actually run a topic model! We will be using the topicmodels package and the most commonly used topic model: latent Dirichlet allocation or LDA. Our first challenge is the input for a topic model is a document term matrix or DTM. In a DTM, each row is a document with a count of the occurrences of each term as columns.

We shouldn’t be surprised that the tidytext package again comes to the rescue! Taking our product review data in a tidy text format, we can compute word frequencies by document and use the cast_dtm() function to easily create a DTM.


---
## Final Slide

```yaml
type: "FinalSlide"
key: "672ef88d0b"
```

`@script`


