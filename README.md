# Final project for Bayesian Statistics Fall 2019

We implemented Stochastic Variational Inference (SVI) from scratch to fit the mean-field Latent Dirichlet Allocation (LDA) model on a corpus of New York Times articles. LDA is a mixed membership model: each article can talk about multiple topics in different propoertions. The mean-field assumption states that the topics are independent of each other.

The purpose of this project is to deeply understand how SVI and LDA work. The original LDA paper uses Coordinate Ascent VI (CAVI):

(1) Initialize topic assignment of each word and parameters

(2) Run Expectation Maximization on each document

(3) Update the global parameters using the output

(4) Repeat (2) and (3) until convergence

However, CAVI is prohibitively slow. SVI replaces step (2) with minibatches, which can be a single document, and modifies step (3) to update using the Robbins-Monro schedule.

Surprisingly, SVI learns the global parameters much faster than CAVI. Using only 10% of the articles, the algorithm managed to learn useful topics--much faster than CAVI, where the results won't be servicable even after passing through all the documents. Hoffman's paper https://papers.nips.cc/paper/3902-online-learning-for-latent-dirichlet-allocation.pdf supports this claim.

The main thing I would change in this project submission is the ELBO calculation. Computing the objective function is much slower than the update step. It turns out that ELBO is typically evaluated on a small subset of the data to make the runtime reasonable. We didn't know at the time, and would've made changes with that knowledge.
