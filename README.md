## Introduction

We propose conala, a scalable, language-agnostic approach for mining parallel corpus of source code and natural language from Stack Overflow (SO). It consists of two components:

![Overview of conala]({{ "conala.png"}})

* An offline training procedure that learns a classifier to detect natural language-code snippet pairs on SO using small amount of annotated data.
* An online mining algorithm that extracts a ranked list of natural language-code snippet pairs for each SO page.

## Source Code and Data Set

### Mining 

We released the training/evaluation code to reproduce the evaluation results in our submission at [here](https://github.com/conala-anonymous/sominer)

### Annotation Dataset

This dataset contains 2,563 high-quality natural language intent and source code snippet pairs in Python. 
We deploy our system on top-50K *how-to* Python-tagged questions, collecting 598,237 candidate intent/snippet pairs.
We hire annotators to annotated top-ranked predictions in the candidate set, producing this annotation dataset.
The dataset is further split into 2,063 examples for training and 500 examples for testing, respectively.

The train/test splits are stored in `json` format. Some examples in the dataset are:

```
{
  "question_id": 36875258,
  "intent": "copying one file's contents to another in python", 
  "rewritten_intent": "copy the content of file 'file.txt' to file 'file2.txt'", 
  "snippet": "shutil.copy('file.txt', 'file2.txt')", 
}

{
  "intent": "How do I check if all elements in a list are the same?", 
  "rewritten_intent": "check if all elements in list `mylist` are the same", 
  "snippet": "len(set(mylist)) == 1", 
  "question_id": 22240602
}

{
  "intent": "Iterate through words of a file in Python", 
  "rewritten_intent": "get a list of words `words` of a file 'myfile'", 
  "snippet": "words = open('myfile').read().split()", 
  "question_id": 7745260
}
```

Here is the description of each field in an example:

Field | Description
------------ | -------------
question_id | Id of the Stack Overflow question
intent | Natural Language intent (i.e., the title of an Stak Overflow question)
rewritten_intent | Crowdsourced revised intents that try to refect the full meaning of the code, typically done by incorporating variable names and arguments appeared in the code into the intent. This is useful for fine-grained language-to-code tasks like code generation
snippet | A code snippet that implements the intent

The dataset is avaiable at [here](conala_annotations.zip)

**All Mined Intent/Snippet Pairs** We also released all 598,237 candidate intent/snippet pairs mined by our system, avaiable at [here](http://i.pcyin.me/python_mine_results.zip). The file is stored in [Json lines](http://jsonlines.org/) format. A description of each field is:

Field | Description
------------ | -------------
question_id | Id of the Stack Overflow question
parent_answer_post_id | Id of the answer post from which the candidate snippet is extracted
intent | The natural language intent
snippet | The extracted code snippet
id | Unique id for this intent/snippet pair
prob | probability given by the mining model

## Reference

```
@inproceedings{yin2018mining,
  author = {Yin, Pengcheng and Deng, Bowen and Chen, Edgar and Vasilescu, Bogdan and Neubig, Graham},
  title = {Learning to Mine Aligned Code and Natural Language Pairs from Stack Overflow},
  booktitle = {International Conference on Mining Software Repositories},
  series = {MSR},
  abbrv = {MSR 2018},
  year = {2018},
  publisher = {ACM},
  doi = {https://doi.org/10.1145/3196398.3196408},
}
```

[arXiv link to the paper](https://arxiv.org/pdf/1805.08949.pdf)

## Links:

* [Neulab](http://www.cs.cmu.edu/~neulab/)
* [STRUDEL Lab](https://cmustrudel.github.io/)
* [Our Code Generation Research](https://github.com/pcyin/NL2code)
* Contact: [Pengcheng Yin](http://pcyin.me)
