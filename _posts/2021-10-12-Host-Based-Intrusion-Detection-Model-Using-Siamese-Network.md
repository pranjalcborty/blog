---
layout: post
title: "[Review] Host-Based Intrusion Detection Model Using Siamese Network"
tags: HIDS CNN LID-DS Review
---

### [Host-Based Intrusion Detection Model Using Siamese Network, May 2021](https://ieeexplore.ieee.org/document/9436776)

#### Key informations
* Dataset: **Leipzig Intrusion Detection Data Set (LID-DS), 2018**, NSL-KDD.
* Architecture: Siamese-CNN (few-shot learning), treating the dataset like an image dataset.
* Proposed architecture performs 6% better than vanilla CNN.

#### Previous works
* [Laskov et al.](https://link.springer.com/chapter/10.1007/11553595_6): Used KNN, MLP, K-means, SVM, Decision Tree for intrusion detection and compared their performances using ROC curves.
* [Le et al.; Kim and Kim](https://ieeexplore.ieee.org/document/7883684): Conducted study to solve high false alarm rates, using SVM, KNN.
* [Kim et al.](https://arxiv.org/abs/1611.01726): Used LSTM (language modeling method) for abnormal behavior based intrusion detection. Used better approach to resolve high false alarm rate.
* [Khan et al.](https://ieeexplore.ieee.org/abstract/document/8854549): Used CNN on KDD99.
* [Upadhyay et al.](https://www.researchgate.net/publication/308411267_Application_of_Convolutional_neural_networks_to_intrusion_type_recognition): Used CNN on KDD99.

#### Information from the paper
* Two types of intrusion detection: Misuse detection & Anomaly detection.
* *Attack types*: DoS (Denial of Service), U2R (User versus Root), R2L (Remote versus Local), Probe attack.
* *Datasets used in previous research*: KDD99, UNM (System call data), ADFA (2013, Relevant for modern systems, System call data).
* *Few-shot learning*: Meta-learning & Metric-learning.
* *Steps of the work*: LID-DS, preprocessing, image generation, Siamese Network, Siamese-CNN, and N-way K-Shot Learning.

#### Possible improvement(s)
* Could have tried **'image augmentation'** to diversify the dataset, as already treating the dataset like images.