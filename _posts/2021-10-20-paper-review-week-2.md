---
layout: post
title: "Paper Review (Draft) - Week 2"
author: "Pranjal Chakraborty"
---

### [LR-HIDS: logistic regression host-based intrusion detection system for cloud environments, October 2018](https://doi.org/10.1007/s12652-018-1093-8)

#### Key informations
* Dataset: NSL-KDD
* Architecture: Feature selection using Logistic Regression; Classification done using **Bagging Algorithm** (MLP, DT, Linear Discriminant Analysis)
* Targeted for cloud environments (virtual machines)

#### Information from the paper
* Important features are selected using factor without regularization, derived from Logistic Regression. (Why not p-values? Not discussed.)
* Very high accuracy than the previous works

#### Possible improvement(s) or extension(s)
* Can be applied on custom datasets and check the robustness of the technique

### [Anomaly Generation Using Generative Adversarial Networks in Host-Based Intrusion Detection, 2018](https://ieeexplore.ieee.org/abstract/document/8796769)

#### Key information
* Dataset: ADFA-LD
* Architecture: Cycle-GAN
* The purpose is to detect anomalies

#### Information from the paper
* Converted existing data into images and produced synthetic anomalous data using GAN to balance the dataset
* Used MLP for classification

#### Possible improvement(s) or extension(s)
* Introducing data augmentation befor CycleGAN could be interesting
