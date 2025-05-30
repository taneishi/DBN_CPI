# Deep Belief Network for Compound-Protein Interaction Prediction

## Introduction

*Deep belief network*, DBN is one of the models proposed in the early days of *deep learning*, DL[^Hinton2006].
It performs pre-training to prevent overfitting of *multilayer perceptron*, MLP.
Here, we show an example that applies DBN to *virtual screening* in drug discovery.

This example is based on the experiment we performed in 2014.
In 2006, we used *support vector machine*, SVM to predict the same virtual screening target, but it was difficult to scale up the dataset due to computational complexity issues.
Then, GPU accelerators made it feasible to train large datasets using DL, and we performed virtual screening based on large-scale data using DBN.

## Dataset

The dataset consist of combinations of proteins belonging to GPCR family and small molecules that interact with them.
As features of the interactions between compounds and proteins, we employ a combination of features based on the chemical structure of small molecules and features based on the amino acid residues of proteins.
The novelty of this approach is that the target of virtual screening is not chemical compounds, but rather the interactions between compounds and proteins.

## Model

DBN is based on MLP, with each layer is pre-trained as *restricted Boltzmann machine*, RBM, then trains as MLP.
We employ `Theano` for DL framework.

### Optimization of Theano

The code used in this experiment was employed by Intel to optimize `Theano` for multi-core processors. The optimized code was reflected in `Theano`.

## Results

As a result, we achieved higher prediction accuracy than the conventional SVM for the dataset of up to 4 million interactions between compounds and GPCRs.
We also confirmed that accuracy increased as the dataset became larger.

On the other hand, since negative examples in this dataset were generated by combinations different from positive examples, we decided to move forward with using actual assay results as the dataset.

[^Hinton2006]: G.E. Hinton et al., *A Fast Learning Algorithm for Deep Belief Nets*, **Neural Computation**, 2006.
