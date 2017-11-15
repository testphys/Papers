
# Table of Contents

1.  [A Continuous Relaxation of Beam Search for End-to-end Training of Neural Sequence Models](#org8feaa89):beam:search:seq2seq:NER:tagging:
    1.  [Problem](#orgd721bb3)
        1.  [model not optimized for beam search decoding](#orgc94a7bc)
        2.  [sometimes beam search worse than greedy search](#orgcdf4ac5)
    2.  [Datasets](#orgdda7221)
        1.  [CONLL 2003 shared task data for German language](#org3007515)
        2.  [CCG Supertagging Bank](#orgbb11ffe)
    3.  [Model](#org66a0de4)
        1.  [architecture](#org293a1b7)
        2.  [training](#orgf2e671c)
        3.  [decoding](#org73e30be)
    4.  [Related Work](#org7fac7d3)
        1.  [reinforcement learning](#org6c11aa8)
        2.  [imitation learning](#orgcb5b5dc)
        3.  [discrete search based methods](#orga6b8d07)
        4.  [continuous approximation of greedy decoding for scheduled sampling objective](#org2dffbcf)
    5.  [Experiments](#orgb652be3)
        1.  [Baselines](#org85dd724)
        2.  [Results](#org043304d)


<a id="org8feaa89"></a>

# A Continuous Relaxation of Beam Search for End-to-end Training of Neural Sequence Models     :beam:search:seq2seq:NER:tagging:

<span class="timestamp-wrapper"><span class="timestamp">&lt;2017-08-02 수 11:05&gt;&#x2013;&lt;2017-08-02 수 11:45&gt;</span></span>
<https://arxiv.org/abs/1708.00111>


<a id="orgd721bb3"></a>

## Problem


<a id="orgc94a7bc"></a>

### model not optimized for beam search decoding

1.  beam search not continuous

    1.  discrete armax decisions
    
    2.  discrete input


<a id="orgcdf4ac5"></a>

### sometimes beam search worse than greedy search

1.  when using BLEU


<a id="orgdda7221"></a>

## Datasets


<a id="org3007515"></a>

### CONLL 2003 shared task data for German language

1.  provided data splits

2.  no preprocessing

3.  10 labels

    1.  sentences biased towards containing no entity


<a id="orgbb11ffe"></a>

### CCG Supertagging Bank

1.  supertagging is a finer version of POS

2.  provided data splits

3.  minor preprocessing

4.  1284 labels

    1.  long tail
    
    2.  correlated


<a id="org66a0de4"></a>

## Model


<a id="org293a1b7"></a>

### architecture

1.  seq2seq with fixed attention

    1.  encoder
    
        1.  embeddings
        
            1.  8/512
        
        2.  bidirectional LSTM with tanh activation
        
            1.  64/512
    
    2.  attention
    
        1.  attend i-th input at i-th decoding step
    
    3.  decoder
    
        1.  LSTM with tan activation
        
            1.  64/512


<a id="orgf2e671c"></a>

### training

1.  Hamming loss

    1.  fraction of labels incorrectly predicted
    
        1.  calculate every timestep
    
    2.  discontinuous

2.  alternative Hinge loss

3.  continuous approximation of beam search procedure

    1.  temperature controlled softmax approximates argmax
    
        1.  peaked-softmax
    
    2.  top-k-argmax representation matrices
    
        1.  square distance of all scores from i-th argmax
        
        2.  peaked softmax over negative square distance of all matrix entries
    
    3.  previous beam identification
    
        1.  summation over vocabulary dimension gives k soft-attention scores for predecessors

4.  annealing of the softmax temperature

5.  hyperparameter tuning

    1.  pick best after 50 epochs
    
        1.  multiple random starts
    
    2.  pretrain with cross-entropy


<a id="org73e30be"></a>

### decoding

1.  softbeam search with hard attention


<a id="org7fac7d3"></a>

## Related Work


<a id="org6c11aa8"></a>

### reinforcement learning


<a id="orgcb5b5dc"></a>

### imitation learning


<a id="orga6b8d07"></a>

### discrete search based methods


<a id="org2dffbcf"></a>

### continuous approximation of greedy decoding for scheduled sampling objective


<a id="orgb652be3"></a>

## Experiments


<a id="org85dd724"></a>

### Baselines

1.  cross-entropy trained seq2seq


<a id="org043304d"></a>

### Results

1.  56 F1 score (+1.5) on NER

2.  85 (+5.5) on supertagging

