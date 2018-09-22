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
So far in this course, you have learned how to wrangle and visualize text. In particular, you’ve applied a tidy, bag-of-words approach to text analysis using the tidytext package. You’ve seen how the tidy text format of a long data frame with a single token per row has facilitated your use of dplyr, ggplot2, and other tidyverse packages to effectively wrangle and visualize text. You’ve applied these techniques to more than 24,000 reviews of a robotic vacuum.


---
## Beyond Word Frequencies

```yaml
type: "TwoColumns"
key: "8f869c1a4b"
```

`@part1`
![](https://assets.datacamp.com/production/repositories/3536/datasets/a1a36aecabd0746d88c0a2976eec12590bdcfc19/word_frequencies.pdf){{1}}


`@part2`
![](https://assets.datacamp.com/production/repositories/3536/datasets/85842f8b40c707cac54318aef1328de90c5d442c/topics.pdf){{2}}


`@script`
However, we often want to do more than just compute and visualize word frequencies. One of the most useful modeling approaches for text is topic modeling. While word frequencies suggest overall meaning, topic modeling is used to uncover the themes or topics being written about within a corpus. Identifying topics within a corpus is especially useful as the number of documents increases and any qualitative assessment of content becomes impractical. We’ll use topic modeling to uncover the concerns with and drivers of satisfaction for a robotic vacuum.


---
## Clustering vs. Topic Modeling

```yaml
type: "TwoRows"
key: "920d6619dc"
```

`@part1`
**Clustering**{{1}}
- Clusters are uncovered based on distance, which is continuous.{{2}}
- Every object is assigned to a single cluster.{{3}}


`@part2`
**Topic Modeling**{{4}}
- Topics are uncovered based on word frequency, which is discrete.{{5}}
- Every document is a mixture (i.e., partial member) of every topic.{{6}}


`@script`
Because topic models uncover topics or groups of words that occur together, they are often confused with other unsupervised learning techniques, clustering in particular. It’s worth taking a moment to distinguish these two techniques.

Common clustering techniques like k-means and hierarchical clustering are identified based on distance between objects, which is an inherently continuous measure. Furthermore, each object being clustered is assigned to a single cluster.

Topic models identify topics based on word frequency, which is an inherently discrete measure. Furthermore, each object (in this case, a document within a corpus) is a mixture or partial member of every topic.


---
## Create a Document Term Matrix

```yaml
type: "TwoRows"
key: "f67f45dbf3"
```

`@part1`
- Latent Dirichlet allocation (LDA) is the most commonly used topic model.{{1}}
- The input is a document term matrix (DTM), where each row is a document and each column is a count of the occurrences of each term.{{2}}


`@part2`
```
dtm_text <- tidy_text %>%
   count(word, document) %>%
   cast_dtm(document, word, n)
```{{3}}
```
dtm_text

<<DocumentTermMatrix (documents: 24243, terms: 4817)>>
Non-/sparse entries: 24243/116754288
Sparsity           : 100%
Maximal term length: NA
Weighting          : term frequency (tf)
```{{4}}


`@script`
But enough of that – let’s actually run a topic model! We will be using the topicmodels package and the most commonly used topic model: latent Dirichlet allocation or LDA. Our first challenge is the input for a topic model is a document term matrix or DTM. In a DTM, each row is a document with a count of the occurrences of each term as columns.

We shouldn’t be surprised that the tidytext package again comes to the rescue! Taking our product review data in a tidy text format, we can compute word frequencies by document and use the cast_dtm() function to easily create a DTM. The DTM is an R object specially encoded by the topicmodels package.


---
## Run a Topic Model

```yaml
type: "FullCodeSlide"
key: "3a32c0c18c"
```

`@part1`
```
lda_out <- dtm_text %>%
   LDA(
      k = 2,
      control = list(seed = 42)
   )
```{{1}}
```
lda_out

A LDA_Gibbs topic model with 2 topics.
```{{2}}


`@script`
Now that we have a DTM as an input, running a topic model is straightforward. We use the LDA() function, specifying the number of topics we want to produce and the seed to help in our recovery of the same topics given the probabilistic nature of model estimation.  The output is, again, a specially encoded R object.


---
## Tidying Topic Model Output

```yaml
type: "TwoRows"
key: "acaf735862"
```

`@part1`
```
lda_topics <- lda_out %>% 
  tidy(matrix = "beta")
```{{1}}
```
lda_topics %>% 
  arrange(desc(beta))

# A tibble: 9,634 x 3
   topic term       beta
   <int> <chr>     <dbl>
 1     2 roomba   0.0583
 2     2 clean    0.0308
 3     1 hair     0.0242
 4     1 time     0.0239
 5     1 floors   0.0200
 6     2 house    0.0199
 7     2 cleaning 0.0194
 8     1 day      0.0166
 9     2 floor    0.0164
10     2 vacuum   0.0147
# ... with 9,624 more rows
```{{2}}


`@part2`



`@script`
The most important output from a topic model are the topics themselves: the dictionary of all words in the corpus sorted according to the probability the word is part of that topic. However, the output from the LDA() function is not tidy. Once again, we can use a tidytext function, in this case tidy(), to take the matrix of topic probabilities and put them into a form that is easily visualized using ggplot2.


---
## Topic Word Probabilities

```yaml
type: "TwoColumns"
key: "267071b7e7"
```

`@part1`
```
lda_topics %>%
  group_by(topic) %>% 
  top_n(15, beta) %>% 
  ungroup() %>%
  mutate(
    term = reorder(term, beta)
  ) %>%
  ggplot(
    aes(
      term, 
      beta, 
      fill = as.factor(topic)
    )
  ) +
  geom_col(show.legend = FALSE) +
  facet_wrap(
    ~ topic, 
    scales = "free"
  ) +
  coord_flip()
```{{1}}


`@part2`
![](https://assets.datacamp.com/production/repositories/3536/datasets/85842f8b40c707cac54318aef1328de90c5d442c/topics.pdf){{2}}


`@script`
This is the same code we used to plot word frequencies, only this time we plot topic word probabilities, grouped and faceted by topic.


---
## Final Slide

```yaml
type: "FinalSlide"
key: "672ef88d0b"
```

`@script`
How do we know 2 topics is enough? How do we even interpret these topics? We’ll return to these issues of how to determine the number of topics and interpret the topics themselves.

For now, it’s your turn to run your first topic model!

