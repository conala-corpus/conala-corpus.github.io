## Introduction

We propose, conala, a scalable, language-agnostic approach for mining parallel corpus of source code and natural language from Stack Overflow (SO). It consists of two components:

![Overview of conala]({{ "conala.jpg"}})

* An offline training procedure that learns a classifier to detect natural language-code snippet pairs on SO using small amount of annotated data.
* An online mining algorithm that extracts a ranked list of natural language-code snippet pairs for each SO page.

## Source Code and Data Set

### Mining 

We released the training/evaluation code to reproduce the evaluation results in our submission at [here](https://github.com/conala-anonymous/sominer)

### Annotation Dataset

We annotated a small amount of NL/snippet pairs to train the classifier, which are released [here](https://github.com/conala-anonymous/annotation_dataset)
