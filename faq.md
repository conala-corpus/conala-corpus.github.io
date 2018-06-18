Below are a few questions that people have asked (or might ask).

## How can I get started?

The best way to get started is to download and run the
[conala baseline](https://github.com/conala-corpus/conala-baseline/).
This is a simple [sequence-to-sequence model with attention](https://arxiv.org/abs/1703.01619) based
on the [xnmt](https://github.com/neulab/xnmt/) toolkit.

If you want to try something more interesting, there are a number
of existing methods for language-to-code generation that are more sophisticated:
* **Syntactic Neural Model** (Yin and Neubig 2017): [Paper](https://arxiv.org/abs/1704.01696) [Code](https://github.com/pcyin/NL2code)
* **Abstract Syntax Networks** (Rabinovich et al. 2017): [Paper](https://arxiv.org/abs/1704.07535)
* **Neural Coarse-to-fine Parsing** (Dong and Lapata 2018): [Paper](https://arxiv.org/abs/1805.04793) [Code](https://github.com/donglixp/coarse2fine)

## How are Outputs Evaluated?

When evaluating the output of a code generation program, the most
important thing is whether the output accurately reflects the semantics
of the true program. One way to do this evaluation would be to create
unit tests or [fuzz tests](https://en.wikipedia.org/wiki/Fuzzing) that
check the correctness of the output of each program. However, given that
CoNaLa covers a large variety of programs that span software libraries
and environments, creating these tests was not feasible given our time
and resource constraints.

Thus, the [official CoNaLa evaluation script](https://github.com/conala-corpus/conala-baseline/blob/master/eval/conala_eval.py)
uses [BLEU score](https://en.wikipedia.org/wiki/BLEU), a measure of similarity
based on n-gram overlap. This has been used in
[previous work on code generation](https://arxiv.org/abs/1603.06744),
and is a proxy measure that tells how close the generated programs
match a gold-standard program.

## What version of Python is CoNaLa?

Python 3. All code found online was converted to Python3 using the
Python `2to3` utility, specifically [this script](https://github.com/conala-corpus/conala-baseline/blob/master/preproc/convert_to_python3.py).
