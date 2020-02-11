# Bayesian Generative Active Deep Learning
## Introduction
There are two interesting approach to design effective training methods that require small labele training sets:
* data augmentation  
It artificially generates new training points, but it indiscriminately generates samples that are not guaranteed to be informative.
* active learning  
It selects the "most informative" subset of unlabeled data to be labelled by an oracle, but it may be insufficient for the training process and overfit the informative training sets due to the small sizes.

In this paper, the authors combines active learning with data augmentation - Bayesian generative active deep learning approach. This work is mainly inspired by the following works:
* Query by synthesis active learning (Zhu & Bento, 2017)
* Bayesian data augmentation (Tran et al., 2017)
* Auxiliary-classifier generative adversarial networks (__ACGAN__) (Odena et al., 2017)
* Variational autoencoder (__VAE__) (Kingma & Welling, 2013)  
Specifically, they use the concept of Bayesian active learning by disagreement (__BALD__) (Gal et al., 2017; Houlsby et al., 2011) to select informative samples, the samples are then delivered to an oracle for annotation and to the __VAE-ACGAN__ for artificial samples generation.

## BALD
This scheme measures the acquistion function by the "mutual information" of the __training sample__ with respect to the __model parameters__. Because the evaluation of the acquistion function is based on the model __uncertainty__, we need to get the approximation of the posterior distribution of the model parameters. Specifically, Monte Carlo dropout method is used to approximate the acquisition functions. In this paper, the authors also adopted this method.

## Generative active Learning
Generating informative samples can significantly accelerate the training process in active learning. In Zhu & Bento's work, the GAN model has been pre-trained and the optimization during generation is solved efficiently. However, it means that the GAN model is not fine-tuned  in the training progresses, the generative and discriminative models do not __"co-evolve"__.
In this paper, the generation processing is conditioned on slected samples and the learner and Xthe generator are jointly trained, i.e. "co-evolve" during training. They show the generated samples belong to the sufficiently small neighborhood of the target empirically and mathmatically.  

![](archi.png)
## Information-Preserving data augmentation for active learning
In the above architecture, they combines BALD and Bayesian Data Augmentation (__BDA__):
BALD selects data according the formula: x* = argmax a(x,M), where a(x,M) is the acquisition function related with Shannon entropy.
BDA comprises a generator, a discriminator and a classifier. The input is a latent variable u (e.g., a multivariate Gaussian variable) and a class label y, the generator maps the tuple(u,y) to a data point x_a = g(u,y).
In this paper, they modify BDA by fedding the sample X adn the correspoding label y istead of the latent variable u in the prototype.
Specifically, the BDA is based on __ACGAN__ and __VAE-GAN__, where the VAE decoder is also the generator of GAN, the combinition is so called __VAE-ACGAN__.

## Summary and criticism
Instead of the traditional approach that is pool-based, this work combines query and synthesizing.
This work is inspired by many other works, and the main parts in the framework are based on the variants or combinition of other works.
The author mentioned that the computational cost is slightly higher than BDA.
Note that the proposed approach is model-agnostic, thus can be integrated with other active learning methods.

### Inspirition
*BALD can serve as a selection policy by measure the model uncertainty
*The generation parts can refrence many other current works
*Model-agnostic approach can provide the generality to other methods

