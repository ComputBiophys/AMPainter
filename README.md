# AMPainter
Painting Peptides with Antimicrobial Potency through Deep Reinforcement Learning


## Overview
This framework consists of three modules:
* a policy network to assign the mutation sites
* a fine-tuned protein language model to replace the assigned residues
* a predictor named HyperAMP to evaluate the antimicrobial activity


## Requirements
* pytorch
* [DHG](https://github.com/iMoonLab/DeepHypergraph)
* [ankh](https://github.com/agemagician/Ankh)
* transformers
* sklearn
* Levenshtein
* [modlamp](https://modlamp.org)


## Usage
### 1) HyperAMP solely
#### Train predictor
```bash
cd HyperAMP
python ankh_embedding.py
python tfidf.py
python train.py # or train_5folds.py
```
#### Predict
```bash
python ./HyperAMP/predict.py  # change input file path first
```
Length of a input peptide sequence should be less than 40.

The output of a input sequence is the transformed score based on its logMIC value to represent its antimicrobial activity.

### 2) Fine-tune Ankh
#### Data processing
(This step can be skipped for using `./data/maskseq1by1_0.2.csv` directly)
```bash
python ./finetune/ankh_ft_data_1by1.py
```
#### Run
```bash
python ./finetune/ankh_ft_noval.py
```

### 3) AMPainter framework
#### Train agent network
```bash
python ./RLloop/reinforce.py
```
#### Evolve input sequences
Default params: `lr = 1e-3`, `batch_size = 128`, `n_steps = 10`, `iterations = 8`
```bash
python ./RLevolve/reinforce.py
```

### 4) Fitness function version
#### Evolve input sequences
```bash
python ./fitness/reinforce.py
```

## Citation
```
@article{Dong2025AMPainter,
  author = {Dong, Ruihan and Cao, Qiushi and Song, Chen},
  title = {Painting Peptides With Antimicrobial Potency Through Deep Reinforcement Learning},
  journal = {Advanced Science},
  volume = {12},
  number = {43},
  pages = {e06332},
  keywords = {antimicrobial peptide, deep reinforcement learning, directed evolution, sequence design},
  doi = {https://doi.org/10.1002/advs.202506332},
  year = {2025}
}
```
