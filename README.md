# Hierarchical Modular Event Argument Extraction
The code is an implementation of Hierarchical Modular Event Argument Extraction (EMNLP19 paper).

# Requirments
tensorflow-gpu==1.10

stanfordcorenlp (see https://github.com/Lynten/stanford-corenlp for detail)

numpy

tqdm

# Usage
To run this code, you need to:
1. put ```English``` folder of ACE05 dataset into ```./```, or you can modify path in ```constant.py```. (You can get ACE2005 dataset here: https://catalog.ldc.upenn.edu/LDC2006T06)
2. put stanford language model (```stanford-corenlp-full-2018-10-05```) into ```./```, or you can modify path in ```constant.py```. (You can download here: https://stanfordnlp.github.io/CoreNLP/history.html)
3. put GloVe embedding file into ```./glove``` folder, or you can modify path in ```constant.py```. (You can download GloVe embedding here: https://nlp.stanford.edu/projects/glove/)
4. Run ```python train.py --gpu 0 --mode HMEAE``` to run with HMEAE model.  Run ```python train.py --gpu 0 --mode DMCNN``` to run with DMCNN model.

All parameters are in ```constant.py```, you can modify them as you wish.

# Dataset
Due to license limitation, we can't distribute datasets directly, please download the dataset by yourself. The download link is given in **Usage** part.

The code will automatically extract information of ACE2005 dataset and dumps them into json format(```train.json``` ,```dev.json``` and ```test.json```) into path ```ACE_DUMP``` in ```constant.py```. This is implented in class ```Extractor``` in ```utils.py```.

Each file is composed of a list, which elements are instances with following format:
```
{
    "tokens": XX,           #tokens of a sentence, a list with string elements
    "start": XX,            #starting offsets of the sentence in original files, an integer
    "end": XX,              #ending offsets of the sentence in original files, an integer
    "offsets":XX,           #offsets of each tokens, a list with tuple elements
    "trigger_tokens":XX,    #tokens of trigger words, a list with string elements
    "trigger_start":XX,     #start index of trigger words of tokens, an integer
    "trigger_end":XX,       #end index of trigger words of tokens, an integer
    "trigger_offsets":XX,   #offsets of trigger words, a list with tuple elements
    "event_type":XX,        #event type of tokens with given triggers, a string
    "file":XX,              #file name without suffix
    "dir":XX,               #dir name
    "entities":XX           #entitie in this sentencem, a list with entity elements
}
```


Each entity is a dictionary with following format:
```
{
    "token":XX,             #tokens of the entity, a list with string elements
    "role":XX,              #role of the entity when trigger is given, a string
    "offsets":XX,           #offsets of entity, a list with tuple elements
    "start":XX,             #start offset of entity, an integer
    "end":XX,               #snd offset of entity, an integer
    "idx_start":XX,         #start index in tokens, an integer
    "idx_end":XX            #end index in tokens, an integer
}
```

# Cite
If the codes help you, please cite our paper:

**HMEAE: Hierarchical Modular Event Argument Extraction.** *XiaoZhi Wang, Ziqi Wang, Xu Han, Zhiyuan Liu, Juanzi Li, Peng Li, Maosong Sun, Jie Zhou, Xiang Ren.* EMNLP-IJCNLP 2019.
