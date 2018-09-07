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
type: "FullSlide"
key: "54884523e3"
```

`@part1`



`@script`
Because topic models uncover topics or groups of words that occur together, they are often confused with other unsupervised learning techniques, clustering in particular. It’s worth taking a moment to distinguish these two techniques.

Common clustering techniques like k-means and hierarchical clustering are identified based on distance between objects, which is an inherently continuous measure. Furthermore, each object being clustered is assigned to a single cluster. Finally, clusters are often summarized based on averages, which is another continuous measure.

Topic models identify topics based on word frequency, which is an inherently discrete measure. Furthermore, each object (in this case, a document within a corpus) is a mixture or partial member of every topic. Finally, topics are often summarized based on word probabilities.

To be clear, a topic model is the appropriate tool for modeling text based on the discrete nature of text and the more realistic property of characterizing every document as a mixture of topics.


---
## Final Slide

```yaml
type: "FinalSlide"
key: "672ef88d0b"
```

`@script`


