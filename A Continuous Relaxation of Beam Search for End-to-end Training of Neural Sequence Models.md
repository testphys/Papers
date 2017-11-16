
# Table of Contents

1.  [A Continuous Relaxation of Beam Search for End-to-end Training of Neural Sequence Models](#org20b9c85):beam:search:seq2seq:NER:tagging:
    1.  [Problem](#orgeab0a30)
        1.  [models are not optimized for beam search decoding](#org418fb7b)
        2.  [sometimes beam search is worse than greedy search](#org41dfe31)
    2.  [Datasets](#orged92542)
        1.  [CONLL 2003 shared task data for German language](#org9b4fef9)
        2.  [CCG Supertagging Bank](#org3570b71)
    3.  [Model](#org42b5876)
        1.  [seq2seq with fixed attention](#orge5d0fbd)
        2.  [use decomposable Hamming loss at each timestep](#orgd2e0cc7)
        3.  [continuous approximation of beam search procedure](#org09568af)
        4.  [annealing of the softmax temperature](#orgf530f16)
        5.  [hyperparameters are chosen after 50 epochs with multiple random starts](#org8ed1033)
        6.  [pretrain with cross-entropy](#orgd1e7210)
        7.  [decode using soft beam search with hard attention](#org12d837a)
    4.  [Related Work](#orgd25b609)
        1.  [reinforcement learning](#org0b5ef8a)
        2.  [imitation learning](#orgf76be33)
        3.  [discrete search based methods](#orgc28a4d4)
        4.  [continuous approximation of greedy decoding for scheduled sampling objective](#orgf4de5ec)
    5.  [Experiments](#orgb544808)
        1.  [baseline is a cross-entropy trained seq2seq model](#org39072fc)
        2.  [56 F1 score (+1.5) on NER](#org6831da7)
        3.  [85 (+5.5) on supertagging](#org4e142de)


<a id="org20b9c85"></a>

# A Continuous Relaxation of Beam Search for End-to-end Training of Neural Sequence Models     :beam:search:seq2seq:NER:tagging:

<span class="timestamp-wrapper"><span class="timestamp">&lt;2017-08-02 수 11:05&gt;&#x2013;&lt;2017-08-02 수 11:45&gt;</span></span>
<https://arxiv.org/abs/1708.00111>


<a id="orgeab0a30"></a>

## Problem


<a id="org418fb7b"></a>

### models are not optimized for beam search decoding

1.  beam search is not continuous

    1.  discrete argmax decisions
    
    2.  discrete input


<a id="org41dfe31"></a>

### sometimes beam search is worse than greedy search

1.  when using BLEU


<a id="orged92542"></a>

## Datasets


<a id="org9b4fef9"></a>

### CONLL 2003 shared task data for German language

1.  used provided data splits

2.  no preprocessing

3.  10 biased labels towards no entity label


<a id="org3570b71"></a>

### CCG Supertagging Bank

1.  supertagging is a finer version of POS

2.  provided data splits

3.  minor preprocessing

4.  1284 long-tailed and correlated labels


<a id="org42b5876"></a>

## Model


<a id="orge5d0fbd"></a>

### seq2seq with fixed attention

1.  64/512 bidirectional LSTM encoder with tanh activation and 8/512 dim embeddings

2.  attend i-th input at i-th decoding step

3.  64/512 LSTM decoder with tan activation


<a id="orgd2e0cc7"></a>

### use decomposable Hamming loss at each timestep

1.  fraction of labels incorrectly predicted


<a id="org09568af"></a>

### continuous approximation of beam search procedure

1.  temperature controlled softmax approximates argmax

2.  top-k-argmax are represented as matrices

    1.  square distance of all scores from i-th argmax
    
    2.  peaked softmax over negative square distance of all matrix entries

3.  summation over vocabulary dimension gives k soft-attention scores for predecessors


<a id="orgf530f16"></a>

### annealing of the softmax temperature


<a id="org8ed1033"></a>

### hyperparameters are chosen after 50 epochs with multiple random starts


<a id="orgd1e7210"></a>

### pretrain with cross-entropy


<a id="org12d837a"></a>

### decode using soft beam search with hard attention


<a id="orgd25b609"></a>

## Related Work


<a id="org0b5ef8a"></a>

### reinforcement learning


<a id="orgf76be33"></a>

### imitation learning


<a id="orgc28a4d4"></a>

### discrete search based methods


<a id="orgf4de5ec"></a>

### continuous approximation of greedy decoding for scheduled sampling objective


<a id="orgb544808"></a>

## Experiments


<a id="org39072fc"></a>

### baseline is a cross-entropy trained seq2seq model


<a id="org6831da7"></a>

### 56 F1 score (+1.5) on NER


<a id="org4e142de"></a>

### 85 (+5.5) on supertagging

