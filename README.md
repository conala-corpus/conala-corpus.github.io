## Introduction

We propose, conala, a scalable, language-agnostic approach for mining parallel corpus of source code and natural language from Stack Overflow (SO). It consists of two components:

![Overview of conala]({{ "conala.png"}})

* An offline training procedure that learns a classifier to detect natural language-code snippet pairs on SO using small amount of annotated data.
* An online mining algorithm that extracts a ranked list of natural language-code snippet pairs for each SO page.

## Source Code and Data Set

### Mining 

We released the training/evaluation code to reproduce the evaluation results in our submission at [here](https://github.com/conala-anonymous/sominer)

### Annotation Dataset

This dataset contains 2,563 high-quality natural language intent and source code snippet pairs in Python. The dataset is further split into 2,063 examples for training and 500 examples for testing, respectively.

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
