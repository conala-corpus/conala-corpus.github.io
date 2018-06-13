Welcome to the site of CMU CoNaLa, the Code/Natural Language Challenge, a joint
project of the Carnegie Mellon University NeuLab and STRUDEL Lab! This
challenge was designed to test systems for **generating programs from natural
language**. For example, if the input is "sort list x in reverse order", then
the system would be required to output `x.sort(reverse=True)` in Python.

* [Dataset Information](#Dataset-Information)
* [Training Baselines](#Training-Baselines)
* [Submitting Results](#Submitting-Results)
* [Leader Board](https://competitions.codalab.org/competitions/19175)

There is also information about how you can train a baseline system, evaluate, and
submit your results to be posted on the leaderboard.

## Dataset Information

We have released a dataset crawled from [StackOverflow](http://stackoverflow.com),
automatically filtered, then curated by annotators, split into 2,063 training and
500 test examples. We also provide a large automatically-mined dataset with 600k
examples, and links to other similar datasets. These data sets can be used for
the CoNaLa challenge, or for any other research on the intersection of code and natural
language.

* **Download**: [CoNaLa Corpus v1](http://www.phontron.com/download/conala-corpus-v1.0.zip)

We describe the data briefly below, and you can find more data in
[our MSR 2018 paper](https://arxiv.org/pdf/1805.08949.pdf), which we'd appreciate
you cite if you use the corpus in your research or participate in the challenge:

```
@inproceedings{yin2018mining,
  author = {Yin, Pengcheng and Deng, Bowen and Chen, Edgar and Vasilescu, Bogdan and Neubig, Graham},
  title = {Learning to Mine Aligned Code and Natural Language Pairs from Stack Overflow},
  booktitle = {International Conference on Mining Software Repositories},
  series = {MSR},
  pages = {476--486},
  year = {2018},
  publisher = {ACM},
  doi = {https://doi.org/10.1145/3196398.3196408},
}
```

### Manually Curated Data

The manually curated CoNaLa dataset contains high-quality natural language
intent and source code snippet pairs in Python, split into the `conala-train`
and `conala-test` datasets. 

The train/test splits are stored in `json` format, and you can see some
examples below:
Some examples in the dataset are:

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
intent | Natural Language intent (i.e., the title of a Stack Overflow question)
rewritten_intent | Crowdsourced revised intents that try to better reflect the full meaning of the code, typically done by incorporating variable names and function arguments that appeared in the code into the intent. This is the input to be used by systems in the CoNaLa challenge.
snippet | A code snippet that implements the intent. This is the output of systems in the challenge.

### Other Data Sources

In the CoNaLa challenge, you are allowed to use other data sources to improve
your system accuracy **as long as you exclude any information from the specific
StackOverflow questions that are included in the test set**. We provide links
to a number of data sources below, but other sources may be used as well:

#### Automatically Mined Intent/Snippet Pairs
The above archive includes 598,237 candidate intent/snippet pairs mined by our 
system, in the `conala-mined` data set.
The file is stored in [Json lines](http://jsonlines.org/) format. 
A description of each field is:

Field | Description
------------ | -------------
question_id | Id of the Stack Overflow question
parent_answer_post_id | Id of the answer post from which the candidate snippet is extracted
intent | The natural language intent
snippet | The extracted code snippet
id | Unique id for this intent/snippet pair
prob | Probability given by the mining model

#### External Datasets

You may also use data from other external sources such as:
* [Django Dataset](https://ahcweb01.naist.jp/pseudogen/)
* [StaQC](https://github.com/LittleYUYU/StackOverflow-Question-Code-Dataset): *note* that this is mined from StackOveflow, so you must ensure that you do not use the questions included in the CoNaLa test set.

## Training Systems

To participate in the CoNaLa challenge, you should use the `conala-train`
and/or `conala-mined` datasets to train a system, take the `rewritten_intent`
field of the `conala-test` dataset as input, and generate output from it.
More details of how to do so, along with example scripts to perform preprocessing
and train a baseline sequence-to-sequence model can be found on the
[conala-baseline](https://github.com/conala-corpus/conala-baseline/) web site.

## Submitting Results

The results are submitted by creating a zip file containing a single file "answer.txt",
which is in JSON array format with one line being one code snippet. An example of how
to create this file can also be found in the [conala-baseline](https://github.com/conala-corpus/conala-baseline/)
directory.

Once you have created this file, you can submit it to the [Leader Board](https://competitions.codalab.org/competitions/19175).

## Mining Method

The CoNaLa data was mined using a scalable, language-agnostic approach for mining parallel 
corpora of source code and natural language from Stack Overflow. 

The **key idea** behind the method, described in detail in 
[our MSR 2018 paper](https://arxiv.org/pdf/1805.08949.pdf) and [this presentation slides](slides.pdf), 
is to *learn semantic correspondence features between the natural language and 
code using neural network models for machine translation*,
which can calculate bidirectional conditional probabilities of the code given 
the natural language and vice-versa of the natural language given the code.

Our approach has two components:

![Overview of CoNaLa]({{ "conala.png"}})

* An offline training procedure that learns a classifier to detect "good" pairs
of natural language and code snippets on Stack Overflow, using only a small amount 
of labeled data.
* An online mining algorithm that can extract a ranked list of pairs of natural 
language and code from a Stack Overflow page or the 
[Stack Overflow data dump](https://archive.org/details/stackexchange).

You can find the training/evaluation code to reproduce the evaluation results in 
our MSR paper [here](https://github.com/conala-anonymous/sominer).

### Human-in-loop Quality Improvement

![Overview of CoNaLa]({{ "iter_quality_improve.png"}})

We aim to improve the performance of the mining model using iterative human feedback.
Specifically, we ask professional programmers to annotate the top-ranked predictions given by the model.
And use the annotated results to re-train the model. 

## Links:

* [Neulab](http://www.cs.cmu.edu/~neulab/)
* [STRUDEL Lab](https://cmustrudel.github.io/)
* [Our Code Generation Research](https://github.com/pcyin/NL2code)
* Contact: [Pengcheng Yin](http://pcyin.me)
