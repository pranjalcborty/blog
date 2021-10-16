---
layout: post
title: "[Review] SCADS: A Scalable Approach Using Spark in Cloud for Host-based Intrusion Detection System with System Calls"
tags: HIDS Spark ADFA-LD Review
---

### [SCADS: A Scalable Approach Using Spark in Cloud for Host-based Intrusion Detection System with System Calls, Sep 2021](https://arxiv.org/abs/2109.11821)

#### Key informations
* Deployed Spark clusters in the cloud (Google Cloud) to scale.
* Dataset: ADFA-LD.
* Architecture: Logistic Regression w/ limited memory BFGS (LR-LBFGS), SVM.

#### Previous works
* [Haider et al.](https://ieeexplore.ieee.org/document/8003385): Proposed Nested-Arc Hidden Semi-Markov Model (NAHSMM) to improve training efficiency of HMM.
* [Chen et al.](https://ieeexplore.ieee.org/abstract/document/7880607): Achieved high speed incremental learning of data streams by implementing a real-time self-structuring learning framework, AnRAD.

#### Information from the paper
* Used multiple-length n-gram method for preprocessing, feature extraction and testing on ADFA-LD. Generated TF-IDF from the word-vectors.
* AUC is used to evaluate detection accuracy.
* Designed an RDD repartitioning method using Spark API, to transform raw system call RDDs into RDDs with more partitions. When they were loaded and cached, they might not have been enough partitioned. This step is important for even distribution of partitions to the worker nodes.

#### Possible improvement(s)
* How computationally expensive it will be if we deploy NN architectures in the clusters?